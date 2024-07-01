# Design Principles

## Thinking Microservice Architecture

Sunbird is built with microservices thinking; it is not a pre-packaged learning management solution. Instead, it is a set of core microservices that have been unbundled from the functionality or the solution inside to provide critical core functionality related to learning, registries, content, attestations, data, etc.

Sunbird contains “microservices” as Lego blocks that can be used by a builder of a platform or solution to compose many solutions rapidly and even rewire them, depending on the context, diversity and needs, rather than rewriting the full technology stack.

#### Unbundling for Diversity

As an architect or a developer downloading Sunbird, there are hundreds of APIs, which are microservices exposed via APIs available for use; these are generalised and micro. Sunbird has unbundled hundreds of microservices in terms of content attestation, data, etc.

An architect or a developer looking at solutions can leverage Sunbird microservices to reimagine solutions to suit their needs and decide what to do with them. It would be possible to compose solutions that are different from those seen in the reference implementation of Sunbird. One can imagine a wide range of use cases as the microservices can be used in many ways.

**Content Microservice** - This includes APIs for content creation or a collection creation, and the concept of the collection is abstracted enough to be able to use it in different contexts, not just k-12 education. The Collection API or collection microservice can be used to create a textbook or a collection of courses. In this case, the concept of a course is nothing but an abstract version of a collection.

This approach opens up the possibility of imagining diverse solutions and large-scale innovation.

#### Loose Coupling for Evolution

Sunbird microservices are not necessarily dependent on each other; one can choose and use any microservice to serve varied needs.

**Registry Microservice** - The Registry microservice can be used for various purposes. It can be used to build a registry of schools, a registry of contributors, or any other registry. This can be done without using anything from the Sunbird content microservice, collections, or other microservices. This decoupling is an integral part of the Sunbird Architecture and composition story because it is built in a decoupled manner. Your ability to reuse parts of it or full of it in any form or fashion gives you combinatorial capability that gives you a lot of possibilities in terms of reimagining solutions to suit different needs and contexts.

#### Observability through Emit vs Extract

Sunbird microservices are built such that every microservice captures every action and interaction on the platform and naturally emits anonymized confidentiality-protecting, privacy-protecting data stream automatically, and accumulated through the Sunbird telemetry infrastructure so that data extraction is avoided.

Extraction is what is done when telemetry is not built natively into the microservice architecture. The only way to get data out of the system is by extracting it from various components and parts of the system. This exercise is time-consuming and inefficient, and most importantly, if the extraction design is not well done, there will be severe privacy and confidentiality implications and unanticipated consequences.

Data and Telemetry microservices: Data and telemetry as a microservice is essential to a platform's building, development and growth. Telemetry is the ability to remotely observe large systems and also the ability of actors in a system to observe smaller actions.

For instance, in the education system, it would be the ability to observe what is happening at a school, a district, and a state level through a set of telemetry feeds coming through the digital platform. The actors at each level - school leaders, education officers, and state administrators- need visibility and often have to extract data to understand what is happening in their network.

Emit vs Extract is an important construct that, even as extenders of Sunbird, developers and architects must ensure that the telemetry and emitting architecture is implemented as part of the microservice, not just as an API.

#### Video on Architecture Principles of Designing Population Scale Digital Infrastructure

To understand the architectural principles of designing population-scale digital infrastructure, listen to Dr Pramod Varma, CTO of EkStep Foundation.

{% embed url="https://youtu.be/1S-599usfjc" %}
