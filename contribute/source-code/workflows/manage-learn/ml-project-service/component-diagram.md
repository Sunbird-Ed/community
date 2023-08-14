# Component Diagram





<figure><img src="../../../../../.gitbook/assets/ML Project Service L0 (2).png" alt=""><figcaption></figcaption></figure>

The ML Project Service is constructed upon the framework of Kafka, MongoDB, and cloud storage, ensuring a smooth amalgamation and efficient data control. Moreover, it collaborates seamlessly with vital services like ml-core-service, ml-survey-service, learner services, and Sunbird-RC services. Within the Project service, five crucial modules are incorporated, each catering to distinct facets of project management.

#### Template Module

This module provides APIs for various project template-related operations, facilitating the creation, retrieval and updating of project templates.

#### Template Tasks Module&#x20;

Responsible for managing project task templates, this module handles the operations related to task templates associated with projects.

#### Reports Module

Focused on generating and managing different project reports.\


#### userProjects Module

This module revolves around user project-related operations, encompassing functionalities for creating, modifying, and sharing user-specific projects.



#### Certificate Template

Devoted to managing project certificate-related aspects, this module governs the templates and functionalities associated with project certificates.



These five modules form the backbone of Ml Projects Service, empowering users to extend and optimize project capabilities within the broader SunbirdEd ecosystem on the App platform.\