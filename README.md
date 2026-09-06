# Secure Cloud Architecture

## Student Information

**Name:** Carl Roy Relivo
**Section:** CCIS 7E
**Course:** BSIT
**Date:** September 6, 2026

## Project Description

This activity demonstrates a proposed secure cloud architecture for a Student Management Application.

The application allows users to view student information while applying basic cloud networking and security principles.

The proposed architecture separates public and private resources to help protect student information and improve application availability.

## Architecture

**Users → CDN → Load Balancer → Application Servers → Private Database**

### Architecture Components

* **Users** – Access the Student Management Application.
* **CDN** – Delivers cached website content closer to users.
* **Load Balancer** – Distributes incoming requests across application servers.
* **Application Servers** – Process application requests and are placed in private subnets.
* **Private Database** – Stores student information and is not directly accessible from the Internet.

## Public and Private Resources

| Resource           | Access  |
| ------------------ | ------- |
| CDN                | Public  |
| Load Balancer      | Public  |
| Application Server | Private |
| Database           | Private |

## Security Controls

The proposed architecture uses the following security controls:

* **IAM** – Controls who can access cloud resources.
* **MFA** – Adds an additional authentication factor, especially for administrators.
* **Firewall / Security Groups** – Controls which network connections are allowed.
* **Private Subnets** – Prevents application servers and the database from being directly accessed from the Internet.
* **Encryption** – Protects student information while stored and transmitted.
* **Logging** – Records important system and user activities.
* **Monitoring** – Detects suspicious activities and security events.
* **Backups** – Allows student information to be recovered after data loss or system failure.

## Principle of Least Privilege

Each user is given only the permissions necessary to perform their responsibilities.

* **Administrator** – Manages cloud resources, security settings, and user permissions.
* **Instructor** – Can access authorized student records.
* **Student** – Can access their own student information.
* **Developer** – Can develop and maintain the application with limited production access.

## Shared Responsibility Model

The **cloud provider** is responsible for security **OF the cloud**, including physical data centers, physical servers, and the underlying cloud infrastructure.

The **customer** is responsible for security **IN the cloud**, including user accounts, student data, IAM permissions, application security, database access rules, and security configurations.

## Repository Structure

```text
secure-cloud-architecture/
│
├── index.html
├── README.md
└── security-plan.md
```

## Project Goal

The goal of this project is to demonstrate an understanding of:

* Basic cloud networking
* Public and private cloud resources
* Cloud security controls
* Principle of Least Privilege
* Shared Responsibility Model
* Secure application architecture
