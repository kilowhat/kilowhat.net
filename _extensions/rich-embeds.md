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
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Features](#features)
- [Extension settings](#extension-settings)

## Introduction

Rich Embeds is a Flarum extension that adds previews to links posted in discussions.
The previews are generated from OpenGraph data or an optional fallback method.

The data crawling is performed by the Flarum server without any external service and is cached for fast retrieval and minimal impact on page load times.

Images and favicons can optionally be proxied through the server to protect the visitor's privacy.

A whitelist or blacklist of websites can be configured to control which websites are previewed and prevent abuse of the proxy script.

<div class="picture-row">
<img src="/medias/extensions/rich-embeds/post.png" alt="Post with 2 different styles of embed" style="width: 500px;">
</div>

## Changelog

### Version 1.0.2 - April 10, 2022

- **Fixed** image proxy toggle not being applied.

### Version 1.0.1 - April 4, 2022

Initial release.

## Compatibility

Rich Embeds overrides the TextFormatter `URL` rendering template and as such may conflict with other extensions.

This page will be kept up to date with any known incompatibility that can't be worked around.

## Installation

- Purchase the ["KILOWHAT Rich Embeds"](https://extiverse.com/extension/kilowhat/flarum-ext-rich-embeds) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-rich-embeds`
- Open the Flarum admin panel and enable the extension
- See below for the settings

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

### Permissions

**Use embeds in own post**: controls which users can use embeds in their posts.
When a post is edited, it's the author of the post that is evaluated.
If the author of a post was deleted, editing the post will cause all embeds to be removed.

**Disable embeds on own post**: controls which users can remove embeds on posts they have authored.
This option appears after the post has been successfully created.

**Disable embeds on any post**: moderation equivalent of the *Disable embeds on own post* permission.

**Refresh embeds on any post**: gives access to the button to refresh an existing embed.
