---
layout: page
title: Flarum Wordpress Integration
permalink: /flarum/extensions/wordpress
---

- **Price:** 5 USD/month + VAT depending on your country
- **Translations**: English only
- **Flarum compatibility**: beta 10+
- See on [flagrow.io](https://flagrow.io/extensions/kilowhat/flarum-ext-wordpress)
- See on [Flarum Discuss](https://discuss.flarum.org/d/22229-premium-wordpress-integration)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Demo](#demo)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Integrity considerations](#integrity-considerations)
- [Support](#support)
- [Settings in Wordpress plugin](#settings-in-wordpress-plugin)
- [Settings in Flarum extension](#settings-in-flarum-extension)
- [Third-party integrations](#third-party-integrations)
- [How global login/logout works](#how-global-loginlogout-works)

## Introduction

The Flarum Wordpress integration is a premium extension developed by Clark Winkelmann.

It offers two main features:

### SSO

<div class="picture-row">
<img src="/medias/extensions/wordpress/login.png" alt="SSO Login modal">
<img src="/medias/extensions/wordpress/welcome.png" alt="Welcome modal">
</div>

Adds Wordpress login to Flarum, along with a global single sign-on and sign-out.

User can connect through Wordpress or Flarum and will automatically be connected on both platforms.

Logging out will also clear both sessions before redirecting to the Wordpress logout page.

Email changes and password resets happen via Wordpress.

Wordpress SSO can be used alongside normal Flarum login, or replace it completely.

### Comments

<div class="picture-row">
<img src="/medias/extensions/wordpress/embed.png" alt="Embed on Wordpress side">
<img src="/medias/extensions/wordpress/summary.png" alt="Post summary on Flarum side">
</div>

Replaces Wordpress comments with an iframe containing a Flarum discussion.

Discussions are automatically created by Flarum along with a summary of the Wordpress post.

Discussions can be automatically locked and hidden when the comments status is changed in Wordpress.

Guest posting is not possible with this integration enabled.

## Changelog

### Version 1.2 - January 7, 2020

- Added search gambits for third-party integrations

You can update the Flarum extension via Bazaar or Composer.
The Wordpress plugin does not need to be updated.

### Version 1.1 - December 17, 2019

- Added compatibility for custom Wordpress login path
- Added more options for excerpt generation

You can update the Flarum extension via Bazaar or Composer.
The Wordpress plugin does not need to be updated.

### Version 1.0 - December 10, 2019

Initial release.

## Demo

A demo/test website is available at <https://wordpress-flarum-demo.http418.ch/>.

The website will be reset manually from time to time.

Please get in touch if you would like admin access.

## Requirements

- Wordpress version must be 5.0 or higher (lower might work, but not tested)
- Flarum version must be beta 10 or higher
- You must have SSH and Composer access on the Flarum hosting
- Flarum server must be able to use Bazaar, which often requires 1GB of RAM or swap
- Wordpress and Flarum must be hosted on the same domain, or subdomains of the same domain (cookie limitations)
- Wordpress and Flarum must be accessible via HTTPS and HTTP urls must be redirected to HTTPS
- Wordpress and Flarum may be hosted on the same server or a different server
- Wordpress and Flarum may use the same database (with different prefixes) or a different database

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Most other Wordpress plugins and Flarum extensions should be compatible.
The extension makes many changes to Wordpress and Flarum logout systems that could cause issues with other extensions.

Wordpress plugins/features verified compatible:

- [Shield Security](https://en-gb.wordpress.org/plugins/wp-simple-firewall/): Hide login, Login Captcha

Wordpress plugins/feature verified incompatible:

- [Shield Security](https://en-gb.wordpress.org/plugins/wp-simple-firewall/): 2FA (Flarum login bypasses 2FA)

## Installation

You must install both the Wordpress plugin and Flarum extension.

### On Wordpress

- Download the plugin via [this link](/download/wordpress/kilowhat-flarum-1.0.0.zip). Current version is 1.0.0
- Extract the content of the ZIP file and place the `kilowhat-flarum` folder under `wp-content/plugins`
- Open the Wordpress admin panel and enable the plugin
- See below for Wordpress settings

### On Flarum

- Install and enable the [Bazaar extension](https://discuss.flarum.org/d/5151-bazaar-the-extension-marketplace)
- Connect Bazaar with your flagrow.io account
- Purchase the "KILOWHAT Wordpress Integration" extension via Bazaar or flagrow.io
- Install and enable the extension via Bazaar
- See below for Flarum settings

## Integrity considerations

Once the extension is enabled, you should not edit any Wordpress post or Flarum discussion directly in the database.
Doing so may break the link between some posts or users and break future synchronisation.

If you ever disable the Flarum extension, there is a risk of breaking links as well.
Re-enabling the extension should work, but some errors could be thrown if Wordpress posts or users have been deleted in the meantime.

If you reset the Wordpress site or switch it with another, you should completely uninstall the extension from Flarum, including rolling back migrations, then install it again.
Otherwise some Wordpress IDs might still be in the database and cause errors and potential security issues.

## Support

If you are having issues with the extension, check the following:

- If the extension doesn't install, check your system meets Bazaar requirement and check logs under the Bazaar history tab (spinning arrow icon)
- If an error happens during activation or usage of the extension, check the logs in `<flarum>/storage/logs`

If you are still having issues, please copy the output of the logs above, as well as the output of `php flarum info` and send an email to <support@kilowhat.net>.

Support is provided on a "best effort" basis.
Most replies should usually be within 24h.

I only provide help solving specific issues with the extension.
I won't install the extension for you.

## Settings in Wordpress plugin

The settings can be found under Settings > General.

### Flarum URL

**Required**

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

In the Flarum extension settings, copy the **Flarum API Key** value and paste it here.

You cannot use another Flarum API key, it has to be the one shown in the Flarum extension settings because it's also used for url signing and reverse authentication by Flarum.

### Flarum User ID

**Required, default value: 1**

The Flarum user that will be used to perform the API calls.

It must be an admin user.

The user will be used as the actor of all actions performed by Wordpress, but is mostly visible in two locations only: they will be set as discussion authors, and will be shown as the ones renaming the discussion title if the name changes.

### Enable SSO integration

Enables the "single sign on" integration features.
The corresponding setting must be enabled in the Flarum extension as well.

Most settings regarding SSO integration are found in the Flarum extension.

### Cookie domain

**Required if Wordpress domain is different from Flarum domain**

The domain on which Flarum login cookies will be set and cleared.

If Wordpress and Flarum are on the same domain, but just different subfolders, this setting is not required.
For example Wordpress at `https://example.com` and Flarum at `https://example.com/forum`, leave this field empty.

If the subdomains are different, the higher-level domain must be used.
Example Wordpress: `https://www.example.com`, Flarum `https://forum.example.com`. Cookie domain = `example.com`.

If Wordpress and Flarum are not on subdomains of the same domain, the SSO integration cannot work.

### Enable comments integration

Enables the "comments" integration features.
The corresponding setting must be enabled in the Flarum extension as well.

All settings regarding comments integration are found in the Flarum extension.

## Settings in Flarum extension

### Flarum API Key

**Auto-generated**

This is a secret Flarum master API key generated for you when the extension is enabled for the first time.

If the key has been compromised, you have to delete it from Flarum. You can use the following MySQL commands in your database:

    DELETE FROM api_keys WHERE key = '<the key from the settings>';
    DELETE FROM settings WHERE key = 'kilowhat-wordpress.api_key';

Then refresh the admin panel page to automatically generate a new API key. Don't forget to update it on the Wordpress side.

### Wordpress URL

**Required**

The URL to your Wordpress site, including the protocol, but without any ending slash or `index.php`.

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

### Wordpress admin username

**Required with the comments integration**

Must be a valid Wordpress username that is allowed to enable and disable comments on any post.

### Enable SSO integration

Enables the "single sign on" integration features.
The corresponding setting must be enabled in the Wordpress plugin as well.

Users created through Wordpress SSO will have a special flag in the database preventing them from:

- Logging in with normal username/password in Flarum
- Resetting password
- Changing email
- Being edited by admins. Admins should edit the user email/password in Wordpress.

See login/logout section below for details on how the global login works.

### Cookie Domain

**Required if Wordpress domain is different from Flarum domain**

The domain entered here will be used to clear Flarum login cookies set by Wordpress.
The value must match with the corresponding setting in the Wordpress plugin.

See the documentation for the Wordpress plugin for how to choose the value.

### Wordpress login path

*Since version 1.1*

**Optional**

If the Wordpress login endpoint was renamed, you can enter the new path relative to the Wordpress url here.
Do not include the leading `/`.

For example if your Wordpress login is now at `https://example.com/secretlogin`, use `secretlogin`.

Leaving this setting empty will use `wp-login.php`.

### Username for new users

The logic used to generate Flarum usernames.

**Username from Wordpress**: Will use the Wordpress username as Flarum username.
The value will be truncated to 27 characters to fit Flarum length rules.
If the username is already taken in Flarum, a 3-numbers suffix will be added to make it unique.

**First name from Wordpress**: Will attempt to use the "first name" attribute from Wordpress.
If no first name exists, it will automatically fallback to username.

Important: for a first name to be used, a Wordpress plugin must have set it up before the user login for the first time in Wordpress.
For example Woocommerce adds the field to the registration form.
Changing the first name in the Wordpress profile will have no effect as the Flarum account is already created at this point.

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

### Only allow Wordpress login

Will replace Flarum login links with the Wordpress login modal.
It also opens the Wordpress login modal when attempting to write a new post as guest.

This completely disables normal login, including from the API.
If you have users not yet linked to Wordpress, they must register on Wordpress to regain access to their Flarum accounts.

When this feature is enabled, the Flarum core permission "Sign Up" is set to Closed.
You must keep "Sign Up" to closed, otherwise it is still possible to register through the API.

When this feature is enabled, it's impossible to use the password reset feature.
If you lock yourself out (for example Wordpress no longer works), you can restore normal login by editing the database:

    DELETE FROM settings WHERE key = 'kilowhat-wordpress.wordpress_login_only';

### Action when a user is deleted in Wordpress

**Ignore**: Do nothing in Flarum.
Keep the user, but unlink it from Wordpress.
They will be able to request a password reset if normal login is allowed.

**Delete**: Delete user in Flarum.
The user posts and discussions will be kept.
A new user will be able to register with the same email and/or username.

**Suspend**: Suspend the user indefinitely in Flarum.
Requires the Suspend extension to be enabled.
The user will be unlinked from Wordpress.
The user will be able to request a password reset if normal login is allowed, but will not be able to interact with Flarum anymore as long as they stay suspended.

### Enable comments integration

Enables the "comments" integration features.
The corresponding setting must be enabled in the Wordpress plugin as well.

When this feature is enabled, new discussions created by Wordpress will have a special flag in the database.
Posting or locking the discussion will trigger updates on the Wordpress post.

Lock status will be kept in sync with the "Allow comments" setting of the Wordpress post.
Updating from either Wordpress or Flarum will update the other side.

### Whitelist of HTML tags to keep in the excerpt

*Since version 1.1*

**Optional**

This feature will load the Wordpress Post HTML inside Symfony's DOM crawler.
If the HTML is invalid, this filter will be skipped and a message will be written to the log file.

HTML tags to keep in the excerpt.
Multiple tags can be specified separated by commas.

For example to keep only paragraphs and lists but exclude images, you can use `p,ul`.

Setting an empty value (default) will skip this filter.

### Length of the content excerpt (in number of HTML nodes)

*Since version 1.1*

**Optional**

This feature will load the Wordpress Post HTML inside Symfony's DOM crawler.
If the HTML is invalid, this filter will be skipped and a message will be written to the log file.

The maximum number of HTML top-level nodes to keep in the excerpt.
Under must circumstances, this can be considered as the number of paragraphs to keep.

If you enable the HTML tags filter (see above), nodes are counted after the whitelist filter has been applied.

Setting 0 or an empty value (default) will skip this filter.

### Length of the content excerpt (in characters)

**Optional**

This feature does not require the Wordpress Post to contain valid HTML.

Controls the length of Wordpress post summaries in Flarum.

The number of characters to keep at minimum.
The characters are counted in the HTML source of the post.
Flarum will cut the text at the next closing paragraph after the given length is reached.

*Before version 1.1*, the text was cut at the last paragraph before the length was reached.

If no match is found, the whole post will be included.

This feature can be enabled together with the HTML whitelist.
It can also be enabled together with the node count but it probably doesn't make much sense to do so.

Setting 0 or an empty value (default) will skip this filter.

### Tag IDs for new comment threads

**Optional**

Flarum tags to set on new discussions created by Wordpress.
Multiple tag IDs must be separated by commas.

You can find tag IDs by looking inside the database table `tags`.

Requires the Tags extension to be enabled.

If you want the tag to show a Wordpress icon, you can use `fab fa-wordpress` as the tag icon.

### Set the summary post as the last post of new discussions

By default Flarum doesn't count "event" posts as replies, which means a discussion with just the Wordpress summary counts as a discussion with no comments.
Such a discussion is always at the bottom of the discussion list until a first person replies.

If you would like the discussion to rise to the top of the discussion list in Flarum even if no one comments immediately, you can enable this feature.

When enabled, the discussion will show as having one new unread post for users, with the date being the same as the discussion creation.

### Action when a Wordpress post is hidden

This action triggers whenever a post is removed from public view in Wordpress, by putting it in the Trash or setting it as Draft after having it published already.

Important: post previews are never deleted.
With Ignore or Lock options, users will still be able to read (part of) the post in Flarum.
Use Hide or Permanent delete to remove the content from the users view or manually delete the summary post.

**Ignore**: The Flarum discussion will stay in the exact same state as it was before the post disappeared from Wordpress.
The lock status will continue to match the posts "allow comments" property.

**Lock discussion in Flarum**: Immediately lock the discussion in Flarum.

**Hide discussion in Flarum**: Soft-delete the discussion in Flarum.
Only users with the "hide discussions" permission will continue to see it, like other deleted discussions.

**Permanently delete discussion in Flarum**: Hard-delete the discussion from Flarum.
The discussion will be unlinked from the Wordpress post.
If the Wordpress post is published again, a new discussion will be created for it.

### Action when a Wordpress post is deleted permanently

Same as above but for when a post has been permanently deleted from Wordpress.

If the Flarum discussion is kept, it will be unlinked from Wordpress and posting/locking will no longer send requests to Wordpress.

### Permissions

A singe permission is currently visible on the Permissions page of Flarum:

*Since version 1.2*

**Third-party gambits**: see below for third-party integrations.
Keep it on Admin only unless you know what you're doing!

## Third-party integrations

*Since version 1.2*

You might want to integrate this extension with your own custom features.
For this reason we offer a few additional parameters that are not used by the extension itself but can be useful to you.

The way the extension is designed, all links between Wordpress and Flarum are managed inside Flarum.
This means there's no way to get the Flarum user ID or username from inside Wordpress.

Some warnings:

- The Flarum username can still be changed by the user later on if you enabled the "Make users choose their username on first visit" option and they have not yet activated their forum account. Avoid storing it in Wordpress.
- The Flarum user ID might change if a user is deleted from Flarum manually, or if their email is manually changed from Flarum instead of Wordpress. Avoid storing it in Wordpress.
- I don't recommended calling the internal login endpoint for other purposes as the parameters are susceptible to change without warning, and it might also create unnecessary tokens that have a very long lifetime and are never invalidated.

In order to let you query the Flarum API from Wordpress, these additional gambits were added to Flarum:

- `GET /api/users?filter[q]=wordpressid:1`: will let you retrieve a Flarum user via its Wordpress user ID
- `GET /api/discussions?filter[q]=wordpressid:1`: will let you retrieve a Flarum discussion via its Wordpress post ID

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

The extensions uses multiple ways to perform login and logout with as few requests and cookies as possible.

If you login from Wordpress, the following happens:

- Credentials are validated by Wordpress and the Wordpress session is open
- Flarum account is created via a server-side API call if it doesn't already exist
- Flarum remember cookie is set on the cookie domain
- A subsequent visit of the forum will open the Flarum session via the remember me feature

If you login from Flarum, the following happens:

- Flarum opens Wordpress login page in a popup
- Credentials are validated by Wordpress and the Wordpress session is open
- Flarum account is created via a server-side API call if it doesn't already exist
- Wordpress returns the remember token directly to Flarum without setting any cookie
- Flarum session opens via the token

If you logout from Wordpress, the following happens:

- User is redirected to a Flarum url that clears session and remember cookies on both Flarum and cookie domain
- User is redirected back to Wordpress for classic Wordpress logout

If you logout from Flarum, the following happens:

- User is logged out of Flarum, cookies are cleared on both Flarum and cookie domain
- User is redirected to Wordpress for classic Wordpress logout

The logout process is based on redirects to signed urls that prevent any cross-site request forgery vulnerability.
