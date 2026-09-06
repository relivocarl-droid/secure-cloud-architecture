# Secure Cloud Architecture Plan

## Architecture

The proposed architecture follows this basic flow:

**Users → CDN → Load Balancer → Application Servers → Private Database**

The purpose of this architecture is to provide a secure and reliable Student Management Application. Public resources are separated from private resources to reduce the risk of unauthorized access.

## CDN

The Content Delivery Network (CDN) delivers cached copies of static website content closer to users. This improves loading speed and reduces traffic going directly to the application servers.

The CDN can be publicly accessible because users need to access the website through the Internet.

## Load Balancer

The load balancer receives incoming requests from users and distributes them across multiple application servers.

It provides a single public entry point to the application and helps improve availability by sending traffic only to healthy application servers.

## Application Servers

Application servers process requests from users and communicate with the database when necessary.

The application servers should be placed in a **private subnet** so that users cannot directly access them from the Internet.

There should be at least two application servers so the application can continue operating if one server fails.

## Database

The database stores student information such as student numbers, names, courses, year levels, and email addresses.

The database should remain **private** and should not be directly accessible from the Internet.

Only authorized application servers should be allowed to connect to the database.

---

# Public and Private Resources

| Resource           | Public or Private? | Explanation                                                                                                       |
| ------------------ | ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| CDN                | Public             | The CDN needs to deliver website content to users through the Internet.                                           |
| Load Balancer      | Public             | The load balancer acts as the public entry point for application traffic.                                         |
| Application Server | Private            | Application servers should not be directly accessible from the Internet.                                          |
| Database           | Private            | The database contains student information and should only accept connections from authorized application servers. |

---

# Security Controls

## IAM

Identity and Access Management (IAM) controls who can access the cloud environment.

Only authorized users should have access to cloud resources. Administrators should have management permissions, while instructors, students, and developers should only receive the permissions necessary for their roles.

Unused accounts and permissions should be removed regularly.

## MFA

Multi-Factor Authentication (MFA) should be enabled for administrator accounts and other accounts with access to sensitive resources.

MFA provides an additional layer of security if a password is stolen or compromised.

## Firewall / Security Group

Firewall and security group rules should only allow necessary connections.

| Connection                         | Status  | Explanation                                                 |
| ---------------------------------- | ------- | ----------------------------------------------------------- |
| Internet → CDN                     | Allowed | Users need to access website content.                       |
| Internet → Load Balancer           | Allowed | The load balancer is the public entry point.                |
| Load Balancer → Application Server | Allowed | Required for application traffic.                           |
| Application Server → Database      | Allowed | Required for database operations.                           |
| Internet → Application Server      | Blocked | Prevents users from directly accessing application servers. |
| Internet → Database                | Blocked | Prevents direct Internet access to student information.     |

## Encryption

Student information should be encrypted both during transmission and while stored.

Encryption protects student information from unauthorized access. Data transmitted between users and the application should use secure connections, while stored database information should also be encrypted.

## Logging

Important activities should be recorded in system logs.

Examples include:

* User login attempts
* Failed login attempts
* Administrator actions
* Changes to IAM permissions
* Database access
* Security configuration changes
* Access to important application resources

Logs can help administrators investigate security incidents and unauthorized activity.

## Monitoring

The system should monitor for suspicious activities such as:

* Repeated failed login attempts
* Unusual administrator activity
* Unexpected database access
* Unusual network traffic
* Unauthorized configuration changes
* Attempts to access blocked resources

Monitoring helps administrators detect potential security problems quickly.

## Backup

The database should have regular backups to prevent permanent data loss.

Backups allow the organization to recover student information after accidental deletion, system failure, data corruption, or a security incident.

Backups should also be protected from unauthorized access.

---

# Principle of Least Privilege

The Principle of Least Privilege means that users should only receive the permissions required to perform their responsibilities.

| User          | Allowed Access                                                                                                                                         |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Administrator | Manage cloud resources, IAM permissions, security settings, application infrastructure, and database administration.                                   |
| Instructor    | View and manage authorized student records relevant to their classes or responsibilities.                                                              |
| Student       | View their own student information and authorized application features.                                                                                |
| Developer     | Develop and maintain the application. Developers should have limited production access and should not automatically receive administrator permissions. |

Administrator access should not be given to everyone because excessive permissions increase the risk of accidental or unauthorized changes.

---

# Shared Responsibility Model

The Shared Responsibility Model divides security responsibilities between the cloud provider and the customer.

| Responsibility        | Cloud Provider or Customer? |
| --------------------- | --------------------------- |
| Physical data center  | Cloud Provider              |
| Physical servers      | Cloud Provider              |
| User accounts         | Customer                    |
| Student data          | Customer                    |
| IAM permissions       | Customer                    |
| Application security  | Customer                    |
| Database access rules | Customer                    |
| Backups               | Customer                    |

## What does Security OF the Cloud mean?

Security **OF the Cloud** means protecting the underlying cloud infrastructure.

The cloud provider is responsible for areas such as physical data centers, physical servers, and the underlying cloud infrastructure.

## What does Security IN the Cloud mean?

Security **IN the Cloud** means protecting the resources and data that the customer uses or deploys in the cloud.

This includes user accounts, student data, IAM permissions, application security, database access rules, encryption, logging, monitoring, and backups.

---

# Architecture Questions

## Which resource should be directly accessible from the Internet?

The CDN and load balancer should be accessible from the Internet because they provide the public entry point for users.

The application servers and database should remain private.

## Why should the database remain private?

The database contains student information. Keeping it private reduces the risk of unauthorized access and protects sensitive data from Internet-based attacks.

## Why should users not connect directly to the database?

Users should not connect directly to the database because this could expose sensitive student information and database credentials.

Users should communicate with the application through the load balancer and application servers.

## What is the purpose of a load balancer?

A load balancer distributes incoming requests across multiple application servers.

It helps improve application performance and availability.

## What happens if one application server fails?

If one application server fails, the load balancer can stop sending traffic to the failed server and direct users to another healthy application server.

This allows the application to continue operating.

## What is the purpose of a CDN?

A CDN delivers cached website content from locations closer to users.

This can improve loading speed and reduce traffic handled directly by the application servers.

## Why should administrator accounts use MFA?

Administrator accounts have powerful permissions. If an administrator password is stolen, an attacker could potentially change security settings or access important resources.

MFA provides an additional layer of protection against unauthorized access.

## Why should administrator access not be given to every employee?

Administrator access gives users powerful permissions over the system.

Giving administrator access to every employee increases the risk of accidental changes, data exposure, and unauthorized activity.

Users should only receive the permissions required for their jobs.

## Why are logging and monitoring important?

Logging records important activities while monitoring helps identify suspicious behavior.

Together, they help administrators detect security incidents, investigate problems, and respond to potential threats.

## Why are backups important?

Backups allow the organization to recover student information after accidental deletion, system failure, data corruption, or a security incident.

Regular backups reduce the risk of permanent data loss.

