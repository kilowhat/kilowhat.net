---
layout: default
title: WordPress Integration
permalink: /flarum/extensions/wordpress
nav_order: 50
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-wordpress/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-wordpress){: .extiverse-badge}

- **Price**: 5 USD/month or 50 USD/year
- **Bundled translations**: English
- **Flarum compatibility**: 1.2+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-wordpress)
- See on [Flarum Discuss](https://discuss.flarum.org/d/22229-premium-wordpress-integration)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Demo](#demo)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Troubleshooting](#troubleshooting)
- [Integrity considerations](#integrity-considerations)
- [Support](#support)
- [Settings in WordPress plugin](#settings-in-wordpress-plugin)
- [Settings in Flarum extension](#settings-in-flarum-extension)
- [Third-party integrations](#third-party-integrations)
- [How global login/logout works](#how-global-loginlogout-works)

## Introduction

The Flarum WordPress integration is a premium extension developed by Clark Winkelmann.

<iframe width="740" height="416" src="https://www.youtube.com/embed/GyjRB6dEEmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

It offers two main features:

### SSO

<div class="picture-row">
<img src="/medias/extensions/wordpress/login.png" alt="SSO Login modal">
<img src="/medias/extensions/wordpress/welcome.png" alt="Welcome modal">
</div>

Adds WordPress login to Flarum, along with a global single sign-on and sign-out.

User can connect through WordPress or Flarum and will automatically be connected on both platforms.

Logging out will also clear both sessions before redirecting to the WordPress logout page.

Email changes and password resets happen via WordPress.

WordPress SSO can be used alongside normal Flarum login, or replace it completely.

### Comments

<div class="picture-row">
<img src="/medias/extensions/wordpress/embed.png" alt="Embed on WordPress side">
<img src="/medias/extensions/wordpress/summary.png" alt="Post summary on Flarum side">
</div>

Replaces WordPress comments with an iframe containing a Flarum discussion.

Discussions are automatically created by Flarum along with a summary of the WordPress post.

Discussions can be automatically locked and hidden when the comments status is changed in WordPress.

Guest posting is not possible with this integration enabled.

### Admin panel

Some screenshots of the admin panel that you will find in the Flarum dashboard.

<div class="picture-row">
<img src="/medias/extensions/wordpress/dashboard-v2.png" alt="Dashboard">
<img src="/medias/extensions/wordpress/wizard.png" alt="Installation wizard">
</div>

## Flarum changelog

### Version 1.8.1 - March 30, 2023

- Fix WP thumbnail change not always synchronising.
- Fix WP post URL slug change not synchronising.
- Update Symfony dependencies to prevent conflict with other Flarum extensions.

### Version 1.8.0 - March 26, 2023

- Added WP author sync to discussion owner.
- Added WP thumbnail sync and display options.
- Added WP tag override feature for multi-site use cases.
- Added more information to WP request log in Flarum log file and disabled logging completely when debug mode is off.

This update requires PHP **7.4** or **PHP 8.0+**. Support for PHP 7.3 has been dropped.

The new features require updating the WordPress plugin to version 1.5.
See below for WordPress plugin changelog.

Both versions 1.7 and 1.8 of the Flarum extension have been verified compatible with Flarum 1.7.

<details markdown="1">
<summary markdown="span">Show older releases</summary>

### Version 1.7.6 - December 13, 2022

- Fix "WordPress" case in the extension name, documentation and English translations. The namespaces and attributes are unchanged and keep their lowercase "p".
- Fix new comment threads with no replies not showing as unread in Flarum discussion list. It will now show as unread + zero replies which Flarum would not natively do.

This problem appeared in version 1.7.4 when the reply count was fixed for new discussions.

### Version 1.7.5 - November 29, 2022

- Fix some internal Flarum links opening inside iframe instead of expected parent window.

The extension was confirmed working on Flarum 1.6.

### Version 1.7.4 - September 13, 2022

- Fix iframe incorrectly showing 1 total comment despite no comments having been made (fix will apply to new comment threads, existing threads will fix themselves upon first comment)
- Fix Flarum discussion list showing 1 less reply than actual count
- Fix iframe header layout on Flarum 1.5
- Fix reply composer being off-center if the iframe is larger than `1000px`
- Add class name to username pick modal
- Tweak some texts and styling in admin panel
- Make health check errors translatable
- Compile javascript with Webpack 5

The extension was confirmed working on Flarum 1.5.

### Version 1.7.3 - January 16, 2022

- Fix incompatibility with extensions that load `firstPost` discussion relationship (including Blomstra Flag Duplicates)

### Version 1.7.2 - December 15, 2021

- Hide WordPress login button when SSO is disabled
- Add support for query string inside the WordPress custom login path

### Version 1.7.1 - September 19, 2021

- Fix broken link from comments iframe to discussion on forum

### Version 1.7.0 - June 16, 2021

- Flarum 1.0+ compatibility

This version can only be installed on Flarum 1.0 and above.

The new version will automatically be installed when you migrate to Flarum stable with Flarum's official instructions.
Requires **version 1.4** or greater of the WordPress plugin.

### Version 1.6.4 - March 29, 2021

- Flarum beta 16 compatibility

This version can only be installed on Flarum beta 16.

The new version will automatically be installed when you migrate to Flarum beta 16 with Flarum's official instructions.
Requires **version 1.4** or greater of the WordPress plugin.

### Version 1.6.3 - December 28, 2020

- Flarum beta 15 compatibility

This version can only be installed on Flarum beta 15.

The new version will automatically be installed when you migrate to Flarum beta 15 with Flarum's official instructions.
Requires **version 1.4** or greater of the WordPress plugin.

### Versions 1.6.1 & 1.6.2 - November 3, 2020

- Flarum beta 14 compatibility

Version 1.6.1 contained a bug. 1.6.2 fixes it.

This version can only be installed on Flarum beta 14.

The new version will automatically be installed when you migrate to Flarum beta 14 with Flarum's official instructions.
Requires **version 1.4** or greater of the WordPress plugin.

### Version 1.6.0 - August 3, 2020

- Better error handling in case a WordPress plugin interferes with the login redirect
- Add Flarum modal login compatibility with WP-Members WordPress plugin

You can update the Flarum extension via Composer.
Requires **version 1.4** or greater of the WordPress plugin.

### Version 1.5.0 - July 2, 2020

- Add compatibility with FoF Follow Tags, Reflar Webhooks and possibly other extensions
- Fix PHP notice when syncing WordPress posts

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.4.0 - May 22, 2020

- Improve link handling in iframe, now links in user content will also open in `_parent`
- Add support for paths customized through the [Custom Paths](/flarum/extensions/custom-paths) extension

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.3.4 - May 6, 2020

- Flarum beta 13 compatibility
- Remove unused code for features not yet implemented

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.3.3 - April 9, 2020

- Fix HTTP error messages that were not shown correctly in Health check and Wizard

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.3.2 - April 3, 2020

- Add session dropdown to iframe and make title translatable

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.3.1 - April 2, 2020

- Fix WordPress URL HTTPS health check

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.3.0 - April 2, 2020

- New admin dashboard for WordPress
- Added Installation wizard
- Added Health check
- Added "Use post date" option for the comments integration
- Tags for the "Tag for new comment threads" option can now be selected from a dropdown
- Fix for user tokens that would end up in the log file

You can update the Flarum extension via Composer.
Requires version 1.2 or greater of the WordPress plugin.

### Version 1.2.4 - March 10, 2020

- Flarum beta 12 compatibility

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.2.3 - February 23, 2020

- Add `formatContent` method for compatibility with third-party extensions that expect `firstPost` to be a `CommentPost`.

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.2.2 - February 19, 2020

- Add support for excerpts in sticky and summaries extension. Existing WordPress discussions won't have excerpts. You can fix that by manually updating the `first_post_id` in the database.

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.2.1 - January 21, 2020

- Fixed incorrect comments count (was off by 1) being synced to WordPress.
- Fixed incorrect comments count in the iframe (was always 1 less than the real count).

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.2.0 - January 7, 2020

- Added search gambits for third-party integrations

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.1.0 - December 17, 2019

- Added compatibility for custom WordPress login path.
- Added more options for excerpt generation.

You can update the Flarum extension via Bazaar or Composer.
Works with any version of the WordPress plugin.

### Version 1.0.0 - December 10, 2019

Initial release.

</details>

## WordPress changelog

### Version 1.5.0 - March 26, 2023

- Added Flarum tags override feature.
- Added post author ID synchronisation.
- Added post thumbnail synchronisation.
- Fixed capitalization of word "WordPress" in setting descriptions.

The plugin must be manually updated.
The new version can be downloaded via [this link](/download/wordpress/kilowhat-flarum-1.5.0.zip).
Works with any version of the Flarum extension.
The new features work in pair with version 1.8 of the Flarum extension.

<details markdown="1">
<summary markdown="span">Show older releases</summary>

### Version 1.4.0 - August 3, 2020

- Enables the fixes released in the Flarum extension version 1.6.0
- Fixes the post update date being updated each time the comment count changes

The plugin must be manually updated.
The new version can be downloaded via [this link](/download/wordpress/kilowhat-flarum-1.4.0.zip).
Works with any version of the Flarum extension.

### Version 1.3.0 - May 16, 2020

- Added comments shortcode for compatibility with custom theme builders

The plugin must be manually updated.
The new version can be downloaded via [this link](/download/wordpress/kilowhat-flarum-1.3.0.zip).
Works with any version of the Flarum extension.

### Version 1.2.0 - April 2, 2020

- Added Wizard and Health check features
- Added "Use post date" option
- Stop pinging Flarum API about post types that are not synchronized
- Fix posts not being synced when they are created and published at the same time. This was causing issues with plugins that auto-publish posts from feeds

The plugin must be manually updated.
The new version can be downloaded via [this link](/download/wordpress/kilowhat-flarum-1.2.0.zip).
Works with any version of the Flarum extension.

### Version 1.1.0 - January 21, 2020

- Add ability to only enable comments integration for some post types (posts and pages by default). This fixes Woocommerce compatibility as well as probably other plugins.
- Add compatibility with Nextend Social Login plugin.

The plugin must be manually updated.
The new version can be downloaded via [this link](/download/wordpress/kilowhat-flarum-1.1.0.zip).
Works with any version of the Flarum extension.

### Version 1.0.0 - December 10, 2019

Initial release.

</details>

## Demo

A demo/test website is available at <https://wordpress-flarum-demo.http418.ch/>.

The website will be reset manually from time to time.

Please get in touch if you would like admin access.

## Requirements

- **PHP**: version 8.0+ is recommended for both Flarum and WordPress and are the only versions tested by the developer.
- Minimum compatible PHP version are 7.4+ for Flarum (hard-requirement) and 7.3 for WordPress (soft-requirement). WordPress extension might work with lower PHP versions but is unsupported.
- **WordPress** version must be 5.0 or higher (lower might work, but not tested)
- **Flarum** version must be 1.2.0 or higher
- You must have SSH and Composer access on the Flarum hosting
- WordPress and Flarum must be hosted on the same domain, or subdomains of the same domain (cookie limitations)
- WordPress and Flarum must be accessible via HTTPS and HTTP urls must be redirected to HTTPS
- WordPress and Flarum may be hosted on the same server or a different server
- WordPress and Flarum may use the same database (with different prefixes) or a different database

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Most other WordPress plugins and Flarum extensions should be compatible.
The extension makes many changes to WordPress and Flarum logout systems that could cause issues with other extensions.

WordPress plugins/features verified compatible:

- [Shield Security](https://en-gb.wordpress.org/plugins/wp-simple-firewall/): Hide login, Login Captcha.
- [Woocommerce](https://woocommerce.com/): compatible since version 1.1.0 of the WordPress plugin. Reviews and order comments from Woocommerce are left untouched.
- [Nextend social login](https://nextendweb.com/social-login/): compatible since version 1.1.0 of the WordPress plugin. Login via social in WordPress correctly connects into Flarum at the same time. It's recommended to **not enable any social login in Flarum** to prevent any confusion as to which button belongs to which application.
- [WP-Members](https://wordpress.org/plugins/wp-members/): custom login forms compatible since version 1.6.0 of the Flarum extension. There are some edge cases in case you manage to be logged in on one side but not the other, you'll need to logout before logging back in.

WordPress plugins/features verified incompatible:

- [Shield Security](https://en-gb.wordpress.org/plugins/wp-simple-firewall/): 2FA (Flarum login bypasses 2FA).
- [Ultimate Member](https://wordpress.org/plugins/ultimate-member/): custom login forms not supported.

Flarum extensions verified incompatible:

- [FriendsOfFlarum Night Mode](https://discuss.flarum.org/d/21492-friendsofflarum-night-mode): causes the CSS to not load in the comments iframe.

Up to version 1.4.0 of the Flarum extension, [FriendsOfFlarum Follow Tags](https://discuss.flarum.org/d/20525-friendsofflarum-follow-tags) would not render the WordPress post content and [Reflar Webhooks](https://discuss.flarum.org/d/17812-webhooks-by-reflar) would fail to send new discussion hooks.
This is fixed since version 1.5.0 of the Flarum extension.

## Installation

You must install both the WordPress plugin and Flarum extension.

### On WordPress

- Download the plugin via [this link](/download/wordpress/kilowhat-flarum-1.5.0.zip). Current version is 1.5.0
- Extract the content of the ZIP file and place the `kilowhat-flarum` folder under `wp-content/plugins`
- Open the WordPress admin panel and enable the plugin
- Go to the **Flarum admin panel** and follow the installation wizard

See below for WordPress settings.

### On Flarum

- Purchase the ["KILOWHAT WordPress Integration"](https://extiverse.com/extension/kilowhat/flarum-ext-wordpress) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-wordpress`
- Open the Flarum admin panel and enable the extension
- On the extension page, use the installation wizard tab to enter your WordPress credentials

See below for Flarum settings.

## Update

When an update to either the WordPress plugin or Flarum extension is available, the Changelog will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/22229).

### Updating the WordPress plugin

When an update is available, the link to the new ZIP file will be provided in the changelog.

### Updating the Flarum extension

When an update is available, you can use the following commands to update:

    composer require kilowhat/flarum-ext-wordpress
    php flarum migrate
    php flarum cache:clear

## Troubleshooting

### The installation wizard is stuck

If you constantly receive "Flarum is already connected with WordPress" or "We could not authenticate with the given credentials".

Double-check the URL, username and password that you typed in the wizard.

If you previously ran the wizard and that an error happened, it's possible the setup is blocked in a half-finished configuration.

To run the wizard again:

- Delete the "WordPress URL" setting in Flarum
- Delete the "Flarum API key" setting in WordPress

And refresh the Flarum admin dashboard.
The wizard should be available again.

### Health check

When you open the WordPress tab in the Flarum admin dashboard, the health check will run.

The checks include:

- Common Flarum URL misconfiguration
- Access to the WordPress API
- Disparities between the values entered in WordPress vs Flarum
- Verify all required Flarum extensions are enabled
- Check that the tags and users referenced in the settings exist

Green: no issues detected.

Red: a list of the issues will be explained.

### There is another error

Check the `<flarum>/storage/logs` folder.
It will contain a log file named with the current date.

All errors triggered by the Flarum extension should be logged in that file.
The log file also contains the history of all requests that WordPress made to Flarum.

## Integrity considerations

Once the extension is enabled, you should not edit any WordPress post or Flarum discussion directly in the database.
Doing so may break the link between some posts or users and break future synchronisation.

If you ever disable the Flarum extension, there is a risk of breaking links as well.
Re-enabling the extension should work, but some errors could be thrown if WordPress posts or users have been deleted in the meantime.

If you reset the WordPress site or switch it with another, you should completely uninstall the extension from Flarum, including rolling back migrations, then install it again.
Otherwise, some WordPress IDs might still be in the database and cause errors and potential security issues.

## Support

If you are having issues with the extension, check the following:

- If the extension doesn't install, check you have correctly configured Extiverse's private repository.
- If an error happens during activation or usage of the extension, check the logs in `<flarum>/storage/logs`.

If you are still having issues, please copy the output of the logs above, as well as the output of `php flarum info` and send an email to <support@kilowhat.net>.

Support is provided on a "best effort" basis.
Most replies should usually be within 24h.

I only provide help solving specific issues with the extension.
I won't install the extension for you.

## Settings in WordPress plugin

The settings can be found under Settings > General.

### Flarum URL

**Required**

*This setting is auto-filled when you configure the extension via the wizard in the Flarum admin dashboard.*

The URL to your Flarum site homepage, including the protocol, but without any ending slash.

The URL must be HTTPS.

Custom API endpoints are not supported.
The API is expected to be at `<url>/api`.

Valid examples:

    https://example.com
    https://example.com/flarum
    https://flarum.example.com
    
Invalid examples:

    https://example.com/
    https://example.com/index.php
    https://example.com/index
    https://example.com/admin
    http://example.com
    example.com

### Flarum API Key

**Required**

*This setting is auto-filled when you configure the extension via the wizard in the Flarum admin dashboard.*

In the Flarum extension settings, copy the **Flarum API Key** value and paste it here.

You cannot use another Flarum API key, it has to be the one shown in the Flarum extension settings because it's also used for url signing and reverse authentication by Flarum.

### Flarum User ID

**Required, default value: 1**

*This setting is auto-filled when you configure the extension via the wizard in the Flarum admin dashboard.*

The Flarum user that will be used to perform the API calls.

It must be an admin user.

The user will be used as the actor of all actions performed by WordPress, but is mostly visible in two locations only: they will be set as discussion authors, and will be shown as the ones renaming the discussion title if the name changes.

### Enable SSO integration

Enables the "single sign on" integration features.
The corresponding setting must be enabled in the Flarum extension as well.

Most settings regarding SSO integration are found in the Flarum extension.

### Cookie domain

**Required if WordPress domain is different from Flarum domain**

*This setting is auto-filled when you configure the extension via the wizard in the Flarum admin dashboard.*

The domain on which Flarum login cookies will be set and cleared.

If WordPress and Flarum are on the same domain, but just different subfolders, this setting is not required.
For example WordPress at `https://example.com` and Flarum at `https://example.com/forum`, leave this field empty.

If the subdomains are different, the higher-level domain must be used.
Example WordPress: `https://www.example.com`, Flarum `https://forum.example.com`. Cookie domain = `example.com`.

If WordPress and Flarum are not on subdomains of the same domain, the SSO integration cannot work.

### Enable comments integration

Enables the "comments" integration features.
The corresponding setting must be enabled in the Flarum extension as well.

All settings regarding comments integration are found in the Flarum extension.

### Comments post types

*Since version 1.1 of the WordPress plugin*

**Default value: `post,page`**

Lets you customize which post types will use the comments integration when enabling comments.
You can specify multiple post types separated by a comma.
Post types not included here will default to normal WordPress comments if comments are enabled on them.

Setting this value will not change whether comments are opened or closed by default.
Default comments status is still controlled by the corresponding native WordPress settings.

### Override Flarum discussion tags

*Since version 1.5 of the WordPress plugin. Requires version 1.8+ of the Flarum extension*

**Default value:** *not set*

This setting is optional.
The value provided here will override the **Tag for new comment threads** value set in the Flarum extension.
In a WordPress multi-site context, this allows specifying different tags depending on the currently active WordPress site.
If you are not using WordPress multi-site, I recommend leaving this setting empty and only using the settings on the Flarum side.

The text input accepts a list of Flarum tag slugs or IDs separated by a comma.
If an invalid slug or ID is provided, it will be ignored and a warning will be written to the Flarum log file.

After the initial comment discussion creation in Flarum, the tags are not updated.
I am not sure whether WordPress or any of its plugins allow moving a post from one site to another.
If that happens, the behaviour might be unexpected.
But most likely nothing will happen, the discussion will stay the same in Flarum and continue to be synced with the same WordPress post ID on the next operation.

### Shortcode for custom themes

*Since version 1.3 of the WordPress plugin*

If for some reason your theme builder is not replacing normal comments with the Flarum iframe, there is a `[flarum_comments]` shortcode you can use.

On a Newspaper theme, replace `[tdb_single_comments ...]` with `[flarum_comments]`.

The presence of the shortcode alone is not sufficient to enable comments.
Make sure the post type is whitelisted in the settings and that comments are enabled on the post.

## Settings in Flarum extension

### Flarum API Key

**Auto-generated**

This is a secret Flarum master API key generated for you when the extension is enabled for the first time.

If the key has been compromised, you have to delete it from Flarum. You can use the following MySQL commands in your database:

    DELETE FROM api_keys WHERE key = '<the key from the settings>';
    DELETE FROM settings WHERE key = 'kilowhat-wordpress.api_key';

Then refresh the admin panel page to automatically generate a new API key. Don't forget to update it on the WordPress side.

### WordPress URL

**Required**

*This setting is auto-filled when you configure the extension via the wizard.*

The URL to your WordPress site, including the protocol, but without any ending slash or `index.php`.

The URL must be HTTPS.

Valid examples:

    https://example.com
    https://example.com/wordpress
    https://wordpress.example.com
    
Invalid examples:

    https://example.com/
    https://example.com/index.php
    http://example.com
    example.com

### WordPress admin username

**Required with the comments integration**

*This setting is auto-filled when you configure the extension via the wizard.*

Must be a valid WordPress username that is allowed to enable and disable comments on any post.

### Enable SSO integration

Enables the "single sign on" integration features.
The corresponding setting must be enabled in the WordPress plugin as well.

Users created through WordPress SSO will have a special flag in the database preventing them from:

- Logging in with normal username/password in Flarum
- Resetting password
- Changing email
- Being edited by admins. Admins should edit the user email/password in WordPress.

See login/logout section below for details on how the global login works.

### Cookie Domain

**Required if WordPress domain is different from Flarum domain**

*This setting is auto-filled when you configure the extension via the wizard.*

The domain entered here will be used to clear Flarum login cookies set by WordPress.
The value must match with the corresponding setting in the WordPress plugin.

See the documentation for the WordPress plugin for how to choose the value.

### WordPress login path

*Since version 1.1*

**Optional**

If the WordPress login endpoint was renamed, you can enter the new path relative to the WordPress url here.
Do not include the leading `/`.

For example if your WordPress login is now at `https://example.com/secretlogin`, use `secretlogin`.

Leaving this setting empty will use `wp-login.php`.

Since version 1.7.2, the path can include a query string.
The extension will replace existing query string parameters if necessary, in particular `redirect_to`.

### Username for new users

The logic used to generate Flarum usernames.

**Username from WordPress**: Will use the WordPress username as Flarum username.
The value will be truncated to 27 characters to fit Flarum length rules.
If the username is already taken in Flarum, a 3-numbers suffix will be added to make it unique.

**First name from WordPress**: Will attempt to use the "first name" attribute from WordPress.
If no first name exists, it will automatically fallback to username.

Important: for a first name to be used, a WordPress plugin must have set it up before the user login for the first time in WordPress.
For example Woocommerce adds the field to the registration form.
Changing the first name in the WordPress profile will have no effect as the Flarum account is already created at this point.

**Random username**: A combination of adjective + animal name + random number will be used.

It is not possible to customize the list of words at this time.
The list of words can be consulted in the `vendor/kilowhat/flarum-ext-wordpress/resources/usernames` folder.
Do not edit these files, the changes will be lost.

### Make users choose their username on first visit

When this option is enabled, a first username is generated according to the rules above, but users will be offered the opportunity to customize it on their first visit on the forum.

### Introduction message

A welcome message that will be shown the first time the user visits the forum.
They won't be able to interact with the forum until they accept the message.

Important: enabling "choose username" or "introduction message" will cause a modal to appear when opening the forum.
This can cause issues with other extensions that also open modals with the page load, like FoF Terms and Flagrow Direct Links.

### Only allow WordPress login

Will replace Flarum login links with the WordPress login modal.
It also opens the WordPress login modal when attempting to write a new post as guest.

This completely disables normal login, including from the API.
If you have users not yet linked to WordPress, they must register on WordPress to regain access to their Flarum accounts.

When this feature is enabled, the Flarum core permission "Sign Up" is set to Closed.
You must keep "Sign Up" to closed, otherwise it is still possible to register through the API.

When this feature is enabled, it's impossible to use the password reset feature.
If you lock yourself out (for example WordPress no longer works), you can restore normal login by editing the database:

    DELETE FROM settings WHERE key = 'kilowhat-wordpress.wordpress_login_only';

### Action when a user is deleted in WordPress

**Ignore**: Do nothing in Flarum.
Keep the user, but unlink it from WordPress.
They will be able to request a password reset if normal login is allowed.

**Delete**: Delete user in Flarum.
The user posts and discussions will be kept.
A new user will be able to register with the same email and/or username.

**Suspend**: Suspend the user indefinitely in Flarum.
Requires the Suspend extension to be enabled.
The user will be unlinked from WordPress.
The user will be able to request a password reset if normal login is allowed, but will not be able to interact with Flarum anymore as long as they stay suspended.

### Enable comments integration

Enables the "comments" integration features.
The corresponding setting must be enabled in the WordPress plugin as well.

When this feature is enabled, new discussions created by WordPress will have a special flag in the database.
Posting or locking the discussion will trigger updates on the WordPress post.

Lock status will be kept in sync with the "Allow comments" setting of the WordPress post.
Updating from either WordPress or Flarum will update the other side.

### Whitelist of HTML tags to keep in the excerpt

*Since version 1.1*

**Optional**

This feature will load the WordPress Post HTML inside Symfony's DOM crawler.
If the HTML is invalid, this filter will be skipped and a message will be written to the log file.

HTML tags to keep in the excerpt.
Multiple tags can be specified separated by commas.

For example to keep only paragraphs and lists but exclude images, you can use `p,ul`.

Setting an empty value (default) will skip this filter.

### Length of the content excerpt (in number of HTML nodes)

*Since version 1.1*

**Optional**

This feature will load the WordPress Post HTML inside Symfony's DOM crawler.
If the HTML is invalid, this filter will be skipped and a message will be written to the log file.

The maximum number of HTML top-level nodes to keep in the excerpt.
Under most circumstances, this can be considered as the number of paragraphs to keep.

If you enable the HTML tags filter (see above), nodes are counted after the whitelist filter has been applied.

Setting 0 or an empty value (default) will skip this filter.

### Length of the content excerpt (in characters)

**Optional**

This feature does not require the WordPress Post to contain valid HTML.

Controls the length of WordPress post summaries in Flarum.

The number of characters to keep at minimum.
The characters are counted in the HTML source of the post.
Flarum will cut the text at the next closing paragraph after the given length is reached.

*Before version 1.1*, the text was cut at the last paragraph before the length was reached.

If no match is found, the whole post will be included.

This feature can be enabled together with the HTML whitelist.
It can also be enabled together with the node count but it probably doesn't make much sense to do so.

Setting 0 or an empty value (default) will skip this filter.

### Show WordPress post thumbnail above excerpt

*Since version 1.8, requires version 1.5+ of the WordPress plugin*

Shows the WordPress post thumbnail above the post excerpt.
The original image URL is hot-linked from WordPress and inserted in its own `<img>` tag.

Discussions created before version 1.8(Flarum extension)/1.5(WordPress plugin) did not save the post thumbnail URL.
If you edit the post in WordPress a new version of the post including thumbnail will be synced.

### Show WordPress post thumbnail in Flarum discussion list

*Since version 1.8, requires version 1.5+ of the WordPress plugin*

Same as the setting above but the WordPress post thumbnail will be added when displaying the comment thread in the Flarum discussion list (homepage, tag page, etc.).

The default styling is very simple.
You can add additional styling targeting the `.KilowhatWordpressDiscussionListItem-Thumbnail` image tag.

### Assign discussion author from SSO

*Since version 1.8, requires version 1.5+ of the WordPress plugin*

By default, the Flarum API user set in WordPress **Flarum User ID** setting will be used as the author of the comment discussion and its event posts.

When this setting is enabled, Flarum will attempt to use the Flarum profile of the WordPress post author as discussion author.
Matching is performed using the WordPress user ID which is set when the user connects to Flarum using the SSO feature.

If the WordPress user has never logged into Flarum, its profile won't be found and the default user set as **Flarum User ID** will be used.

Discussions created before version 1.8(Flarum extension)/1.5(WordPress plugin) will not be retroactively updated.
You may use my free [Author Change extension](https://discuss.flarum.org/d/21731) to manually fix older discussions.
Don't forget to update both the discussion and first post authors.

When this setting is enabled, the first post author will be displayed similarly to regular Flarum comments, with the avatar in the left margin on desktop and a mouse-activated user card.
If you customized the CSS of the WordPress summary, you can adjust the CSS variables `--wordpress-post-article-border-width` (originally `5px`) and `--wordpress-post-article-padding` (originally `20px`) on `.KilowhatWordpressSummaryPost` to automatically adjust the positioning of the avatar.

### Tag for new comment threads

**Optional**

Flarum tags to set on new discussions created by WordPress.

You can select primary or secondary tags via the dropdown.
The number of tags selected doesn't need to match the Flarum tags for minimum and maximum settings.

If you want to add multiple top-level primary tags or want to use a combination of primary and secondary tags, you can manually enter a list of tag IDs to use.
Select "Custom values" in the dropdown and enter a comma-separated list of tag IDs (not slugs) in the text field that appears.

Requires the Tags extension to be enabled.

If you want the tag to show a WordPress icon, you can use `fab fa-wordpress` as the tag icon.

### Set the summary post as the last post of new discussions

By default, Flarum doesn't count "event" posts as replies, which means a discussion with just the WordPress summary counts as a discussion with no comments.
Such a discussion is always at the bottom of the discussion list until a first person replies.

If you would like the discussion to rise to the top of the discussion list in Flarum even if no one comments immediately, you can enable this feature.

When enabled, the discussion will show as having one new unread post for users, with the date being the same as the discussion creation.

### Use WordPress post date as the discussion creation date

*Since version 1.3*

By default, Flarum discussions will use the current time as their creation date.

When enabled, the discussion creation date will be copied from WordPress post date.

For this option to work, you must set the WordPress post date before publishing the post.
It works with date in the past as well as in the future.

If the date is in the past, the new discussion will not appear at the top of Flarum discussion list until a first user replies, even if "Set the summary post as the last post of new discussions" is enabled.

Changing the WordPress post date on a post that already has a linked Flarum discussion will have no effect.

### Action when a WordPress post is hidden

This action triggers whenever a post is removed from public view in WordPress, by putting it in the Trash or setting it as Draft after having it published already.

Important: post previews are never deleted.
With Ignore or Lock options, users will still be able to read (part of) the post in Flarum.
Use Hide or Permanent delete to remove the content from the users view or manually delete the summary post.

**Ignore**: The Flarum discussion will stay in the exact same state as it was before the post disappeared from WordPress.
The lock status will continue to match the posts "allow comments" property.

**Lock discussion in Flarum**: Immediately lock the discussion in Flarum.

**Hide discussion in Flarum**: Soft-delete the discussion in Flarum.
Only users with the "hide discussions" permission will continue to see it, like other deleted discussions.

**Permanently delete discussion in Flarum**: Hard-delete the discussion from Flarum.
The discussion will be unlinked from the WordPress post.
If the WordPress post is published again, a new discussion will be created for it.

### Action when a WordPress post is deleted permanently

Same as above but for when a post has been permanently deleted from WordPress.

If the Flarum discussion is kept, it will be unlinked from WordPress and posting/locking will no longer send requests to WordPress.

### Permissions

A singe permission is currently visible on the Permissions page of Flarum:

*Since version 1.2*

**Third-party gambits**: see below for third-party integrations.
Keep it on Admin only unless you know what you're doing!

## Third-party integrations

*Since version 1.2*

You might want to integrate this extension with your own custom features.
For this reason we offer a few additional parameters that are not used by the extension itself but can be useful to you.

The way the extension is designed, all links between WordPress and Flarum are managed inside Flarum.
This means there's no way to get the Flarum user ID or username from inside WordPress.

Some warnings:

- The Flarum username can still be changed by the user later on if you enabled the "Make users choose their username on first visit" option and they have not yet activated their forum account. Avoid storing it in WordPress.
- The Flarum user ID might change if a user is deleted from Flarum manually, or if their email is manually changed from Flarum instead of WordPress. Avoid storing it in WordPress.
- I don't recommended calling the internal login endpoint for other purposes as the parameters are susceptible to change without warning, and it might also create unnecessary tokens that have a very long lifetime and are never invalidated.

In order to let you query the Flarum API from WordPress, these additional gambits were added to Flarum:

- `GET /api/users?filter[q]=wordpressid:1`: will let you retrieve a Flarum user via its WordPress user ID
- `GET /api/discussions?filter[q]=wordpressid:1`: will let you retrieve a Flarum discussion via its WordPress post ID

The gambits are added to the search feature of Flarum, so those endpoints will return a list of results.
If a resource is found, `data` will contain a single result.
An empty `data` object results indicates no results.
There are no 404 errors on that endpoint.

By default, only admins can use the gambits.
You can control who can use the gambits via the "Third-party gambits" permission on the Permissions page.

Additionally, the internal login endpoint also returns the Flarum user ID and username along with the token.
The return payload looks like this:

    # Request (request body not documented on purpose, see kilowhat-flarum-login.php file if needed)
    POST /api/kilowhat/wordpress/user/login/1
    # Response
    {"user_id":42,"username":"DemoUser","token":"TUaJ7o3N8VftAz4wLFghApT4YZF6H0fCaou1uhvM"}

## How global login/logout works

The extension uses multiple ways to perform login and logout with as few requests and cookies as possible.

If you login from WordPress, the following happens:

- Credentials are validated by WordPress and the WordPress session is open
- Flarum account is created via a server-side API call if it doesn't already exist
- Flarum remember cookie is set on the cookie domain
- A subsequent visit of the forum will open the Flarum session via the remember me feature

If you login from Flarum, the following happens:

- Flarum opens WordPress login page in a popup
- Credentials are validated by WordPress and the WordPress session is open
- Flarum account is created via a server-side API call if it doesn't already exist
- WordPress returns the "remember" token directly to Flarum without setting any cookie
- Flarum session opens via the token

If you logout from WordPress, the following happens:

- User is redirected to a Flarum url that clears session and remember cookies on both Flarum and cookie domain
- User is redirected back to WordPress for classic WordPress logout

If you logout from Flarum, the following happens:

- User is logged out of Flarum, cookies are cleared on both Flarum and cookie domain
- User is redirected to WordPress for classic WordPress logout

The logout process is based on redirects to signed urls that prevent any cross-site request forgery vulnerability.
