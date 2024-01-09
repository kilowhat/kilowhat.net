---
layout: default
title: Cimaise - Albums for Flarum
permalink: /flarum/extensions/cimaise
redirect_from:
  - /flarum/extensions/albums
nav_order: 50
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-cimaise/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-cimaise){: .extiverse-badge}

- **Price**: 30 USD / 50 USD lifetime license (special price for early access: non-profit/for-profit)
- **Bundled translations**: English and French
- **Flarum compatibility**: 1.2+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-cimaise)
- See on [Flarum Discuss](https://discuss.flarum.org/d/32138)

Table of content:

- [Introduction](#introduction)
- [Early Access](#early-access)
- [Changelog](#changelog)
- [Demo](#demo)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Storage](#storage)
- [Conversions](#conversions)
- [Exif](#exif)
- [Drafts](#drafts)
- [Approval](#approval)
- [Licenses](#licenses)
- [Image editor](#image-editor)
- [Albums](#albums)
- [Discussion albums](#discussion-albums)
- [Global settings](#global-settings)
- [Leftovers and unfinished features](#leftovers-and-unfinished-features)

## Introduction

Cimaise is a premium Flarum extension that adds picture albums to your forum.

Albums and pictures are standalone entities with their own pages and permalinks.

You decide if any user can create their own albums or if they can only add to moderator-created albums.

Pictures have a title, description and license information (license type and author name).
Optionally, you can require each picture to be approved.

You can connect an album to a discussion so that each new picture triggers an event post and optionally attached to a comment.

An image editor is included to crop images, mask areas and add stickers.
The edits are fully modifiable and reversible by moderators.

On the picture page, the Exif data (camera make, exposure, geolocation, etc.) is displayed together with an optional map powered my Mapbox.

At the moment, a picture can only exist in a single album.
Pictures are not meant to be embedded externally as image links can change during certain edits.

### What does "Cimaise" mean?

To distinguish the extension from other potential "Album" extensions (particularly if they are compatible are used together) and following the convention I started with my previous premium extensions, I named this extension after a word from the [French dictionary](https://fr.wikipedia.org/wiki/Cimaise).

The word has many meanings in architecture, arts and others.
I think the most fitting definition here is the wall or apparatus used to hang paintings in a museum.

## Early Access

The extension is currently in "early access". This means:

- You get access to the extension at a discounted price, and you will receive the full extension when it releases in early 2023.
- A few features are still missing that will make the use in production a bit tricky.
- There are still some bugs and suboptimal UX.
- Not all texts can be translated. Many texts will be rewritten and/or moved for the final release.
- The bundled French translation is not up-to-date with English but will be completed when texts are deemed final.
- The database structure might still receive big changes, but a way to upgrade will be provided.

Early access customers are encouraged to share their feedback in the official extension discussion so any bug can get addressed and their suggestions implemented if they fit within the scope of the extension.

The extension already meets the same security expectations as my other extensions:

- Access control for all resources is implemented.
- All visible permissions are implemented.
- Uploads are already protect against possible attack vectors.
- Any security issue will be promptly addressed through a patch release.

Translators, please do not spend too much time on this extension yet.
I will rename many of the translation keys until the final release.

The following features are still on the TODO for the final release:

- A way to manage server storage, to see used disk space and set per-user and global limits.
- A way to manage drafts and soft-deleted content and choose how they will be permanently deleted.
- A more logical gallery browser in the lightbox where pictures are sorted in the same direction as in the discussion.
- A list of user albums on their profile.
- Asynchronous queue support for conversion generation.

The following features are planned but will probably be implemented after leaving early access:

- Cloud disk settings (S3-compatible first, others later).
- Scout search integration.
- Custom Paths compatibility.
- Ability to publish pictures without albums.
- Ability to publish pictures in multiple albums.
- Ability to assign tags to pictures and use them as filters when browsing the album.
- Ability to hide pictures from the main view of the album and only show them when specific tags are selected.
- Ability to embed a standalone album inside a post, and create it on the fly if needed.

The following features have been considered but are currently not planned.
They can be implemented if there is demand:

- Ability to comment on pictures.
- Ability to upload animated pictures or other types of content.
- Ability to rotate pictures in the editor.
- Ability to add text or highlight to the editor.
- Ability to resize or compress original images before storing them on the server.
- Hotlink protection with access control.

## Changelog

### Version 1.0.4 - January 9, 2024

- Fix compatibility with MariaDB.
- Fix inability to un-crop via REST API.

### Version 1.0.3 - January 9, 2024

- Fix error when submitting picture if licenses are not setup.
- Update code to reduce number of deprecation warnings.

### Version 1.0.2 - August 9, 2023

- Fixed permission issue that allowed anyone with "upload picture" permission to upload to personal albums they don't own.
- Fixed messages not appearing on the page if an error happens during picture submission.
- Modified picture error messages to reference which attribute the user is not authorized to edit for easier troubleshooting.

### Version 1.0.1 - July 9, 2023

- Fixed multiple issues related to EXIF-tagged portait or upside-down images.
  - Fixed image not orientating itself when re-generating thumbnails. This would happen when editing mask stickers, cropping, or manually re-creating thumbnails.
  - Fixed `original_width` and `original_height` picture attributes not taking into account Exif orientation. This affected the placement of stickers in viewbox, even if the image was correctly orientated.
- Fixed stickers overflowing outside the image viewbox.
- Modified image editor to prevent resizing stickers below the minimum backend-validated size. It was previously very difficult to find the sticker that caused the error or resize it to just barely the accepted size.
- Reduced minimum sticker size to 6px instead of previous 10px.
- Fixed lightbox exit button sometimes not being clickable.
- Added new options to `cimaise:migrate` CLI command: `--refresh-exif`, `--refresh-width-height`, `--refresh-filesize`.

If your database contains any image with Exif-tagged orientation you should run the following commands after the update.

`upgrade` with `--refresh-width-height` will correct any invalid original width/height value:

    php flarum cimaise:upgrade --refresh-width-height

If you have any image rendering sideways you can run `conversions:regenerate` to fix them:

    php flarum cimaise:conversions:regenerate

Both commands can take several minutes to run on a large number of pictures.
There is a progress bar rendered when running.
The last command might not be necessary if you never edited any of the pictures after the initial upload.

### Version 1.0.0 - December 15, 2022

Initial early access release.

## Demo

Visit https://clark-flarum-demo.http418.ch/albums to see the extension in action.
You can register and upload your own pictures for testing.

A demo with the ability to see/test the admin side will be made available later.

## Requirements

- Flarum 1.2+
- PHP 8.0+
- MySQL 5.7.8+ or MariaDB 10.2.7+ (for `JSON` data type support)
- You must have SSH and Composer access on the Flarum hosting

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Most other Flarum extensions should be compatible.

As time goes on this section will be filled with any extension that could be incompatible.

## Installation

> Please make sure you understand the limitation of the [early access](#early-access) conditions before purchasing.

- Purchase the ["KILOWHAT Cimaise"](https://extiverse.com/extension/kilowhat/flarum-ext-cimaise) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-cimaise`
- Open the Flarum admin panel and enable the extension
- See below for the settings
- Raise `upload_max_filesize` limit in `php.ini` if needed

## Update

When an update is available, the [Changelog](#changelog) will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/32138).

You can use the following commands to update:

    composer require kilowhat/flarum-ext-cimaise
    php flarum migrate
    php flarum cimaise:upgrade
    php flarum cache:clear

## Support

If you are having issues with the extension, check the following:

- If the extension doesn't install, check you have correctly configured Extiverse's private repository.
- If an error happens during activation or usage of the extension, check the logs in `<flarum>/storage/logs`.

If you are still having issues, please copy the output of the logs above, as well as the output of `php flarum info` and send an email to <support@kilowhat.net>.

Support is provided on a "best effort" basis.
Most replies should usually be within 24h.

I only provide help solving specific issues with the extension.
I won't install the extension for you.

## Storage

In the early version, the storage path cannot be customized.
All files are stored in `<public>/assets/albums/`.

Future versions will include the option to customize the CDN prefix or use external storage methods.

The files are stored with the following filenames:

- `/albums/<picture id>/<view token>/<conversion>.jpg`
- `/albums/<picture id>/original-<source token>.<ext>`

The URL parts have the following purpose:

- `<picture id>` is the sequential MySQL ID.
- `<view token>` is a random 16-character value available to everyone who can view the picture resource. It changes every time the picture is edited or soft-deleted. It ensures drafts and deleted images can't be enumerated. It also intentionally breaks any existing hotlink on soft deletion.
- `<source token>` is a random 32 character value available to the picture owner and moderators.
- `<conversion>` is one of the configured conversion sizes. See "Conversions" chapter for details.

The original file is not 100% verbatim because it receives additional Exif from PHP during the upload process, but it's otherwise untouched and will be used to re-generate conversions if needed.

## Conversions

Conversions are pre-generated resized versions of the image.

In the early version, only built-in conversions are available.
Future versions will allow customization of the conversions via an extender.

A conversion is only generated if the source image is smaller or equal to its size.
`150` and `full` are always generated.

Conversions are always in JPEG format.
Future versions will allow customizing the format and compression.

The following conversions are built-in:

- `150` (square, zoomed in to fill)
- `400`, `800`, `1400`, `2048` (max width or height, whichever is largest)
- `full` (1:1 to original)

All conversions are built from the cropped+masked image and don't contain any Exif data.

The frontend is designed to select the best conversion to display based on the context, but this is still a work in progress.
The 2048 picture (or lower if not available) is currently always used when showing the picture in full.

## Exif

The Exif data of every picture is always extracted from uploaded images and stored into the database.

Users with the "View Exif" permission will see that data on the picture page/lightbox.

Exif tags which are not recognized by PHP will not be displayed but are still stored in the database in case they might be useful for a future update.

Any user with access to Exif data will be able to see the picture geolocation if the picture contains it.

Optionally, that geolocation data can be used to additionally render a map.
To enable, fill in the **Mapbox Token** in the extension settings.
At the moment the map is a static image.
It's planned to add an option for an interactive map in the future.

## Drafts

After a picture is added through the file upload modal, it will exist on the server but can only be modified by its author.

The user can then edit the title, description, author, license and use the image editor as many times as they want before they decide to publish the image.

A draft image will not be visible to anybody when browsing the album, but any existing draft will appear again when re-opening the upload modal.

Drafts are attached to an album and cannot be moved to another album.

Drafts can be deleted from the upload modal.

Drafts are currently not auto-deleted, this will be added later on.
There will be a customizable duration after which drafts are permanently deleted through the scheduler.

## Approval

Similarly to discussions and posts in Flarum, you can customize which users will be subject to approval through permissions.
There is a separate permission for personal and community albums.

When a picture is put under approval, a gavel icon will be shown on the picture.
It will be visible to the author and all moderators in the album and under "all pictures".

If the album is connected to a discussion, the event post or comment that contains the pictures will immediately be published, but the picture will be blanked out and shown to everyone as awaiting approval.
The same happens if a picture is manually reverted to approval after having been already approved.

## Licenses

A license can be specified on each separate picture.
It's comprised of 2 attributes:

- A license name and description, to be picked from a list configured in the admin panel.
- An author name, which can be any string of 3 to 255 characters.

The author field is always optional.
A default author name is automatically pulled from the Exif data if available.

The license name is optional by default but can be made mandatory with the "Require selecting a license" setting in the admin panel.

If (zero) or (one + "Require selecting a license") licenses only are configured in the admin panel, the user will not be prompted to choose a license during upload.

When configuring a License in the admin panel, the following attributes are available:

- **Key**: a unique value used to identify this License in the database. You shouldn't change it once a license has been used as it will break connections to existing pictures which will then show the orphaned old key as license.
- **Label**: a translatable license name. Will be visible in the license choice dropdown and next to the copyright icon on the picture page.
- **Description**: a translatable description. Will be visible behind an info icon next to the license label.

You should make sure your website terms of use cover what licensing applies to content without an explicit declaration to avoid any confusion.
In particular, you might want to reserve your rights to use the uploaded content for commercial use yourself if you allow users to select a non-commercial license on your for-profit website.
Consult your legal team.

## Image editor

After a draft has been created, the image editor becomes available in the upload modal.

The image editor can also be accessed later through the 3-dot menu on the picture page.

The editor is powered by [Fabric.js](http://fabricjs.com/) which is dynamically loaded from the `jsdelivr.net` CDN when the editor is opened.

The picture editor offers 3 features:

### Crop

To crop, click the crop button at the top right.
Handles then appear on the picture to choose the visible area.

### Mask

Masks allow to hide parts of the image for privacy.

2 shapes are available: rectangle and disc.

Drag and drop the shape from the panel on the right on top of the picture.
You can then scale the shape or rotate/resize for the rectangle.

A Mask is filled with a flat color.
There's no blur.

During editing, the color of the Mask will automatically update to match with the content behind it.
You can click on the color square in the list of layers on the right to manually set a different color.

The Masks will be "burnt" into the conversion files and the original content will not be visible to regular users.
However, the Masks can still be edited or removed later and new conversions will be re-created from the original unaltered file.

### Stickers

The Stickers panel only appears if at least one Sticker has been configured in the admin panel.

Editing works similarly to Masks, except they are not "burnt" into the conversion files and can be hidden from the UI.
At the moment they become semi-transparent when the mouse hovers the picture but a future version will add an option for users to hide Stickers altogether.

Stickers can be resized and rotated, but will retain their width/height ratio.
They cannot be recolored.

When creating a Sticker in the admin panel, the following attributes are available:

- **Key**: a unique value used to identify this Sticker in the database. You shouldn't change it once a sticker has been used as it will break existing edits.
- **Label**: a translatable value to display in the Sticker list and layer list of the image editor. This value might also later be visible to visitors when they click on a Sticker on a picture.
- **URL**: a fully qualified URL to the Sticker image. Any image supported by a browser can be used, including but not limited to PNG, JPEG and SVG. At the moment there is no upload feature for Stickers, you must place them on your server yourself and copy the URL. You can place them on any domain, but make sure the cross-origin configuration allows embedding the images in a canvas. This image will never be retrieved server-side.

## Albums

There are 2 types of albums:

- **Personal**: only the album owner (if they have **Upload pictures** permission) and moderators can upload pictures.
- **Community**: any user with permission **Upload pictures** can upload pictures.

Once created, the type of the album cannot be changed.
It might be added in a future version.

All albums are visible to all users with "View" permission.
There are no private albums.

## Discussion albums

This feature closely combines a single album with a single discussion so that the discussion can serve as a kind of "timeline" for the album.

The combination can either be created automatically via the "Automatically create an album for every new discussion" setting or by manually attaching an album through the discussion dropdown menu.
Manually attaching albums to discussions is only meant for moderators as giving the permission will allow modifying this setting for any discussion on the forum.

While this is not the intended use case, multiple discussions can be connected to a single album.
I recommend not doing so, please notify me if you are using this feature.

When the album and discussions are combined, picture can be uploaded from either the album page or the reply composer.

When uploading from the reply composer, the new pictures will be associated with the comment.

Pictures can be de-selected in the post preview.
Those pictures will not be published but will remain as drafts and re-appear the next time the upload modal or reply composer is open.

When uploading from the album page, the new pictures will make a new event post appear in the discussion showing the pictures that were just added.
If more pictures are uploaded later, the event posts will be combined if there were no upload or comments by other users in the meantime.

If the user has the "Publish pictures silently" permission, an additional checkbox will be available when uploading from the album.
This allows skipping the creation of an event post.

## Global settings

The following settings auto-save when modified:

**Watermark image**: upload a file to be applied 1:1 on top of all conversions except `150`.
The watermark will not be resized if larger than the conversion.
The file will be stored in the same place as the forum logo and favicon (`<public>/assets` unless customized through another extension).
It's placed there for ease of implementation, so it can be shown in the admin panel but the URL is never shown to the users and only read from PHP when creating conversions.

The following settings must be saved with the button at the bottom of the page:

**Watermark placement**: controls in which corner of the image the watermark is applied.

**Automatically create an album for every new discussion**: see "Discussion albums" chapter.
This setting will automatically create and assign albums with identical titles for new discussions in any tag.

**Never synchronise discussion and album titles**: see "Discussion albums" chapter.
This disables the synchronisation if identical titles between albums and discussions if that behaviour is unwanted.

**Column theme**: changes how the "picture show" page and the lightbox look.
By default, the picture meta is shown in a panel below the picture.
With this option enabled, the picture meta is shown in a side panel on the right of the image.
Depending on the aspect ratio of the image, this impacts the size of the displayed image.
On mobile, both options look identical with the meta below the picture.

**Mapbox Token**: enable the geolocation map. See "Exif" chapter.

**Require selecting a license from the list below**: see "Licenses" chapter.

**Licenses**: see "Licenses" chapter.

**Stickers**: see "Image editor" chapter.

## Leftovers and unfinished features

The following features still exist in one form or another in the source code but will still be refactored or removed at a later point:

- **Favorites**: moderators can promote pictures to favorites. Favorite pictures are pushed to the top of the list no matter the upload date.
- **Take date**: currently pulled from the Exif data when available. Will be fillable by the user in a future version.
- The PHP event **AlbumPublicPicturesChange** should not be used. More comprehensive events will replace it later on.
