---
layout: page
title: Flarum Formulaire
permalink: /flarum/extensions/formulaire
---

[![Extiverse badge](https://extiverse.com/extension/kilowhat/flarum-ext-formulaire/badge)](https://extiverse.com/extension/kilowhat/flarum-ext-formulaire)

- **Price**: 5 USD/month or 50 USD/year
- **Bundled translations**: English and French
- **Flarum compatibility**: beta 13+
- See and purchase on [Extiverse](https://extiverse.com/extension/kilowhat/flarum-ext-formulaire)
- See on [Flarum Discuss](https://discuss.flarum.org/d/23063)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Demo](#demo)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Update](#update)
- [Support](#support)
- [Warnings](#warnings)
- [Extension settings](#extension-settings)
- [Form options](#form-options)
- [Submission options](#submission-options)
- [Field options](#fields-options)
- [Replacement variables](#replacement-variables)
- [Import and export](#import-and-export)
- [Extensibility](#extensibility)

## Introduction

Formulaire is a premium extension bringing an advanced form builder to Flarum.

<iframe width="740" height="416" src="https://www.youtube.com/embed/reFqzTzAof4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Multiple form types are included:

### Standalone

Similar to Google Forms.

These forms are not linked to other flarum resources and you can control who is allowed to create or fill them.
The author of submissions is recorded for logged in users.
You can customize max submissions and configure email notifications.

*Example use cases:* contact form, survey, event registration, ...

*Planned features:* submission limit per user, anonymous submissions, editable submissions for guests.

### User profile

Similar to Flagrow Masquerade.

Each user profile form becomes a new page under a user profile.

At the moment the profile fields are private.
Only moderators and the user itself can see the answers.

Each form can be configured so that only members of a given group must fill it.

*Example use cases:* private contact info, payment details, curriculum vitae, ...

*Planned features:* public profile, user card fields, registration fields.

### Discussion fields (beta)

Similar to Flagrow Mason. 

The fields show up on discussions.
The discussion author is able to edit them.

This feature is in beta and fields can only be filled after a discussion has been created for now.

*Planned features:* fields in discussion composer.

## Changelog

### Version 1.1.0 - October 21, 2020

- **Changed:** it is now possible to enable notifications on non-standalone forms.
- **Changed:** "accept submissions" and "allow edit" form settings now also available to non-standalone forms.
- **Changed:** Viewing profile and discussion forms is now controlled by additional permissions instead of the global "view submission list" permission.
- **Added:** new feature to create discussions automatically from a submission for Discussion fields.
- **Added:** customizable title and body in notification emails.
- **Fixed:** file uploads being invisible in readonly submissions.
- **Fixed:** issue when Formulaire was enabled while Tags was disabled.

This version is only compatible with Flarum beta 13.
The Flarum beta 14 update will be released within a week.

The new features were sponsored by [Konica Minolta](https://www.aire.link/). Thanks!

### Version 1.0.2 - May 6, 2020

- Fix issues with drag and drop in form editor and multi-field
- Use new beta 13 features, add beta 13 compatibility

### Version 1.0.1 - March 20, 2020

- Add missing code in policy that had been removed by mistake in 1.0.0

### Version 1.0 - March 10, 2020

Initial release.

## Demo

A demo/test website is available at <https://formulaire-demo.http418.ch/>.
An example form can be accessed at <https://formulaire-demo.http418.ch/forms/example-form>

The website will be reset manually from time to time.

Please get in touch if you would like admin access.

## Requirements

- Flarum version must be beta 13
- MySQL 5.7.8+ or MariaDB 10.2.7+ (for `JSON` data type support)
- You must have SSH and Composer access on the Flarum hosting

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Most other Flarum extensions should be compatible.

As time goes on this section will be filled with any extension that could be incompatible.

## Installation

- Purchase the ["KILOWHAT Formulaire"](https://extiverse.com/extension/kilowhat/flarum-ext-formulaire) extension via the Extiverse website
- If this is your first premium extension purchase from Extiverse, follow the "Composer configuration" instructions available at <https://extiverse.com/premium/subscriptions>
- Install the extension via Composer: `composer require kilowhat/flarum-ext-formulaire`
- Open the Flarum admin panel and enable the extension
- See below for the settings

## Update

When an update is available, the [Changelog](#changelog) will be updated above and a message will be posted on the [Flarum Discuss discussion](https://discuss.flarum.org/d/23063).

You can use the following commands to update:

    composer require kilowhat/flarum-ext-formulaire
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

## Warnings

Once a form has started to receive submissions, you must use caution with the template editing.

Adding new fields is generally safe.

Changing a field type, changing a field key or deleting a field will cause a loss of data.
The data for those fields will not be immediately removed from the database, but any edit to a submission will remove the existing data about fields that no longer exist.

Changing a field type could break the ability to edit submissions.
To be safe, always delete a field you no longer use and create a new one.
Or manually change the field key.

Deleting an upload field will not delete the associated files on disk.
Delete the submission or form to delete the associated files.

## Extension settings

### Settings modal

**Max file size**: the maximum file size for the upload field type.
Please note that if a user tries to upload a file bigger than your PHP file limit, the web server will throw an error before Flarum can even start.
A Flarum validation error only shows up for files that are between the specified size and the PHP file limit.

**Show undo/redo controls on submission page**: toggle to enable the undo/redo buttons in submissions.

**Show side navigation on submission page**: toggle to show the left navigation from the homepage on submission pages in standalone mode.
By default the form is shown centered on the page without any side navigation.

### Permission

**Fill standalone forms**: which users can fill standalone forms.
It is planned to make it customizable per-form, but the permission is currently global.

**View user profile submissions**: which users can see profile fields on all user profiles.
By default users can only see their own submissions.
*Available since version 1.1.0.*

**View discussion fields submissions**: which users can see discussion fields on all discussions.
By default users can only see their own submissions.
*Available since version 1.1.0.*

**Create forms (beta)**: which users can create new forms.
The owner of a form can manage the form options and submissions.
At the moment the owner cannot see the list of submissions.

**Moderate all forms**: which users can see/edit all forms and submissions.

**View the list of forms that aren't deleted** (for third-party extensions): allows listing all forms, even if they no longer accept submissions.
This permission was added for third-party extensions that might want to list forms to visitors.
The extension doesn't include such a list by itself.

**View the list of submissions** (for third-party extensions): allows users to list their own submissions.
This permission was added for third-party extensions that might want to list submissions to visitors.
The extension doesn't include such a list by itself.

## Form options

**Expert mode**: toggles between normal and expert mode in the template builder.
This only switches the mode in your own browser and is not saved along with the form.

**Special form types**: choose the type of form.
See [Introduction](#introduction) for the explanation of the different types.

**Title**: title of the form.
Visible to users.

**Slug**: optional, token for the url.
By default the url to the form will be a UUID.
For standalone forms, the form will be available at `/forms/<slug or uuid>`.
Profile forms will be available at `/u/<username>/forms/<slug or uuid>`.

**Automatically create discussions from form submission**: only available for discussion fields.
When disabled, submissions can only be created from an existing discussion page.
When enabled, submissions can also be created through the form url like if it was a standalone form.
When created through the standalone form, a discussion will automatically be created and attached to the submission.
*Available since version 1.1.0.*

**Options for new discussions**: available when *Automatically create discussions from form submission* is enabled.
**Discussion title** and **Post content** accept replacement variables as described in [Replacement variables](#replacement-variables).
If not specified, Formulaire will attempt to find a field with a slug of `title` and `content` respectively, and default to the form title and an empty content.
**Discussion tags** accepts a comma-separated list of tag slugs.
The tag the form is linked to (if selected) will always be added in addition to this list of tags.

**Accept new submissions**: as it says.
Prior to version 1.1.0, was only available for standalone forms.

**Allow users to edit their existing submissions**: as it says.
Prior to version 1.1.0, was only available for standalone forms.

**Max submissions**: optional, the maximum number of submissions before the form automatically closes.
When the max submissions number is reached, it has the same effect as if **Accept new submissions** was disabled.
Locked submissions count towards the max submissions.
Deleted submissions no longer count towards the max submissions.
Prior to version 1.1.0, was only available for standalone forms.
It is not advisable to set this setting for non-standalone forms.

**Send confirmation email to participants**: toggle to send an email with a summary of the answers to the user who submitted the form.
If the form contains a field with key `email`, an email will also be sent to that address.

**Confirmation email template**: available when *Send confirmation email to participants* is enabled.
**Title** and **Body** accept replacement variables as described in [Replacement variables](#replacement-variables).
Title defaults to the name of the form while Body defaults to an empty string.

**Send a copy of the data to those comma-separated emails**: when filled, an email with a summary of the answers is sent to those addresses.

**Notification email template**: available when *Send a copy of the data to those comma-separated emails* is enabled.
**Title** and **Body** accept replacement variables as described in [Replacement variables](#replacement-variables).
Title defaults to the name of the form while Body defaults to an empty string.

**Confirmation message on the web**: optional, the message to show once the field has been submitted.
This message is not secret, it's exposed via the API even to users who did not submit the form yet.

**Confirmation message via email**: optional, the message to show at the top of the email sent to users.
Only has an effect if **Send confirmation email to participants** is enabled.
*In version 1.1.0, this option was moved to Confirmation email template*.

**Delete**: forms can be soft-deleted.
A soft-deleted form will no longer be visible to users and will no longer accept answer or edits to submissions.
A soft-deleted form can be permanently deleted.

## Submission options

**Lock**: prevents the submission from being edited, even if **Allow users to edit their existing submissions** is enabled on the form.

**Delete**: soft-deletes the submission.
A soft-deleted submission will no longer be visible to the author and cannot be edited.
A soft-deleted submission no longer counts towards the submission count.
A soft-deleted submission can be permanently deleted.

## Fields options

This section explains the options available for fields.

Common options between all field types:

**Title**: rendered above the field in a title tag.

**Description**: rendered below the title in a paragraph tag.
Formatting is not possible.

**Required**: marks the field as required.

When you enable **Expert mode**, additional options become available:

**JSON key**: this is the key used internally to save the field value as part of a JSON object.
A key must be unique across a level of fields.
Fields can use the same key if one is inside of a multi-entry.
Changing a key once data has been submitted will result in loss of data for that field!

**Fill permission**: controls which users can edit the field value.
A user can always see the value.
If a user doesn't have the permission, they will be enable to change the field value from the current value.
If the field is required but doesn't have a current value, the user will be unable to submit the form.

### Short text

Text field rendered as an HTML text input.

**Email**: toggle to apply email validation to the field value.

**Regular expression**: optional, enter a custom regular expression to validate the field value.

### Long text

Text field rendered as an HTML textarea.

**Minimum**: optional, minimum (inclusive) number of characters to enter.
Only applies if some content was entered or if the field is required.

**Maximum**: optional, maximum (inclusive) number of characters to enter.
When specified, a character counter will be shown underneath the field.

**Rich text**: enables formatting through Flarum's TextFormatter (same as in posts).
When enabled, a preview will appear above the field.

### Number

Field rendered as an HTML number input.

**Integer**: toggle to apply integer validation to the field.

**Minimum**: optional, minimum (inclusive) value for the field value.

**Maximum**: optional, maximum (inclusive) value for the field value.

### Date

**Minimum**: optional, minimum (inclusive) allowed date.

**Maximum**: optional, maximum (inclusive) allowed date.

### Content

This special field simply renders custom content.
It has no title and no description.
It doesn't cause any value to be added to submissions.

Formatting is done through Flarum's TextFormatter (same as in posts).

### Upload

File upload.
By default, multiple files can be uploaded.

At this time, only local file storage is enabled.

**MIME type**: Allowed MIME types for the uploaded files.
The MIME detection is using Symfony's MIME guesser.
PHP files are always blocked.

**Minimum**: optional, minimum (inclusive) number of files.
Only applies if the number of files is greater than zero or if the field is required.

**Maximum**: optional, maximum (inclusive) number of files.

*Limitations*: file upload is not possible inside a multi-entry field.

### Multi-entries

This special field allows to create a sub-form inside of the main form.

**Minimum**: optional, minimum (inclusive) number of allowed entries.
Only applies if the number of entries is greater than zero or if the field is required.

**Maximum**: optional, maximum (inclusive) number of allowed entries.

*Limitations*: only one level deep is possible.

## Replacement variables

Some fields accept "magic" text that will be replaced with a value from the form submission or other record.

Consult the documentation above to see which fields support "Replacement variables".

A variable takes the form `{slug}` where `slug` must be the slug of a field that's at the first level of the submission.
The slug of a field can be obtained or modified by turning on "Expert mode" on the form builder.
By default slugs are long unique UUIDs, so the replacement variable will look something like `{af927b85-f19a-4710-8c94-add4ea6c3ca6}`.
Fields that are more than one level deep (Multi-entries) are not available.

The documentation above refers to `{title}` and `{content}`.
Those variables look for fields that have been manually applied a slug of `title` or `content` respectively.

The following special values are also available for replacement, assuming no field exists with the same slug:

- `{user_id}`: ID of the submission owner.
- `{user_display_name}`: Display Name of the submission owner.
- `{user_username}`: Username of the submission owner.
- `{user_email}`: Email of the submission owner.
- `{user_group_ids}`: Comma-separated list of group IDs the submission owner belongs to.
- `{user_group_names}`: Comma-separated list of singular group names the submission owner belongs to.

"Submission owner" refers to the user attached to a submission.
It's always the actor for a standalone form, but will be the author of the discussion for discussion fields and the subject for profile fields, even if another user is the first to fill in that form.

For example if you had a field "Date" with slug `af927b85-f19a-4710-8c94-add4ea6c3ca6`, you could set the confirmation email to

```text
Confirmation of your appointment on {af927b85-f19a-4710-8c94-add4ea6c3ca6}
```

And you could set the notification email (to admin) to:

```text
{user_username}'s appointment on {af927b85-f19a-4710-8c94-add4ea6c3ca6}
```

## Import and export

### Submissions

More options will be added in later releases.
At the moment you can only access the raw data of the submissions via the database.

The `data` column of the `formulaire_submissions` table contains a JSON object representing a submission.
Each key of the JSON object can be customized via "expert mode" in the form opions.

Files are stored separately.
The JSON object just contains the UUID of the uploaded file(s).

### Forms

A form template is described by a JSON object.
That template can be copied from the textarea below the template editor.

You can paste a template into another form's template editor to create a new form with identical fields.

## Extensibility

Formulaire is designed to be highly extensible by other extensions.

Every javascript component is exposed and can be extended.

PHP events exist for `SubmissionCreated` and `SubmissionUpdated`.

If you would like to create an integration, feel free to reach out to me.
I'll need to find a way to share documentation about the javascript API.
