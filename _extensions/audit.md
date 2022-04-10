---
layout: default
title: Audit Log
permalink: /flarum/extensions/audit
nav_order: 50
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-audit-pro/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-audit-pro){: .extiverse-badge}

- **Price**: 30 USD lifetime license
- **Bundled translations**: English
- **Flarum compatibility**: 1.2+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-audit-pro)
- See on [Flarum Discuss](https://discuss.flarum.org/d/24206)

Table of content:

- [Introduction](#introduction)
- [Free vs Pro](#free-vs-pro)
- [Changelog](#changelog)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Extension settings](#extension-settings)
- [Logged actions](#logged-actions)

## Introduction

Audit Log is a premium extension that adds an extensive action logging feature to Flarum.

Administrators can browse all logs from the admin panel.
Shortcuts are provided to quickly check a discussion or profile audit log from the forum interface.

The logs are read-only, preventing any tempering.

<div class="picture-row">
<img src="/medias/extensions/audit/log-browser.png" alt="Log browser in the admin panel">
</div>

## Free vs Pro

A [free version](https://discuss.flarum.org/d/24432) is available with limited features.

To get access to all feature and to support the ongoing development of the extension, consider upgrading to Pro!

|--------------------------------|------------------------------|-----|
| Feature                        | Free                         | Pro |
|--------------------------------|------------------------------|-----|
| **Logged events**              |                              | |
| Flarum core user events        | <span class="yes">Yes</span> | <span class="yes">Yes</span> |
| Flarum core discussion events  | <span class="yes">Yes</span> | <span class="yes">Yes</span> |
| Flarum core post events        | <span class="yes">Yes</span> | <span class="yes">Yes</span> |
| Flarum core extensions events  | <span class="yes">Yes</span> | <span class="yes">Yes</span> |
| Flarum core admin panel events | <span class="no">No</span>   | <span class="yes">Yes</span> |
| Community extensions events    | <span class="no">No</span>   | <span class="yes">Yes</span> |
| **Browsing**                   |                              | |
| Via admin panel                | <span class="yes">Yes</span> | <span class="yes">Yes</span> |
| Via discussion and profiles    | <span class="no">No</span>   | <span class="yes">Yes</span> |
| Customize who can see the logs | <span class="no">No</span>   | <span class="yes">Yes</span> |
| IP Country indicator           | <span class="no">No</span>   | <span class="yes">Yes</span> |
| **Support**                    |                              | |
| Support                        | Community-only               | Email |
| Download                       | Via Packagist                | Via Extiverse |

## Changelog

### Version 1.5.1 - March 22, 2022

- Fix compatibility issues with some admin themes.

### Version 1.5.0 - February 28, 2022

- <span class="pro-badge">pro only</span> Add limited access permission and settings.
- <span class="pro-badge">pro only</span> Add forum-side log access via session dropdown for users who cannot access admin panel.
- <span class="pro-badge">pro only</span> Add optional IP country indicator. See [documentation](#ip-country-indicator) for how to enable.

This version requires Flarum version 1.2 or higher.

<details markdown="1">
<summary markdown="span">Show older releases</summary>

### Version 1.4.2 - August 25, 2021

- Fix Flarum boot error if Flags extension has been uninstalled via Composer.

### Version 1.4.1 - July 21, 2021

- Fix IP address not logged for login and signup.

FoF Ban IP support has been confirmed.

### Version 1.4.0 - June 3, 2021

- Add compatibility with Flarum 1.0.
- Add support for Flarum Nickname extension.
- <span class="pro-badge">pro only</span> Add separate logs for nickname change requests in FoF Username Request extension.
- <span class="pro-badge">pro only</span> Add "reason" log for FoF Impersonate extension (visible under raw log).
- <span class="pro-badge">pro only</span> Fix "edited at" not correctly logged for Author Change extension.
- <span class="pro-badge">pro only</span> Slug and display name driver settings changes are now logged with their values.

FoF Ban IP support is still included but has not been tested for compatibility because it has not been updated for Flarum 1.0 yet.

This version can be installed on Flarum 1.0.0 and all future 1.x versions.
It will be automatically installed when you upgrade to Flarum 1.0 by following the official release guide.

### Version 1.3.3 - March 19, 2021

- Add compatibility with Flarum beta 16.
- Fix `post.dismissed_flags` being incorrectly logged every time a post was permanently deleted.

This version can only be installed on Flarum beta 16.
It will be automatically installed when you upgrade to Flarum beta 16 by following the official release guide.

### Version 1.3.2 - February 28, 2021

- Fix old email not being logged when users change email through the email change feature.
- Fix error in the log browser when a `user.suspended` or `post.create_date_changed` log was visible.

### Version 1.3.1 - December 28, 2020

- Add compatibility with Flarum beta 15.
- Use native Flarum admin page.
- Fix incorrect tag change log.

Due to a [a change](https://github.com/flarum/core/issues/2514) in Flarum security release 14.1 for Tags, Audit Log was no longer able to log tag changes correctly.
This resulted in the old tags being logged as both old and new.
The fix is only available for beta 15.

This version can only be installed on Flarum beta 15.
It will be automatically installed when you upgrade to Flarum beta 15 by following the official release guide.

### Version 1.3.0 - October 20, 2020

- Add compatibility with Flarum beta 14.
- Add missing text for `post.approved` action.
- Add `reason` information to `post.flagged` action.
- Only log `post.flagged` for flags submitted by users (no longer logs flag creation by Approval/Akismet).
- Add `post.dismissed_flags` action.

This version cannot be installed on Flarum beta 13.
It will automatically install when you upgrade to Flarum beta 14 by following the official release guide.

### Version 1.2.2 - July 16, 2020

- <span class="pro-badge">pro only</span> Fix PHP Warning being issued during permission change.

This release was not tagged for the free version.

### Version 1.2.1 - July 11, 2020

- Fix for wrong version being read causing the admin page to fail loading.

### Version 1.2.0 - July 11, 2020

- Add missing translation for "comment".
- <span class="pro-badge">pro only</span> Add support for `clarkwinkelmann/flarum-ext-author-change`.

### Version 1.1.0 - July 9, 2020

- Separate extension into Free and Pro.
- Rename pro package from `kilowhat/flarum-ext-audit` to `kilowhat/flarum-ext-audit-pro`.
- Add admin page header with documentation links and version.

### Version 1.0.1 - June 21, 2020

- Fix `user:` search gambit not being compatible with MariaDB.

### Version 1.0.0 - June 14, 2020

Initial release.

</details>

## Requirements

- Flarum version must be 1.2.0 or greater
- MySQL 5.7.8+ or MariaDB 10.2.7+ (for `JSON` data type support)
- You must have SSH and Composer access on the Flarum hosting

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Audit Log provides integration with various extensions that you will find in the documentation below.

Most other Flarum extensions should work fine alongside Audit Log even if no integration is provided.

As time goes on this section will be filled with any extension that could be incompatible.

## Installation

> These instructions apply to the Pro version only.
> For the free version, consult the dedicated [Discuss](https://discuss.flarum.org/d/24432) thread.

- Purchase the ["KILOWHAT Audit Pro"](https://extiverse.com/extension/kilowhat/flarum-ext-audit-pro) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-audit-pro`
- Open the Flarum admin panel and enable the extension
- See below for the settings

## Update

> These instructions apply to the Pro version only.
> For the free version, consult the dedicated [Discuss](https://discuss.flarum.org/d/24432) thread.

When an update is available, the [Changelog](#changelog) will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/24206).

You can use the following commands to update:

    composer require kilowhat/flarum-ext-audit-pro
    php flarum migrate
    php flarum cache:clear

## Support

> Support is only available for users of the Pro version.

If you are having issues with the extension, check the following:

- If the extension doesn't install, check you have correctly configured Extiverse's private repository.
- If an error happens during activation or usage of the extension, check the logs in `<flarum>/storage/logs`.

If you are still having issues, please copy the output of the logs above, as well as the output of `php flarum info` and send an email to <support@kilowhat.net>.

Support is provided on a "best effort" basis.
Most replies should usually be within 24h.

I only provide help solving specific issues with the extension.
I won't install the extension for you.

## Extension settings

The extension has a single setting which is a permission found on the Permissions page of the admin panel.

### View audit log <span class="pro-badge">pro only</span>

Users with this permission can access all logs via the session dropdown and user/discussion pages.

### View limited audit log <span class="pro-badge">pro only</span>

Users with this permission get access to the same UI as the first permission, but only a subset of the logs will be visible.

The button next to the permission name lets you configure what is visible:

- **View IP Address**: restricts visibility of the IP address. The country indicator stays visible to every user with access to the logs.
- **Actions**: select which actions are visible. If you hide all of `user.*` or `discussion.*`+`post.*`, the corresponding log button is hidden from user or discussion page.

### IP Country Indicator

The IP country is not shown by default.
To enable, download the latest mmdb file from <https://db-ip.com/db/download/ip-to-country-lite> and extract it to `<flarum>/storage/dbip-country-lite.mmdb`.

If you are giving access to the logs to other users, you are responsible for adding the DB-IP attribution to your page.

The extension should also work with the commercial version of DB-IP, but it has not been tested.

## Logged actions

The following actions are currently logged.

A log consists of the following information:

- an action name
- the date and time
- The ID of the subject resource being modified or interacted with
- The client, which can be:
  - `session`: Cookie session, usually the Flarum web interface
  - `access_token`: Direct API request with a user's access token
  - `api_key`: Direct API request with a master API key
  - `cli`: Flarum command ran via SSH
  - `unknown`: Default in case none of the above can be verified
- The IP address (only available for web requests)
- The actor (usually only available for web requests)
- Additional log data indicated below

**Important**: the "Filter logs" search field provided by the extension only supports a selection of built-in gambits.
Typing anything else in the search field will have no effect.

The following gambits can be used to search in logs:

- `action:<name>` (see action names below)
- `actor:<username>`
- `client:<client>` (see clients above)
- `discussion:<id>` - returns both discussion and post events for the discussion
- `ip:<ip>`
- `user:<username>`

### Flarum Core

- `cache_cleared` <span class="pro-badge">pro only</span>: When the cache is manually cleared
- `discussion.created`: When a discussion is created
- `discussion.deleted`: When a discussion is permanently deleted
- `discussion.hidden`: When a discussion is soft-deleted
- `discussion.renamed`: When a discussion title changes (data logged: old title, new title)
- `discussion.restored`: When a soft-deleted discussion is restored
- `extension.enabled` <span class="pro-badge">pro only</span>: When an extension is enabled via the admin panel
- `extension.disabled` <span class="pro-badge">pro only</span>: When an extension is disabled via the admin panel
- `extension.uninstalled` <span class="pro-badge">pro only</span>: When an extension is rolled back via the admin panel
- `permission_changed` <span class="pro-badge">pro only</span>: When a permission is edited via the admin panel (data logged: old groups, new groups)
- `post.created`: When a post is created
- `post.deleted`: When a post is permanently deleted
- `post.hidden`: When a post is soft-deleted
- `post.restored`: When a soft-deleted post is restored
- `post.revised`: When a post content is edited (no data logged at this time)
- `setting_changed` <span class="pro-badge">pro only</span>: When a setting is edited via the admin panel (data logged: old value, new value. data is logged only for known non-sensitive fields)
- `user.activated`: When a user is activated by an administrator or extension
- `user.activated_with_email`: When a user is activated via the activation email
- `user.avatar_changed`: When a user avatar is replaced with a new avatar
- `user.avatar_removed`: When a user avatar is removed
- `user.created`: When a user is created
- `user.deleted`: When a user is deleted permanently
- `user.email_changed`: When a user email is changed (data logged: old email, new email)
- `user.email_change_requested`: When an email change is requested for a user (data logged: new email)
- `user.groups_changed`: When the groups of the user are changed (data logged: old groups, new groups)
- `user.logged_in`: When a user is logged in via the login form
- `user.logged_in_with_provider`: When a user is logged in via social login
- `user.logged_out`: When a user is manually logged out
- `user.password_changed`: When a user password is changed
- `user.password_change_requested`: When a password change is requested for a user
- `user.provider_connected`: When a new social login is connected to a user account
- `user.username_changed`: When a user username is changed by an administrator (data logged: old username, new username)

The following actions were purposefully silenced to reduce duplicated logs for a same event:

- `user.activated` is not logged if the user was enabled during its creation with the `isEmailConfirmed` attribute
- `user.avatar_changed` is not logged if an avatar was automatically set via social login
- `user.logged_in_with_provider` is not logged the first time a provider is connected to an account, as `user.provider_connected` is already logged

**Known issue**: when the audit extension is enabled, it is unable to log the author and client used.
As such, the activation of the extension is shown as Guest / unknown.

### Flarum Approval

- `post.approved`: When a post is approved

### Flarum Flags

- `post.flagged`: When a post is flagged (data logged: reason, since version 1.3.0)
- `post.dismissed_flags`: When the flags of a post are dismissed.

### Flarum Lock

- `discussion.locked`: When a discussion is locked
- `discussion.unlocked`: When a discussion is unlocked

### Flarum Nicknames

- `user.nickname_changed`: When the nickname is changed via the Nicknames extension

### Flarum Sticky

- `discussion.stickied`: When a discussion is stickied
- `discussion.unstickied`: When a discussion is unstickied

### Flarum Suspend

*Note:* There is no log when a ban naturally expires.

- `user.suspended`: When a user is suspended (data logged: until date)
- `user.unsuspended`: When a user is manually unsuspended

### Flarum Tags

- `discussion.tagged`: When the tags of a discussion are modified (data logged: old tags, new tags)
- `tag.created` <span class="pro-badge">pro only</span>: When a tag is created
- `tag.deleted` <span class="pro-badge">pro only</span>: When a tag is permanently deleted
- `tag.updated` <span class="pro-badge">pro only</span>: When a tag is modified via the admin panel

### FriendsOfFlarum Ban IPs

- `fof_ban_ips.banned` <span class="pro-badge">pro only</span>: When an IP is banned (data logged: IP, reason)
- `fof_ban_ips.unbanned` <span class="pro-badge">pro only</span>: When an IP is unbanned (data logged: IP)

**Known issue**: `unbanned` is not logged when unbanning a single issue due to [FriendsOfFlarum/ban-ips#4](https://github.com/FriendsOfFlarum/ban-ips/issues/4).

### FriendsOfFlarum Impersonate

- `user.impersonated` <span class="pro-badge">pro only</span>: When a user is impersonated (data logged: reason)

### FriendsOfFlarum Mason

No integration planned. Waiting for a Mason update.

### FriendsOfFlarum Masquerade

Integration planned.

### FriendsOfFlarum Pages

Integration planned.

### FriendsOfFlarum Split

*Note:* due to the immutability of audit logs, logs related to a post prior to the split won't be visible in the new discussion audit log modal.
The `discussion:` gambit will only return posts if those posts were in the given discussion at the moment of the event.

- `discussion.split_away` <span class="pro-badge">pro only</span>: When a discussion is split (data logged: new discussion ID, number of posts moved)
- `discussion.split_into` <span class="pro-badge">pro only</span>: When a discussion is split (data logged: original discussion ID, number of posts moved)

Two events are used together so that they easily appear in both discussion's history.

### FriendsOfFlarum Terms

Integration planned for a future release.

### FriendsOfFlarum Upload

No integration planned.

All files upload and downloads are already logged by Upload itself.

### FriendsOfFlarum User Bio

- `user.bio_changed` <span class="pro-badge">pro only</span>: When a user bio is changed

### FriendsOfFlarum Username Request

- `user.username_requested` <span class="pro-badge">pro only</span>: When a username request is created (data logged: new username)
- `user.username_request_approved` <span class="pro-badge">pro only</span>: When a username request is approved (data logged: old username, new username)
- `user.username_request_rejected` <span class="pro-badge">pro only</span>: When a username request is rejected (data logged: new username, reason)
- `user.nickname_requested` <span class="pro-badge">pro only</span>: When a nickname request is created (data logged: new nickname)
- `user.nickname_request_approved` <span class="pro-badge">pro only</span>: When a nickname request is approved (data logged: old nickname, new nickname)
- `user.nickname_request_rejected` <span class="pro-badge">pro only</span>: When a nickname request is rejected (data logged: new nickname, reason)

### KILOWHAT Cimaise

Integration planned for a future release.

### KILOWHAT Custom Paths

No special integration.

Settings changes are logged by `setting_changed`.

### KILOWHAT Formulaire

Integration planned for a future release.

### KILOWHAT Wordpress Integration

No special integration.

Wordpress synchronisation will be logged under the actor selected for "Flarum User ID" and will show client "API Key" with the IP of your Wordpress server.

Settings changes are logged by `setting_changed`.

**Known issue**: no login or logout are logged for Wordpress users using SSO.

### ClarkWinkelmann Author Change

- `discussion.create_date_changed` <span class="pro-badge">pro only</span>: When a discussion start date is changed
- `discussion.user_changed` <span class="pro-badge">pro only</span>: When a discussion author is changed
- `post.create_date_changed` <span class="pro-badge">pro only</span>: When a post start date is changed
- `post.edit_date_changed` <span class="pro-badge">pro only</span>: When a post edit date is changed
- `post.user_changed` <span class="pro-badge">pro only</span>: When a post author is changed

### ClarkWinkelmann Catch The Fish

No integration planned.

### ClarkWinkelmann Create User Modal

No special integration.

Users created by administrators will reflect the administrator as the actor instead of Guest.

### ClarkWinkelmann Passwordless

No special integration.

Users logging in via passwordless will be logged as `user.logged_in` like password logins.

### ClarkWinkelmann Status

Integration planned, but only after Status gets an overhaul.
