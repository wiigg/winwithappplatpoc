# Humongous Healthcare -- Win with App Platform
This repository shows one potential solution for the following case study.

## Instructions

Follow the steps in the [Before the Hands-On Lab](Before%20the%20Hands-On%20Lab.md) guide first to configure your Azure environment.  Then, follow the steps in the [Hands-On Lab](Hands-On%20Lab.md) guide to create one potential solution for the following case study.

The Hands-On Lab guide contains a shortened version of the case study, but the full version is available below for reference.

## Case Study

**Humongous Healthcare** is a global network of healthcare providers with presence throughout the industry.  Humongous Healthcare wishes to drive a new Health Checks initiative, which specifically entails building a suite of health check applications for its 7,500 combined direct and partner network employees worldwide to use.  These applications will allow users to submit information on their current health status and submit a questionnaire concerning any medical symptoms they might have experienced over the past 14 days.  Employees would enter this information before leaving for work each day, allowing Humongous to track potential employee health issues over time.

Molly Fischer, the Chief Technical Officer (CTO) and Vice President of Engineering at Humongous Healthcare, wants to use cloud services for their Health Checks initiative, thereby freeing Humongous Healthcare from any physical requirements for on-premises hardware.  Humongous already uses a variety of Microsoft Azure services, taking advantage of both Infrastructure-as-a-Service and Platform-as-a-Service offerings.  Their software engineers and infrastructure team have a good working familiarity with Azure services and wish to use this opportunity to develop an innovative product which can serve as a guide for future modernization of their existing applications and infrastructure.

The Engineering team at Humongous Healthcare wants a modern, innovative application platform, but this is not the only key group which will be involved.  Antonio de la Cruz, Vice President of Product Management, made clear that business analysts will be responsible for creating the business logic and user experience for most of the Health Checks applications (with the assistance of an outside consulting group).  These applications should be able to access API endpoints which the Engineering team plan to build.

Humongous architects have sketched out a high-level overview of their ideal API, but there is some disagreement within the team around whether the techniques they should use for endpoint design and access.  One architect believes that a HTTP-based REST API, using classic endpoints like GET and POST, would be best because Humongous engineers have a fair amount of experience working with .NET MVC and Web API applications.  A second architect would prefer a GraphQL approach, arguing that it is a more modern and flexible take on API design.  Their third architect is indifferent between the two approaches but strongly prefers using the Command and Query Responsibility Separation (CQRS) pattern for any API design.  The three architects have all agreed that, because they are not as familiar as they would like to be with Azure services, they will put a great deal of weight on Microsoft's advice.  They're all confident that their software engineers could handle either REST or GraphQL, but want to learn about best practices, as well as understand what works best in Azure.

Humongous would like to manage one API for accessing the back end of all these health applications. In practice, Humongous expects something on the order of 15 to 20 endpoints to support the breadth of their health check application suite, but for the purposes of a proof of concept, they would like to have two endpoints implemented:  one which submits information on current health status and one which retrieves submissions for the registered user.  The key data points Humongous would like to have in this proof-of-concept are as follows:

- Submission ID, generated by the system.
- Patient ID, handled as part of a future authentication process.  For the proof of concept, it would be okay for the end application to hard-code the patient ID.
- Date and time of submission.
- Current health status (one of "I feel well" or "I feel unwell").
- A list of symptoms over the past 14 days, where each symptom is a free-form text entry with no validation.

When retrieving submissions for a registered user, they would like the ability to retrieve all submissions for the logged-in user or pass in a submission ID to retrieve details solely on that particular submission.  Humongous Engineering plans to expand these requirements in their full product implementation, such as extending the data model and implementing lookup lists and checks on symptoms.  For a proof of concept, however, they do not want to complicate things unnecessarily.

