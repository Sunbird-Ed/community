# Delete User Functionality

#### JIRA ID: [**LR-683**](https://project-sunbird.atlassian.net/browse/LR-683)

### Overview

[Google Play's policy](https://support.google.com/googleplay/android-developer/answer/13327111?sjid=3212926861345917362-AP) mandates the inclusion of functionality that permits users to request account deletion. This enhances transparency and gives users control over personal data, simultaneously allowing developers to demonstrate their commitment to responsible data handling.&#x20;

### What's changing for you?

**New adopter: No changes**

For new adopters, version 7.0.0 of the release package introduces this functionality.

**Using older versions of Sunbird ED?**

If you are using older versions of Sunbird ED, you must implement the delete user functionality in your app version.

### Workflow

Let's understand the general workflow for user account deletion, which is consistent across both portal and mobile platforms.

1. Log in to your account using your credentials.
2. Click the user profile icon and select the Profile option from the menu.
3. Click the Delete Account button from the profile page.
4. Check all the Terms and Conditions checkboxes. This will confirm that you understand all the consequences of account deletion.
5. Click the Delete Account button.
6. Enter the OTP sent to your registered email address or mobile number and click the Delete account button to proceed.

Once the account is deleted, users will be logged out of the app.&#x20;

#### Detailed workflows of:

* [Portal](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3438346248/Portal+Flow+of+Delete+User+Account)&#x20;
* [Mobile App](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3499360274/Delete+User+Account+Flow)

{% hint style="warning" %}
* Deletion of your account is irreversible and may lead to permanent data loss. Please proceed with utmost caution.
* Before proceeding with the deletion process, ensure you have retrieved any important information or data associated with your account.
{% endhint %}

### Backend changes

When the account deletion is initiated, two primary actions take place in the backend:

1. The user's Personal Identifiable Information (PII) needs to be removed.
2. _The assets (like questions, content, etc.) created by this user must be transferred to an identified user - a feature coming in release 8.0.0_

The modifications to the back-end infrastructure are facilitated by three building blocks:

[Lern](https://lern.sunbird.org/use/learn-more/delete-user-functionality)

[Inquiry](https://inquiry.sunbird.org/use/learn-more/delete-user-functionality/user-pii-cleanup)

[Knowlg](https://knowlg.sunbird.org/use/release-notes/release-5.7.0#user-pii-data-updater)

{% hint style="info" %}
**Note**: The job works for all object types (including Question, QuestionSet, Content, Collection, Assets) which are configured to the job.

**Variable Name:** user\_pii\_target\_object\_types

**Description**: Target Object Type and Schema Version should be configured as value.&#x20;

Example: If you want to process 5 different objects for deleted user, then all 5 object types should be part of this configuration along with corresponding schema versions.

**Default Value:**

{ \\"Question\\": \[\\"1.0\\", \\"1.1\\"], \\"QuestionSet\\": \[\\"1.0\\", \\"1.1\\"], \\"Asset\\": \[\\"1.0\\"], \\"Content\\": \[\\"1.0\\"], \\"Collection\\": \[\\"1.0\\"] }
{% endhint %}

### Code changes

Once your back-end changes are up and running, the following code changes are required to integrate the delete user functionality into the existing code of your application:

{% hint style="warning" %}
**Note**: The provided code serves as a reference and should be customised to meet your specific requirements.
{% endhint %}

[Portal documentation](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3446538329/Portal+Adding+Delete+User+Functionality+in+Portal+for+adaptors)

[Mobile app documentation](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3494609191/Delete+User+functionality+for+adopters)

