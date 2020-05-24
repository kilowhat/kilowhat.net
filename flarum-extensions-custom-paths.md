---
layout: page
title: Custom Paths
permalink: /flarum/extensions/custom-paths
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-custom-paths)

- **Price**: 10 USD lifetime license
- **Bundled translations**: English
- **Flarum compatibility**: beta 13+
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
- [FriendsOfFlarum's User Directory](https://discuss.flarum.org/d/5682)
- [FriendsOfFlarum's Pages](https://discuss.flarum.org/d/18301)
- [Askvortsov's Categories](https://discuss.flarum.org/d/23184)

The following extensions are incompatible:

- [JasperVriends's SEO](https://discuss.flarum.org/d/18316) (the extension won't be able to add SEO meta tags on pages that you have customized through Custom Paths). I will try to find some workaround.
- [FriendsOfFlarum's Sitemap](https://discuss.flarum.org/d/14941) (paths are hard-coded in the sitemap extension)

Most other Flarum extensions should work fine alongside Custom Paths, but no integration will be automatically provided.

You may request additional integrations on the Discuss page.

## Known issues

- The URLs in emails won't be updated. You can use [FriendsOfFlarum's Pretty Mail](https://discuss.flarum.org/d/11178) with a custom HTML template to correct the URL.
- You can't re-use an existing path, like `/d/` or `/all` or `/settings` or others anytime, `/t/` or `/tags` when the Tags extension is enabled, or `/p/` when the Pages extension is enabled.
- The "Following" link in the side navigation doesn't have an "active" effect when the page is displayed if the path has been customized.
- The Flags page can't be loaded or redirected when typing the URL directly. This is a bug in Flarum, see [flarum/flags#23](https://github.com/flarum/flags/pull/23).
- The eye icon in the Pages admin panel won't open the correct URL if it was customized, but the customized path is correctly applied.

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

All settings can be found in the settings modal available via the Extensions page of the admin panel.

You don't need to install/enable all the compatible extensions.
Only the paths for your enabled extensions will be customizable.

### Paths

Each of the paths can be customized by entering an alternate path segment in the text field, then saving with the button at the bottom of the modal.

**Do not reuse a path**.
You cannot re-assign a path that was originally for another route, like `/d/`, `/t/` (if Tags are enabled) or `/p/` (if Pages are enabled).
You cannot use the same path two times.
Doing so will lock you out of the forum and you will need to edit the settings in the database to regain access.

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
