# Architecture - Component Diagram

The architecture diagram explains the L0 architectural view of Sunbird-ED.

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-14 at 4.58.08 PM.png" alt=""><figcaption></figcaption></figure>

### Learning Apps

These are the client-facing applications where users (Admin, Creators and Consumers) can drive some capabilities.

* **Sunbird-Portal UI**\
  The Sunbird portal is the browser-based interface for the Sunbird application stack. It provides a web app through which all Sunbird functionality can be accessed.
* **Sunbird-Mobile-App**\
  The Sunbird Mobile app provides mobility to its feature-rich learning platform. It provides learners with the flexibility to learn anywhere, anytime.
* **Sunbird-Desktop**\
  It is powered by Sunbird-Portal itself. The same code-base is being used for offline access of portal application.
* **Sunbird-CoKreat (part of Sunbird-CoKreat building block)**\
  [**https://cokreat.sunbird.org/learn/readme#what-is-sunbird-cokreat**](https://cokreat.sunbird.org/learn/readme#what-is-sunbird-cokreat)

#### Video on Sunbird ED Architecture - Part 2

(Refer to this [link](https://ed.sunbird.org/learn/technical-overview/technical-architecture-diagram#video-sunbird-tech-architecture) for Part 1 of the explanation)

{% embed url="https://youtu.be/XPrhdALMHeI?si=4DgX6U6QlwgBQSqX&t=116" %}

### Front-end Libraries

Please refer to the below for more details on front-end libraries.

[independent-libraries](reference-apps/independent-libraries/ "mention")

### API Player

* Sunbird-Portal (API service)\
  Sunbird portal is packaged with Client & Server side applications. The server slide application (NodeJS) will be built and deployed independently, acting as a proxy service for the Sunbird Portal (UI) application.
* Sunbird-Creation-Portal (API service)\
  Sunbird creation portal is also packaged with Client & Server side applications. The server slide application (NodeJS) will be built and deployed independently, acting as a proxy service for the Sunbird-Creation-Portal (UI) application.
* Form service

[form-service](form-service/ "mention")

* Contribute (Program) service

{% embed url="https://cokreat.sunbird.org/contribute/contribution-service" %}

### Dependant Sunbird BB's

[dependencies.md](../learn-more/dependencies.md "mention")
