---
layout: default
title: Rich Embeds
permalink: /flarum/extensions/rich-embeds
nav_order: 50
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-rich-embeds/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-rich-embeds){: .extiverse-badge}

- **Price**: 20 USD lifetime license
- **Bundled translations**: English
- **Flarum compatibility**: 1.2+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-rich-embeds)
- See on [Flarum Discuss](https://discuss.flarum.org/d/30516)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Features](#features)
- [Extension settings](#extension-settings)
- [Site-specific integrations](#site-specific-integrations)
- [Commands](#commands)
- [MySQL requirements](#mysql-requirements)

## Introduction

Rich Embeds is a Flarum extension that adds previews to links posted in discussions.
The previews are generated from OpenGraph data or an optional fallback method.

The data crawling is performed by the Flarum server without any external service and is cached for fast retrieval and minimal impact on page load times.

Images and favicons can optionally be proxied through the server to protect the visitor's privacy.

A whitelist or blacklist of websites can be configured to control which websites are previewed and prevent abuse of the proxy script.

Optionally, the extension will also retrieve and display metadata of images embedded into posts with bbcode or markdown. 

<div class="picture-row">
<img src="/medias/extensions/rich-embeds/post.png" alt="Post with 2 different styles of embed">
<img src="/medias/extensions/rich-embeds/api-powered.png" alt="4 websites with API-powered embeds">
</div>

## Changelog

### Version 1.2.1 - July 25, 2022

- **Fixed** Rich Images wrapped in links not rendering correctly.
- **Fixed** Alt text missing from Rich Images.
- **Fixed** MySQL version check not comparing the correct numbers.

You must clear the Flarum cache for the alt text fix to be applied.

See 1.2.0 release notes if you are upgrading from an older version.

### Version 1.2.0 - July 24, 2022

- **Added** Scan command for import and update after permission changes.
- **Added** Refresh command to mass-refresh embeds.
- **Added** API-powered Flarum embeds (discussions+users).
- **Added** API-powered GitHub embeds (repos+issues+pulls).
- **Added** API-powered YouTube embeds (videos).
- **Added** API-powered Google Drive embeds (files).
- **Added** Embedded player on YouTube links.
- **Added** Popover on links that failed rendering to give access to refresh controls.
- **Added** MySQL version check during extension activation.
- **Changed** Tweaked colors and margins.
- **Changed** No longer proxying images to the same domain as Flarum.
- **Fixed** Links containing ampersands wouldn't render as blocks.

You must run `php flarum migrate` immediately after performing the update.
Trying to create discussions or posts before the migrations have run will lead to errors.

If you get an error saying your MySQL version is unsupported, see workaround in [MySQL requirements](#mysql-requirements) and please report your `select version() as version` SQL command output and I'll get it fixed ASAP.

Most of the new features are disabled by default.
Visit the extension page in the admin panel to configure.

Just like in previous versions, the MediaEmbed feature from FoF Formatting has priority over regular links.
This means the new YouTube and Google Drive rich embeds can only be used when MediaEmbed is disabled.

<details markdown="1">
<summary markdown="span">Show older releases</summary>

### Version 1.1.0 - June 1st, 2022

- **Added** Rich image embeds feature. Disabled by default.
- **Changed** Rich link previews now show the domain name of the destination website if the URL was a redirect instead of the domain name from the posted link.
- **Changed** Any link longer than 2048 characters is now automatically blacklisted and cannot be previewed.
- **Fixed** errors when inserting links longer than 255 characters.
- **Fixed** blacklist/whitelist not being applied to HTTP redirect destination.
- **Fixed** favicon not aligned properly with text.
- **Fixed** post preview now debounced to avoid many requests and crawls being performed if a URL is typed by hand.
- **Fixed** inline preview not switching to page title label when entering a link without ending slash.

This update also started collecting image Exif data, but this information is currently not displayed.
It might be made visible in a future update.

You must run `php flarum migrate` immediately after performing the update.
Trying to create discussions or posts before the migrations have run will lead to errors.

### Version 1.0.2 - April 10, 2022

- **Fixed** image proxy toggle not being applied.

### Version 1.0.1 - April 4, 2022

Initial release.

</details>

## Requirements

In addition to [Flarum's server requirements](https://docs.flarum.org/install/#server-requirements), you need:

- Flarum 1.2+
- PHP `libxml` extension
- MySQL 5.7.8+ or MariaDB 10.2.7+ (for `JSON` data type support)
- SSH and Composer access on the Flarum hosting

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Rich Embeds overrides the TextFormatter `URL` rendering template and as such may conflict with other extensions.

When image embeds are enabled, the `IMG` rendering template is also overridden.

This page will be kept up to date with any known incompatibility that can't be worked around.

### MediaEmbed

The MediaEmbed feature provided by the FoF Formatting extension will always take priority over Rich Embeds.

If you want to use the YouTube API/player or Google Drive API embeds, you will need to disable MediaEmbed.

## Installation

- Purchase the ["KILOWHAT Rich Embeds"](https://extiverse.com/extension/kilowhat/flarum-ext-rich-embeds) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-rich-embeds`
- Open the Flarum admin panel and enable the extension
- See below for the settings

If you get an unsupported database error, see workaround in [MySQL requirements](#mysql-requirements).

## Update

When an update is available, the [Changelog](#changelog) will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/30516).

You can use the following commands to update:

    composer require kilowhat/flarum-ext-rich-embeds
    php flarum migrate
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

## Features

### Disabling Embeds

You can disable all embeds on a specific post.

Users with the required permission will see a button appear when they hover any embeds on a post.
After accepting the confirmation modal that appears, all embeds will be detached from that specific post.

There is currently no way to re-enable the embeds on a post that has been disabled.
An option will be added in a future update.

In the meantime if you must re-enable embeds on the post, you can edit the `kilowhat_rich_embeds_disable` column on the `posts` table in the database manually.

### Refreshing Embeds

Users with the matching permissions are allowed to request an update of the crawled data for an embed.

Please be careful with this permission as there is currently no rate limiting that controls how often you can request new previews.

When an identical link is posted again in a new post, a refresh is not automatically requested (the existing cached data is always used).
Only users with the permission can manually request a refresh for a URL.

### OpenGraph Parser

This extension includes a custom parser that follows the [OGP specification](https://ogp.me/).

A "fallback" parser takes care of retrieving the favicon as well as optional fallback values in case OpenGraph data is missing.
See documentation [on the corresponding setting](#generate-rich-embeds-for-pages-without-opengraph-data).

### Whitelist

You can control which websites can be embedded in posts through a blacklist and/or whitelist.
See documentation [on the whitelist setting](#url-whitelist-and-blacklist).

Admins and moderators are subject to the same rules as regular users and can't add previews to websites that are not whitelisted.

Existing previews that were generated before a setting change will not be deleted.

### Importing

A future update will add a way to generate previews for all existing posts in the database.

In the meantime, you need to edit at least one character in a post and save it to have the previews generated.

## Extension settings

All settings can be found in the extension page of the admin panel.

### Layout

Controls the positioning of the link preview around the original link:

- **Inline**: replaces the link text with the crawled page title and adds the favicon in front of the text. Hovering the link reveals the preview block.
- **Block** (default): replaces the link with the full preview block.
- **Separated**: the post content is not altered. Preview blocks are added below the post content.

Notes:

**Inline** is automatically used for links without OpenGraph data, links where OpenGraph parsing failed, and links with custom labels.

**Separated** mode currently doesn't auto-updates during post editing. It updates after the post has been saved.

### Style

Controls the look of the block preview:

- **Vertical** (default): The images are placed under the text content and takes the full width of the block.
- **Horizontal**: The images are placed to the right of the text content.

### Image Proxy

Proxies all images and favicons through Flarum's server.

The origin server will only see the "Guzzle" user agent (the library used internally for requests) and the server IP.

Flarum will only perform the proxy request if the image URL is whitelisted, and will only return the response if the returned `Content-Type` starts with `image/`.

### Generate rich embeds for pages without OpenGraph data

When this option is enabled, a fallback preview will be generated from the page's `<title>`, `<meta>` and `<img>` tags in the page body.

These previews might not look as good as OpenGraph previews because the data crawled this way might not have been intended to be displayed in a preview.

### URL Whitelist and Blacklist

These 2 settings control which URLs will have previews generated as well as the URLs that can be sent through the image proxy.

Each entry in the lists should be separated by a newline.

Each entry can be either a domain name or a regular expression.

A domain should contain only the host part of a URL without any protocol or path, for example `www.youtube.com` or `github.com`.
Subdomains of the given domain will automatically be accepted as well.

Regular expressions should include delimiters and modifiers.
The accepted delimiters are `/` or `~`.
Make sure to include the `i` modifier for case-insensitive matching.
The expression will be evaluated against the raw URL typed by the user with [`preg_match`](https://www.php.net/manual/en/function.preg-match.php).

All URLs are already validated with PHP's `FILTER_VALIDATE_URL` and TextFormatter's `#url` filter so you don't need to repeat any such validation in your regex.

Don't forget to whitelist the domain names of any CDN server used by your whitelisted website's OpenGraph images.

The extension will automatically blacklist all URLs that include private range IPs, unless you explicitly whitelist them.
Consider blacklisting your internal domain names if the server is not isolated.

### Rich Embeds for Images

*This feature is experimental. Feedback is welcome!*

Image embeds are an optional feature you can enable via the extension settings.
After changing the setting you must clear the Flarum cache manually using the button in the admin panel or the `php flarum cache:clear` command.

When this feature is enabled, the same preview crawler used for links will parse all image links from the post.

If the image URL is whitelisted and returns a 200 HTTP code with `image/*` MIME type, the image in the post will show additional information on hover.

The image overlay will show the image format, resolution, file size and domain name.
It will also contain controls to copy the image URL or open it in a new tab.

Exif metadata is also collected and will be shown in a future update.
Suggestions for how to use this data are welcome!

If an image metadata was successfully retrieved, the width and height will also be automatically injected into the DOM.
This prevents the page "jumping" while loading images of unknown size and fixes Flarum jumping to the wrong post when following permalinks in discussions filled with many images.

### Permissions

**View API-powered Google Drive thumbnails**: controls who can see Google Drive file thumbnails when API-powered Google Drive previews are enabled (see below).

**Use embeds in own post**: controls which users can use embeds in their posts.
When a post is edited, it's the author of the post that is evaluated.
If the author of a post was deleted, editing the post will cause all embeds to be removed.

**Disable embeds on own post**: controls which users can remove embeds on posts they have authored.
This option appears after the post has been successfully created.

**Disable embeds on any post**: moderation equivalent of the *Disable embeds on own post* permission.

**Refresh embeds on any post**: gives access to the button to refresh an existing embed.

## Site-specific integrations

The extension is able to render additional information not part of OpenGraph with site-specific HTML scraping or REST API access.

Some of these features rely on external APIs which might come with rate limits or fees.

Information collected from the external APIs is never exposed directly to the client.
The full API responses are stored in the database but only some whitelisted fields are used to build the rich-"er" previews.

### Flarum

**Enable advanced Flarum previews**: This feature parses additional JSON data already included in the HTML by all Flarum-powered forums.
It will work with any forum that runs Flarum 1.4+ and advertises the `X-Powered-By` Flarum header.

This feature does not require any third-party credentials and therefore cannot incur any cost.

The feature might not work properly or at all on heavily modified forums.
It's designed to fail gracefully by displaying only the available information and falling back to OpenGraph.

Disabling the feature will immediately hide the data on existing embeds.
The data is preserved and won't be queried again if the feature is re-enabled later.

The following information will be displayed:

- For discussions:
  - Title
  - Replies count
  - Participants count (number of different users)
  - Start date
  - Excerpt from first post (if the link points to the start of the discussion)
  - Up to 2 images from first post
- For user profiles:
  - Display name
  - Avatar
  - Bio (if FoF User Bio extension is enabled and visible to guests)
  - Discussion count
  - Comment count
  - Join date (if public)

### GitHub

**GitHub API Key**: Fill in to enable API-powered rich GitHub previews for repos, issues and PRs.
This setting acts as both the storage for the key and enables the feature.

This feature has been tested with [Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) but it should also work with app tokens or other method described in the [GitHub REST API documentation](https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api#authentication).
The extension is not able to perform any oauth flow.
The same token will be used to retrieve every embed created by any user.

This feature is intentionally designed to show private repos and issues if the token has access to it.
Make sure to configure permissions correctly to prevent accidental exposure of your private repository information.
Consider creating a GitHub "machine user" for this specific purpose if needed.

This feature performs 1 API request for links to repository index pages, 1 API request for pull request pages and 2 API requests for issue pages.
Other GitHub page links will not cause any API request to be performed.

**Organisation whitelist**: Comma-separated list of GitHub organisations that will use the API-powered preview.
Use this field to prevent every private repo accessible by the API key to be exposed, to reduce API usage or to only change the embed style of your own org.
If left empty, any repo that the API key can access can be previewed.

This setting only applies to new embeds.
Existing embeds that already contain information about other organisations will continue to show their data until manually refreshed.

The following information will be displayed:

- For issues and pull requests:
  - Title
  - Excerpt from body (raw Markdown)
  - Author name and avatar
  - Comments count
  - Creation date
- Additionally, for pull requests:
  - Review count
  - Commit count
- Repository index pages:
  - Private indicator if repo is private
  - Open issue count
  - Watcher count
  - Star count
  - Fork count

If the repository is public and has an OpenGraph image, the image will be shown.
This can cause some information to be shown 2 times, as part of both GitHub's OpenGraph image and the rich embed.

### Google

This section contains settings that will apply to both **YouTube** and **Google Drive** since both rely on the Google API Client for PHP.

The PHP Client is bundled with the extension, so you don't need to install any additional package.

The PHP Client can pick up its configuration from environment variables like `GOOGLE_APPLICATION_CREDENTIALS`.
If you use environment variables, you can leave the fields in this section empty and your credentials will automatically be read (`$client->useApplicationDefaultCredentials()` will be called).

You need to enable the YouTube and Google Drive APIs in your Google Cloud Console project.

**Google SDK API key**: use this setting to provide an [API key](https://cloud.google.com/docs/authentication/api-keys).
The value will be passed via `$client->setDeveloperKey($key)` internally.

**Google SDK Auth Config Path**: use this setting to provide a path to a [JSON file containing the credentials to a Service Account](https://cloud.google.com/docs/authentication/production#manually).
The value will be passed via `$client->setAuthConfig($path)` internally.

Using a Service Account instead of an API Key is useful if you wish to embed private information.
You can share access to your YouTube account or Google Drive with the service account to make the information visible in Flarum.

### YouTube

**Allow playing YouTube videos from the preview**: When enabled an iframe player will be loaded on demand via a new "play" button that appears above the thumbnail in the preview.

This feature is entirely client-side and doesn't require setting up the Google API client.
No request is made to Google server until the play button is clicked.

You might need to adjust your CSP settings to allow frames from `www.youtube.com` to be loaded on your forum.

**Use YouTube no-cookie iframe domain**: When enabled, the domain for the play feature is replaced with `www.youtube-nocookie.com`.

This feature doesn't appear to have a documentation page in Google Developer documentation.
It's called the "Privacy-enhanced mode" in the embed share modal of YouTube's website.

**Enable advanced API-powered rich YouTube previews**: Enables API-powered rich YouTube previews for videos.

The Google API Client must be configured as described in the [Google](#google) section above.

This feature performs 1 API request for each video link (`youtube.com` or `youtu.be` domains).
Other YouTube links won't cause any API request.

The following information will be displayed:

- Medium quality thumbnail returned by the API
- Video duration
- View count
- Like count
- Comment count
- Publish date

### Google Drive

**Enable advanced API-powered rich Google Drive previews**: Enables API-powered rich Google Drive previews for files.

The Google API Client must be configured as described in the [Google](#google) section above.

This feature performs 1 API request for each file link (`drive.google.com/file/[...]`).
Other Google Drive links won't cause any API request.

Additionally, 1 more request is performed to the Google CDN servers for each file thumbnail.
This request doesn't count in the Google API quota.

The following information will be displayed:

- Google Drive site icon is replaced with the Google Drive icon for the file type
- File thumbnail
- File size
- Creation date
- Modified date (if more than 10 minutes after creation date)

Customize the **View API-powered Google Drive thumbnails** permission to make the thumbnail visible to more users.

The file thumbnails are cached by the forum because the links expire within about 1h for non-public files.
If the Flarum cache is cleared, the file thumbnails will be deleted as well.
They will automatically be retrieved again the next time the embed is viewed by a user.
This will cause 1 API request and 1 CDN request again, and be cached.

## Commands

The following commands can be run via SSH.
Connect to your server and `cd` into the Flarum folder to execute them (same place you would run `composer` commands).

**Please read the documentation in detail** before running a command.
The commands can take a long time to complete and can also fill your hosting or external service quotas very quickly.

If you are using the API-powered options, the commands may incur costs for hundreds or thousands of requests.

This website will show the options and behaviour for the latest version of the extension, which might not be the version you currently have.
Use the `php flarum help` command as described to check the complete documentation for your exact version.

### Scan command

Check documentation with `php flarum help kilowhat:rich-embeds:scan`

This command is useful to perform the initial import after you enable Rich Embeds for the first time.
It will scan all comment posts on the forum for links, retrieve each page, create the embed and save the embed relationships.

You can run the command with `--dry-run` first to scan the database but not actually perform any request.
At the bottom of the output you'll see how many images and links have been found.
Those numbers include duplicates of the same links as well as links that already have an embed generated.

```sh
php flarum kilowhat:rich-embeds:scan --dry-run
 123000/123000 [▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓] 100%

Total images scanned 9
Total bbcode scanned 0
Total links scanned 36
```

Once you are ready to start the real import, run `php flarum kilowhat:rich-embeds:scan` and wait for the command to complete.

All underlying API requests will be performed one after another without any wait.
If all links point to the same servers, this could get you throttled.
If that's happening to you, please reach out and I'll see what I can do.

### Refresh command

Check documentation with `php flarum help kilowhat:rich-embeds:refresh`

This command updates the information about existing embeds that match the given conditions.

It can be used in a CRON task to maintain the medata visible in some embeds up to date.
It is most useful when combined with API-powered embeds which contain a lot of additional information, some of which is most useful when kept up to date.

Some example usages:

```sh
# Update all links to your own website, including those created very recently
php flarum kilowhat:rich-embeds:refresh https://*.mydomain.tld/* --any-age
# Update all GitHub embeds that have not been updated in the last 10 days
php flarum kilowhat:rich-embeds:refresh --api-resource="github.*" --older-than="10 days ago"
# Just like the scan command, use --dry-run to get the output but not perform any actual request
php flarum kilowhat:rich-embeds:refresh --dry-run
```

### Process command

Check documentation with `php flarum help kilowhat:rich-embeds:process`

This command is mostly meant for troubleshooting.
You should not need it, but I might ask you to run it if you encounter issues.

Example usage:

```sh
# Call with -v to get the complete JSON output of the OpenGraph, fallback and API parsers
php flarum kilowhat:rich-embeds:process https://discuss.flarum.org/d/30516 -v
```

## MySQL requirements

As described in [Requirements](#requirements), this extension requires a version of MySQL that supports JSON columns.

Trying to enable the extension on an unsupported database will result in an error and a broken database state.

To prevent users accidentally breaking their database, the extension attempts to guess if the MySQL version is supported before installation.

This process is not entirely reliable because the format of the version is different on each operating system and might not be accurate for remote databases.

If you cannot enable the extension due to a false positive, you can disable the MySQL version check by modifying Flarum's `config.php` file:

If you encounter a false positive, please share your output of the `select version() as version` SQL command with me so I can fix it.

```php
<?php return array (
  'debug' => false,
  // [database configuration, headers, etc...]
  // At the end of the array, add:
  'kilowhat' => [
    'ignore-mysql-requirement' => true,
  ],
);
```

After the initial activation of the extension, those additional lines can be removed.

Behind the scenes, the check is performed by a special migration that runs before all other migrations.
Once it has run, it won't run again even if the extension adds new migrations.
