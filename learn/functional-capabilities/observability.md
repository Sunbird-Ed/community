# Observability

### <mark style="color:orange;">What is Observability?</mark>

Observability is a critical concept in modern digital ecosystems, enabling organizations to monitor and understand the internal state of their systems based on external outputs.&#x20;

Sunbird ED provides observability by acknowledging users' actions in the form of consumption reports, course progress exhausts, and multiple Dashboards. This is enabled by 'Telemetry'.

Observability in Sunbird ED refers to the capability of tracking and understanding user actions and behaviors within the platform. It is achieved through the use of Telemetry, which automatically records and measures statistical data from user interactions. Telemetry collects information about who performed an action, what action was performed, on what object, where the action occurred, and using which tool. This data is then used to analyze user navigation, behavior, and usage patterns, providing insights for decision-making and research outcomes. Sunbird ED's observability features include consumption reports, course progress tracking, and multiple dashboards.

#### <mark style="color:orange;">Telemetry</mark>

Telemetry plays a fundamental role in the observability of systems like Sunbird ED by meticulously capturing and relaying data on user interactions and behaviors back to organizations for analysis. This automated data collection mechanism encompasses recording details of user actions, such as who performed it, the nature of the action, and the context within which it was performed. Through telemetry, Sunbird ED can generate detailed consumption reports, track course progress, and offer comprehensive dashboards, thereby enhancing decision-making and improving user experience. In broader applications, telemetry extends its utility to various fields including space exploration, healthcare, and environmental monitoring, demonstrating its versatility and critical importance in both digital and physical environments.

In today’s connected world, Telemetry is a term used for technologies that automatically record and measure statistical data from real-world use and forward it to IT systems in a remote location for further analysis and study. Telemetry is used in a myriad of industries from tracking spacecraft, medical monitoring, tracking wildlife, and so on.

‘Events’ are broad, human-readable actions that can be tracked as a string. Events are used to categorize telemetry data. They are the basic unit for analytics and help identify user navigation or flow.

The concept of telemetry events is to identify:

**Who** did **what**, **on** **what**, and **where**, **using** **what**, **in relation** to what?

Every event has the following sections and corresponding fields to capture the data:

| Section        | Description              | Attributes                |
| -------------- | ------------------------ | ------------------------- |
| About          | About the event          | ets mid                   |
| Who            | About the actor          | uid                       |
| did            | Verb or action           | eid                       |
| on what        | Action on what object?   | content\_id content\_ver  |
| and where      | Context of the action    | env did sid channel pdata |
| using what     | Using which tool?        | ?                         |
| In relation to | Related to which action? | cdata                     |

### <mark style="color:orange;">Why do we need Telemetry?</mark> <a href="#why-we-need-telemetry" id="why-we-need-telemetry"></a>

* **Continuous Improvement**: Sunbird ED relies on telemetry to continuously improve its educational services, ensuring content and features meet user needs and enhance learning outcomes.
* **User Behavior Insights**: Gathers data on how educators and learners interact with the platform, which features are most used, and how content is consumed, helping tailor the educational experience.
* **Product Development**: Informs the development of new features and services by highlighting user demands and identifying gaps in the current offerings.
* **Security and Compliance**: Enables monitoring for potential security threats and ensures compliance with educational standards and regulations.
* **Performance Monitoring**: Helps in identifying and resolving issues with the platform’s performance, ensuring a smooth and efficient user experience.
* **Informed Decision Making**: Provides a data-driven basis for decision making, from content curation to UI/UX design, significantly influencing the platform's evolution.
* **Customization and Personalization**: Aids in creating a more personalized learning experience by understanding individual and collective learning patterns and preferences.

The objective of telemetry is to assist in product, application, or service development, modification, or security. It works as a framework. Telemetry enables automatic collection of data from real-world, real-time use.

Typically, there are four levels of telemetry:

* Security
* Basic
* Enhanced
* Full

The level of data collected is a discrete decision of an organization or business. Analysis of this data offers insights into product and user behaviour and usage patterns, driving business decisions and research outcomes. You can program your telemetry analytics to suit your requirements.

Sunbird’s telemetry service has Full level telemetry.

### <mark style="color:orange;">How to Configure?</mark>

The above capabilities of Observability are derived from components of Sunbird Lern. You can find details by clicking on the link [here](observability.md)
