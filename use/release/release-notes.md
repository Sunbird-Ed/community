# Release notes

<table data-full-width="true"><thead><tr><th>Release Version</th><th>Date</th></tr></thead><tbody><tr><td>7.0.0</td><td>TBD</td></tr></tbody></table>

### Overview

This release focusses on the removal of hard-coded values within mobile and web applications enabling adopters to create their own frameworks and customise the features as per their requirements. Furthermore, in compliance with Google Play's regulations, the inclusion of an account deletion feature for Android users has now been mandated.

Discussion thread: [https://github.com/orgs/Sunbird-Ed/discussions/669](https://github.com/orgs/Sunbird-Ed/discussions/669)

### New Features

#### **1.** **Delete user functionality for Android users (**[**LR-683**](https://project-sunbird.atlassian.net/browse/LR-683)**)**

<details>

<summary>Details</summary>

Sunbird Mobile and Web app will comply with the [Google Play app's account deletion requirements](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en#zippy=%2Cwhat-users-will-see-if-your-app-supports-account-deletion). It has mandated that if the app allows users to create their account, it must also allow users to request account deletion. This will establish transparency and give users control over their data.

The User Data policy's [Account Deletion Requirement](http://support.google.com/googleplay/android-developer/answer/13316080#account\_deletion) means that:&#x20;

1. All developers must complete new Data deletion questions in the Data safety form on the [**App content**](https://play.google.com/console/app/app-content/summary) page (Policy > App content) in Play Console.
2. If your app enables account creation, you must:
   * provide users with an in-app path to delete their app accounts and associated data; and&#x20;
   * provide a web link resource where users can request app account deletion and associated data deletion.&#x20;

For more details, refer to this [link](../../misc/misc-pages/minimal-build-properties-1.md).

</details>

#### **2.** Generalisation of Sunbird ED by r**emoval of hard-coded values in Mobile and Portal (**[**ED-1957**](https://project-sunbird.atlassian.net/browse/ED-1957)**,** [**ED-3042**](https://project-sunbird.atlassian.net/browse/ED-3042)**)**

<details>

<summary>Details</summary>

Previously, Sunbird ED supported only a single domain, i.e., Education. Now, adopters can create their framework and customise the features per their requirements.&#x20;

The features have been made dynamic by removing the hard-coded values in the portal and the mobile app.

#### **Note (only for existing adopters)**

1. **Portal -** Update the [menu bar forms](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Menu-Bar-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference).

From release-7.0.0, the hardcoding of ALL tab/global filters has been removed, and the menu bar forms have been modified within the ALL tab section inside the metadata object as `globalFilterConfig`

2. **Mobile -** Update the [framework config forms](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3452239908/Framework+Agnostics+Release+7.0.0#Form%3A-Framework\_update\_config).

Follow the links to configure the forms step-by-step for the [portal](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3434512396/ED-Portal+Framework+Agnostics+Release+7.0.0) and [mobile](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3452239908/Framework+Agnostics+Release+7.0.0#Form:-Framework\_update\_config).

</details>

### Enhancements / Technical Tasks

#### **1.**[ ](https://github.com/Sunbird-Ed/Community/blob/7e03a2a3a6d002b0f80afa6c5a80994949125228/use/releases/release-notes/6.0.0-draft.md#enhancements-technical-tasks-details)Capacitor migration ([ED-2963](https://project-sunbird.atlassian.net/browse/ED-2963))

<details>

<summary>Details</summary>

Migration from Cordova to Capacitor version 5

Note: Capacitor beta version is done

</details>

#### **2.** Improved file upload feedback **(**[**ED-1629**](https://project-sunbird.atlassian.net/browse/ED-1629)**)**

<details>

<summary>Details</summary>

Users will now see a pop-up message and an error icon if any files fail to upload when they submit or sync their projects. Users can also re-upload or remove the files with errors.

</details>

#### 3. Enhanced task end date validation ([ED-1373](https://project-sunbird.atlassian.net/browse/ED-1373))

<details>

<summary>Details</summary>

Users can now only set the task end date within the project start and end dates. Users will also get confirmation pop-ups if changing the project dates affects the task end dates.

</details>

#### 4. Content creation screen in Workspace is enhanced ([ED-2429](https://project-sunbird.atlassian.net/browse/ED-2429))

<details>

<summary>Details</summary>

Currently, the content creation screen in the workspace is static. This is enhanced, and it is made dynamic and configurable.

</details>

### Bug Fixes

This release had a few bug fixes. For a complete list, refer to this link



### Open/Known Bugs

There are a few known bugs in this release. For a complete list, refer to this link

1. Observation led imp flow is not working as expected for the projects that has certificates ([ED-3261](https://project-sunbird.atlassian.net/browse/ED-3261))
2. Project is already available in the program even without importing it ([ED-3280](https://project-sunbird.atlassian.net/browse/ED-3280))
3. NVSK data issue ([ED-3094](https://project-sunbird.atlassian.net/browse/ED-3094))

### Build Tags

The build tags used by the below building blocks for this release to upgrade your Sunbird ED are:

_Sunbird ED_

_Sunbird Lern_

_Sunbird Obsrv_

_Sunbird-Knowlg_

_Sunbird-InQuiry_

### Installation or Upgrade

_For fresh installation 7.0.0_

_Upgrade Sunbird from 6.0.0 to 7.0.0_

### Configuration/Environment variable

This section provides a list of environment variables with their default values and descriptions required to run either the Sunbird portal or mobile service. To change the default behavior, modify the variable value based on your requirements.

_Adding new variables_

### Deprecations and Removals

This section provides the list of APIs that are deprecated or removed from this release.

_Note: There are no APIs deprecated or removed in this release._

### Breaking Changes

Portal:&#x20;

Mobile:

### Release Notes: Dependent building blocks

Sunbird-Knowlg: [V 5.7.0](https://knowlg.sunbird.org/use/release-notes/release-5.7.0-latest)

Sunbird-Obsrv: [V5.1.0](https://obsrv.sunbird.org/use/release-notes/release-v-5.1.0)

Sunbird-Lern: [V7.0.0](https://lern.sunbird.org/use/release-notes/release-v-7.0.0)

Sunbird-inQuiry: [V7.0.0](https://inquiry.sunbird.org/use/release-notes/inquiry-release-v7.0.0-latest)
