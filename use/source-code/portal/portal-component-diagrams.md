---
description: >-
  The Sunbird portal is the browser-based interface for the Sunbird application
  stack. It provides a web app through which all functionality of Sunbird can be
  accessed.
---

# Component Diagram

## GitHub Repository

{% embed url="https://github.com/Sunbird-Ed/SunbirdEd-portal" %}
git
{% endembed %}

## Architecture

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption><p>Sunbird ED Portal Architecture</p></figcaption></figure>

## Sunbird ED Portal

The Sunbird ED portal is divided into two folders

**App:** Contains the back-end code base, which uses the Node.js framework for server-side.

**Client**: Contains the front-end code base which uses Angular framework for client-side.

![](<../../../.gitbook/assets/image (22).png>) ![](<../../../.gitbook/assets/image (23).png>)

## **Sunbird Portal UI**

![](<../../../.gitbook/assets/image (2) (1).png>) ![](<../../../.gitbook/assets/image (3) (1).png>)

[**Client Folder**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app/client) includes the client source code for the Angular application. This folder includes various components, modules, services, styles, and other assets necessary to build the front end of the application.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-08-09 at 10.56.12 AM.png" alt=""><figcaption><p>Sunbird Portal UI Architecture</p></figcaption></figure>

### **Key modules used in the Sunbird Portal**&#x20;

The objective of the following modules or folders is to provide all the features in one place, which can be leveraged further if needed.

#### [Public](https://sunbird-ed.github.io/docs/portal/modules/PublicModule.html)

**Objective**: To provide all the public routes (i.e. consumers).

This folder contains routing for the modules that can be accessed by everyone and does not have any auth required, such as guest user/anonymous user.

#### [Core](https://sunbird-ed.github.io/docs/portal/modules/CoreModule.html)

**Objective**: To provide a static screen component that is present in every route.

The folder contains those components that are statically positioned, though data will be dynamic; we can integrate the core components at the app level so that they are present in every route and also provide the routes to different modules such as the header, footer, search, main menu, and language dropdown.

#### [Shared](https://sunbird-ed.github.io/docs/portal/modules/SharedModule.html)

**Objective:** To provide all reusable features.

The folder contains all the reusable components across the portal, such as the loader, popup, card, sb-data table, alert popup, slick, etc.

#### [Manage Learn](../../../misc/misc-pages/portal-manage-learn-component-diagram.md)

Manage Learn contains tools or solutions like Observation, Projects, and Surveys. These tools are used to help the learners to learn in a structured manner.

### Additional Info:

#### Forms

