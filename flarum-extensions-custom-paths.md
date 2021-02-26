---
layout: page
title: Custom Paths
permalink: /flarum/extensions/custom-paths
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths)

- **Price**: 10 USD lifetime license
- **Bundled translations**: English
- **Flarum compatibility**: beta 15+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths)
- See on [Flarum Discuss](https://discuss.flarum.org/d/23872)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Compatibility](#compatibility)
- [Known issues](#known-issues)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Extension settings](#extension-settings)

## Introduction

Custom Paths is a Flarum extension that allows you to customize the URL to various user-facing pages.

When a path is customized, the original URL returns a 404 error.
You can optionally enable redirects from the old paths to the new paths.

<div class="picture-row">
<img src="/medias/extensions/custom-paths/settings.png" alt="Settings Modal" style="max-width: 300px;">
</div>

## Changelog

### Version 1.3.0 - February 27, 2021

- Add ability to customize v17development's Flarum Blog pages.
- Add ability to customize FriendsOfFlarum's Byobu pages.
- Add ability to customize ClarkWinkelmann's Group List page.
- Fix v17development's SEO inability to add SEO tags to customized pages.
- Fix issue when setting a customized page as homepage.

### Version 1.2.0 - January 18, 2021

- Add ability to customize Formulaire standalone form and submission URLs.

### Version 1.1.0 - December 27, 2020

- Flarum beta 15 compatibility.
- Add ability to customize FoF Gamification rankings page.
- Add ability to customize the user profile page filters (`/discussions`, `/mentions`).
- Add ability to re-use paths.

This version can only be installed on Flarum beta 15 and will automatically be installed when you migrate to Flarum beta 15 with Flarum's official instructions.

### Version 1.0.3 - November 3, 2020

- Flarum beta 14 compatibility.
- Fix `/u/<username>/mentions` not being affected by the `/u/` customization.

This version can only be installed on Flarum beta 14 and will automatically be installed when you migrate to Flarum beta 14 with Flarum's official instructions.

### Version 1.0.2 - May 22, 2020

- Fix issues with loading order.

### Version 1.0.1 - May 20, 2020

- Fix issues with original paths that include variables.

### Version 1.0.0 - May 20, 2020

Initial release.

## Compatibility

Custom Paths provides integration with the following extensions:

- Flarum's Tags
- Flarum's Subscriptions
- Flarum's Flags
- Flarum's Mentions (since 1.1.0)
- [KILOWHAT Formulaire](/flarum/extensions/formulaire) (since 1.2.0)
- [FriendsOfFlarum's User Directory](https://discuss.flarum.org/d/5682)
- [FriendsOfFlarum's Pages](https://discuss.flarum.org/d/18301)
- [FriendsOfFlarum's Gamification](https://discuss.flarum.org/d/20671) (since 1.1.0)
- [FriendsOfFlarum's Byobu](https://discuss.flarum.org/d/4762) (since 1.3.0)
- [Askvortsov's Categories](https://discuss.flarum.org/d/23184)
- [v17development's Flarum Blog](https://discuss.flarum.org/d/25392) (since 1.3.0)
- [ClarkWinkelmann's Group List](https://discuss.flarum.org/d/25386) (since 1.3.0)

The following extensions are incompatible:

- [FriendsOfFlarum's Sitemap](https://discuss.flarum.org/d/14941) (paths are hard-coded in the sitemap extension)

Most other Flarum extensions should work fine alongside Custom Paths, but no integration will be automatically provided.

You may request additional integrations on the Discuss page.

## Known issues

- The user profile filters (`/discussions`, `/mentions` suffix) are not affected by the "Redirect" setting. Typing the old URL will always redirect to the homepage. (This is because this is a frontend-only route)
- The eye icon in the FoF Pages admin panel won't open the correct URL if it was customized, but the customized path is correctly applied. (the original path is hard-coded in the admin panel)

Issues in previous versions that have been fixed as of 1.1.0:

- The URLs in emails won't be updated. You can use [FriendsOfFlarum's Pretty Mail](https://discuss.flarum.org/d/11178) with a custom HTML template to correct the URL.
- You can't re-use an existing path, like `/d/` or `/all` or `/settings` or others anytime, `/t/` or `/tags` when the Tags extension is enabled, or `/p/` when the Pages extension is enabled.
- The "Following" link in the side navigation doesn't have an "active" effect when the page is displayed if the path has been customized.
- The Flags page can't be loaded or redirected when typing the URL directly. This is a bug in Flarum, see [flarum/flags#23](https://github.com/flarum/flags/pull/23).

Issues that have been fixed as of 1.3.0:

- [v17development's SEO](https://discuss.flarum.org/d/18316) was not able to add SEO tags to pages with customized URLs.

## Installation

- Purchase the ["KILOWHAT Custom Paths"](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-custom-paths`
- Open the Flarum admin panel and enable the extension
- See below for the settings

## Update

When an update is available, the [Changelog](#changelog) will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/23872).

You can use the following commands to update:

    composer require kilowhat/flarum-ext-custom-paths
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

## Extension settings

All settings can be found in the extension page of the admin panel.

You don't need to install/enable all the compatible extensions.
Only the paths for your enabled extensions will be customizable.

### Paths

Each of the paths can be customized by entering an alternate path segment in the text field, then saving with the button at the bottom of the page.

**Be careful with path re-use**.
Since version 1.1.0, you can re-use tokens that were part of other URLs in new paths.
For example you can use `/t/` (originally for tags) for discussions, provided you set the tags path to something different.
The extension will not check for duplicated paths, but Flarum won't work correctly if you use the same path twice.

There is no data validation, but for optimal compatibility with browsers you should only use the following:

- Use alphanumerical values and dashes/underscores (A-Za-z0-9_-).
- There is no maximum length, but it's probably a good idea to remain below 50 characters.
- Minimum length is 1 character. It's not possible to use an empty path segment.

If you leave a field empty, the default path will be kept.

### Redirects

By default, the original URL of modified paths will return a 404 page not found error.
By enabling "Redirect default Flarum paths to new paths", a redirect to the new path will be returned instead.

- With debug mode enabled, a 302 temporary redirect is used.
- With debug mode disabled, a 301 permanent redirect is used.