The expectation is that Humongous software engineers will implement all API endpoints for the Health Checks initiative (beyond what you will create for the proof of concept), and multiple, independent teams may implement different endpoints over time.  Both Molly and the architects would like this system to be as simple to manage as possible. While there is an Operations team in the Engineering department, that group tends to be overwhelmed with existing tasks and they have very limited time available to manage new software solutions.  Ideally, the software engineers should be able to instrument, monitor, and manage these endpoints themselves, but Humongous Healthcare does not have a great DevOps culture today.  They are moving in that direction, but would appreciate any tooling, processes, or product selections which could make the process of instrumentation, monitoring, and management easier for their software engineers.

Although Antonio's team will work with partners do much of the front-end application work, Molly does not want this to become a "shadow IT" initiative.  She would like, as much as possible, to have Antonio's team working in a single, collaborative environment, where her Engineering department can review application security, ensure that everything is configured properly, and manage costs most efficiently.  They are very concerned with security breaches based on misconfiguration.  As Antonio put it, "I don't want one of my people to check the wrong box and suddenly we have governments fining us due to regulatory violations."

Molly and the Engineering team also wish to have all data stored in a single database, as this will simplify security and open opportunities for their data scientists to analyze the data most efficiently.  In addition, they would like to centralize management of any access points to the data.  Different Engineering teams will work on separate API endpoints and Molly is interested in anything which can improve the coordination between teams and make their architecture group's lives easier.  Molly strongly prefers centralized solutions, and she does have a concern around the overlapping capabilities in Azure services.  She does not want to spend the time combining a lot of applications to get to Humongous's desired solution, so the fewer the number of working parts, the better it is in her mind.

As far as data storage is concerned, the architects focused on the need for flexible data structures.  The reason for this is that individual providers in their network often have differing requirements on what data they collect, depending on their specialization.  Antonio provided as one example that all providers in the network will be able to generate admission, transfer, and discharge records based on a common HL7 format.  Beyond that, however, the data elements collected for outpatient treatment facility for a minor surgical procedure might differ considerably from 23-hour observation in a behavioral health treatment facility. The questionnaires which end users fill out will likely differ based on facility, mode of treatment, nation, and region.  Antonio also mentioned that these questionnaires may change over time to support additional testing options, such as asking end users a subset of the questions sometimes or adding and removing questions from the survey applications.  Antonio is not sure just how often these changes will occur but mentioned tha Humongous Healthcare's clinical research staff is excited to have that potential capability.

Following up from Antonio's point, Molly reiterated that any solution should have the capability to analyze large-scale data later, as Humongous Healthcare data scientists and the clinical research staff are hoping to perform longitudinal studies of end user symptoms over an extended period to test the efficacy of various treatment regimes.  Their data scientists have medical records information, but that information is limited to a subset of end users who were admitted for treatment and the opportunity to analyze data on symptoms treated outside of a health care facility is of great interest to them.

Another consideration that Molly would like to keep in mind is that Engineering has relied on their Jenkins-based Continuous Integration and Continuous Deployment (CI/CD) pipelines for code development and deployment on-premises and into virtual machines hosted on Azure.  This works well for their existing code bases, but they are interested in learning how to use Azure DevOps or GitHub Actions, taking the knowledge they have earned over time and applying it to these new technologies.  The concern Molly expressed, however, is that Microsoft seems to be giving ambiguous and contradictory advice on which platform teams like hers should use and would like clarity on what the right answer is.

All stakeholders agree that any health check applications must ensure compliance with appropriate regulatory authorities and follow any regulations for Personally Identifiable Information (PII) or Protected Health Information (PHI).  To this end, security is paramount:  they need a solution which provides a consistent security model across all components and can ensure that customer data is kept in a secure manner, as well as one which keeps compliance with data privacy regimes--such as the General Data Protection Regulation (GDPR) or California Consumer Privacy Act (CCPA)--in mind.

In addition to these compliance and regulatory requirements, the security team is concerned about the possibility of denial of service (DoS) or distributed denial of service attacks (DDoS), as these applications will be accessible to mobile and desktop devices without tunneling through a VPN.  Before they can sign off on a potential solution, they need to know that it can successfully handle DoS or DDoS attacks.  One idea they have is to limit the number of calls for a single user to no more than ten over a five-minute interval.  They also want to use their own certificates and keys whenever possible.