In the portal, lots of UI capabilities are generalised in terms of [formConfig](https://documenter.getpostman.com/view/25186239/2s946pXoZ2) to reduce the code dependency by decoupling form logic from the portal code.

## Front-End Libraries

<figure><img src="../../../.gitbook/assets/Screenshot 2023-08-08 at 2.32.52 PM.png" alt=""><figcaption><p>Frontend libraries</p></figcaption></figure>

The purpose of all the libraries is to make the UI more consistent across all the clients who are using this library.

| Library Name       | GitHub Repo                                                                                                                                        | Description                                                                                                                                                                                                       |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Common-Consumption | [https://github.com/Sunbird-Ed/SunbirdEd-consumption-ngcomponents#readme](https://github.com/Sunbird-Ed/SunbirdEd-consumption-ngcomponents#readme) | These components are designed to be used in Sunbird consumption platforms _( web portal, offline desktop app)_ to drive reusability, maintainability hence reduce the redundant development effort significantly. |
| SB-Forms           | [https://github.com/Sunbird-Ed/SunbirdEd-forms](https://github.com/Sunbird-Ed/SunbirdEd-forms)                                                     | This Library expects a configuration and renders form according to the view.                                                                                                                                      |
| SB-Dashlet         | [https://github.com/Sunbird-Ed/sb-dashlets](https://github.com/Sunbird-Ed/sb-dashlets)                                                             | Library used for Reusable charts. Supported by charts has an extensible, general purpose analytical presentation capabilities like graphs, tables, charts etc..                                                   |
| Client-Services    | [https://github.com/Sunbird-Ed/sunbird-client-services](https://github.com/Sunbird-Ed/sunbird-client-services)                                     | Library used to create API calls with Sunbird Environment. Includes necessary typescript code to do search, content read, corresponding data models of the platform are available.                                |
| Quml Player        | [https://github.com/Sunbird-inQuiry/player/tree/release-6.0.0](https://github.com/Sunbird-inQuiry/player/tree/release-6.0.0)                       | The library which is responsible for rendering questions and question sets created according to the QuML specification.                                                                                           |
| Collection-Editors | [https://github.com/Sunbird-Knowlg/sunbird-collection-editor](https://github.com/Sunbird-Knowlg/sunbird-collection-editor)                         | Library which supports to create all type of collections like Book, Course, PlayList & QuestionSet                                                                                                                |
| Video Player       | [https://github.com/Sunbird-Knowlg/sunbird-video-player](https://github.com/Sunbird-Knowlg/sunbird-video-player)                                   | The Video player library is used to play video/audio content in Sunbird ED                                                                                                                                        |
| PDF Player         | [https://github.com/Sunbird-Knowlg/sunbird-pdf-player](https://github.com/Sunbird-Knowlg/sunbird-pdf-player)                                       | The PDF player library is used to play pdf content on Sunbird ED                                                                                                                                                  |
| Epub Player        | [https://github.com/Sunbird-Knowlg/sunbird-epub-player](https://github.com/Sunbird-Knowlg/sunbird-epub-player)                                     | The Epub player library is used to play epub content on Sunbird ED                                                                                                                                                |

## Sunbird Portal API Servcies

![](<../../../.gitbook/assets/image (4).png>) ![](<../../../.gitbook/assets/image (1) (1).png>)

[**App Folder**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app) (without client) includes back-end API interface which is used Node.js framework.

It leverages a keyCloakHelper file to handle login and logout functionalities while adopting token-based session storage to manage user sessions effectively.

Additionally, the interface integrates multiple API middleware functions to accomplish tasks such as token verification, API whitelisting, and customizing request headers as needed.

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption><p>API Layer Architecture</p></figcaption></figure>

### Code Structure

### [User Session Management - **Server.js**](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-7.0.0/src/app/server.js)

It is used in web development for the server-side entry point of a Node.js application.

It acts as the main starting point of the server, responsible for initializing the server, defining routes, and handling incoming requests from clients.

It is used to store the session based on [Anonymous](https://project-sunbird.atlassian.net/wiki/spaces/SP/pages/3324477457/Portal+-+Login+Work+flow+post+success+with+keycloak+-+Anonymous) &[ Logged in User](https://project-sunbird.atlassian.net/wiki/spaces/SP/pages/3324182538/Portal+-+Login+Work+flow+post+success+with+keycloak+-+Logged+In+User).

### [**Routes**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app/routes)

It handles all the API routes, which are triggering from the client side, such as content/\*, content/copy/questionset, etc.

### [API Whitelisting: **Helpers Folder**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app/helpers)

Contains all the js files which are used for user [authentication](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-6.0.0/src/app/helpers/kongTokenHelper.js) and [authorization](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-6.0.0/src/app/helpers/keyCloakHelper.js).

Contains the [API Whitelist](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-6.0.0/src/app/helpers/apiWhiteList.js) js file, which Handles whitelisting and role checks of Portal API(s).

### [Role check: **Proxy Folder**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app/proxy)

It contains the set-up methods such as decoraterequestHeader, verifyToken, and isApiwhitelisted, which validates whether the API request is valid or not with proper role check and auths token.

### [**ResourceBundles**](https://github.com/Sunbird-Ed/SunbirdEd-portal/tree/release-7.0.0/src/app/resourcebundles)&#x20;

It contains the resource bundles in the application for internationalization and localization purposes. It is used for translations and provides a seamless way to display the application's user interface in different languages based on user preferences.

### [EnvVariablesHelper](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-6.0.0/src/app/helpers/environmentVariablesHelper.js)

It contains the [envHelperFile](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-6.0.0/src/app/helpers/environmentVariablesHelper.js), which is responsible for storing the env variable that is required in the portal from DevOps.

## **Dependent Sunbird BBs**

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Dependent Sunbird BBs' Architecture</p></figcaption></figure>

There are lots of front-end libraries and services that we are leveraging from the other building blocks.

### **Sunbird Building Blocks, which are being used in the ED Portal**

* [Lern](https://lern.sunbird.org/)
* [Obsrv](https://obsrv.sunbird.org/)
* [InQuiry](https://inquiry.sunbird.org/learn/readme)
* [Knowlg](https://knowlg.sunbird.org/learn/readme)
* [ED](https://ed.sunbird.org/learn/readme)
