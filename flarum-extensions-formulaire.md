---
layout: page
title: Flarum Formulaire
permalink: /flarum/extensions/formulaire
---

- **Price:** 5 USD/month + VAT depending on your country
- **Bundled translations**: English and French
- **Flarum compatibility**: beta 12+
- See purchase on [flagrow.io](https://flagrow.io/extensions/kilowhat/flarum-ext-formulaire)
- See on [Flarum Discuss](https://discuss.flarum.org/d/23063)

Table of content:

- [Introduction](#introduction)
- [Changelog](#changelog)
- [Demo](#demo)
- [Requirements](#requirements)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Support](#support)
- [Warnings](#warnings)
- [Extension settings](#extension-settings)
- [Form options](#form-options)
- [Submission options](#submission-options)
- [Field options](#fields-options)
- [Import and export](#import-and-export)
- [Extensibility](#extensibility)

## Introduction

Formulaire is a premium extension bringing an advanced form builder to Flarum.

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

### Version 1.0 - March 10, 2020

Initial release.

## Demo

A demo/test website is available at <https://formulaire-demo.http418.ch/>.
An example form can be accessed at <https://formulaire-demo.http418.ch/forms/example-form>

The website will be reset manually from time to time.

Please get in touch if you would like admin access.

## Requirements

- Flarum version must be beta 12 or higher
- You must have SSH and Composer access on the Flarum hosting
- Flarum server must be able to use Bazaar, which often requires 1GB of RAM or swap

Only the current Flarum version is supported.
New features and fixes in the extension will only work with the latest Flarum version.

## Compatibility

Most other Flarum extensions should be compatible.

As time goes on this section will be filled with any extension that could be incompatible.

## Installation

- Install and enable the [Bazaar extension](https://discuss.flarum.org/d/5151-bazaar-the-extension-marketplace)
- Connect Bazaar with your flagrow.io account
- Purchase the "KILOWHAT Formulaire" extension via Bazaar or flagrow.io
- Install and enable the extension via Bazaar
- See below for the settings

## Support

If you are having issues with the extension, check the following:

- If the extension doesn't install, check your system meets Bazaar requirement and check logs under the Bazaar history tab (spinning arrow icon)
- If an error happens during activation or usage of the extension, check the logs in `<flarum>/storage/logs`

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

The following options are only available in standalone mode:

**Accept new submissions**: as it says.

**Allow users to edit their existing submissions**: as it says.

**Max submissions**: optional, the maximum number of submissions before the form automatically closes.
When the max submissions number is reached, it has the same effect as if **Accept new submissions** was disabled.
Locked submissions count towards the max submissions.
Deleted submissions no longer count towards the max submissions.

**Send confirmation email to participants**: toggle to send an email with a summary of the answers to the user who submitted the form.
If the form contains a field with key `email`, an email will also be sent to that address.

**Send a copy of the data to those comma-separated emails**: when filled, an email with a summary of the answers is sent to those addresses.

**Confirmation message on the web**: optional, the message to show once the field has been submitted.
This message is not secret, it's exposed via the API even to users who did not submit the form yet.

**Confirmation message via email**: optional, the message to show at the top of the email sent to users.
Only has an effect if **Send confirmation email to participants** is enabled.

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
