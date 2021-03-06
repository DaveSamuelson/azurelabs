---
title: Azure Dev / Test Labs 
description: Implement functional checks in an application that external tools can access through exposed endpoints at regular intervals.
---

<h1> Azure Dev / Test Labs </h1>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdavesamuelson%2Fazurelabs%2Fmaster%2Fscripts%2Flabprovisioning%2Fazuredeploy.json" target="_blank">
<img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/load=https%3A%2F%2Fraw.githubusercontent.com%2Fdavesamuelson%2Fazurelabs%2Fmaster%2Fscripts%2Flabprovisioning%2Fazuredeploy.json" target="_blank">
<img src="http://armviz.io/visualizebutton.png"/>
</a>



   
# Azure Dev Test Labs

Provisions an Azure Dev Test lab with security.
## Context and problem

It's a good practice, and often a business requirement, to monitor web applications and back-end services, to ensure they're available and performing correctly. However, it's more difficult to monitor services running in the cloud than it is to monitor on-premises services. For example, you don't have full control of the hosting environment, and the services typically depend on other services provided by platform vendors and others. 

There are many factors that affect cloud-hosted applications such as network latency, the performance and availability of the underlying compute and storage systems, and the network bandwidth between them. The service can fail entirely or partially due to any of these factors. Therefore, you must verify at regular intervals that the service is performing correctly to ensure the required level of availability, which might be part of your service level agreement (SLA).

## Solution

Implement health monitoring by sending requests to an endpoint on the application. The application should perform the necessary checks, and return an indication of its status. 

A health monitoring check typically combines two factors:

- The checks (if any) performed by the application or service in response to the request to the health verification endpoint. 
- Analysis of the results by the tool or framework that performs the health verification check. 

The response code indicates the status of the application and, optionally, any components or services it uses. The latency or response time check is performed by the monitoring tool or framework. The figure provides an overview of the pattern.

![Overview of the pattern](images/health-endpoint-monitoring-pattern.png)

Other checks that might be carried out by the health monitoring code in the application include:
- Checking cloud storage or a database for availability and response time.
- Checking other resources or services located in the application, or located elsewhere but used by the application.

Services and tools are available that monitor web applications by submitting a request to a configurable set of endpoints, and evaluating the results against a set of configurable rules. It's relatively easy to create a service endpoint whose sole purpose is to perform some functional tests on the system. 

Typical checks that can be performed by the monitoring tools include: 

- Validating the response code. For example, an HTTP response of 200 (OK) indicates that the application responded without error. The monitoring system might also check for other response codes to give more comprehensive results.
- Checking the content of the response to detect errors, even when a 200 (OK) status code is returned. This can detect errors that affect only a section of the returned web page or service response. For example, checking the title of a page or looking for a specific phrase that indicates the correct page was returned.
- Measuring the response time, which indicates a combination of the network latency and the time that the application took to execute the request. An increasing value can indicate an emerging problem with the application or network. 
- Checking resources or services located outside the application, such as a content delivery network used by the application to deliver content from global caches.
- Checking for expiration of SSL certificates.
- Measuring the response time of a DNS lookup for the URL of the application to measure DNS latency and DNS failures.
- Validating the URL returned by the DNS lookup to ensure correct entries. This can help to avoid malicious request redirection through a successful attack on the DNS server.










<!-- TOC -->

- [1. Solution Overview](#1-solution-overview)
- [2. Reference Architecture Solution Template Overview](#2-reference-architecture-solution-template-overview)
- [3. Licenses & Costs](#3-licenses-costs)
- [4. Target Audience](#4-target-audience)
- [5. Prerequisites](#5-prerequisites)
- [6. Reference Architecture Diagram](#6-reference-architecture-diagram)
- [7. Technologies Used in the Solution](#7-technologies-used-in-the-solution)
- [7. Configurations](#7-configurations)
    - [6.2 Deployed Infrastructure](#62-deployed-infrastructure)
- [7. Deployment Steps](#7-deployment-steps)
- [8. Configuration](#8-configuration)
    - [8.1 Configuration Guides](#81-configuration-guides)
- [9. Management & Operations](#9-Management-Operations)
- [10. Support](#10-support)

<!-- /TOC -->

##  1. Solution Overview

> ☛ As this solution is currently going through a forma


An integrated ARM Template (<a href="https://azure.microsoft.com/en-us/documentation/articles/resource-group-overview/">Azure Resource Manager</a>) that stitches all the above technology into a single deployment. The following is a feature table that is pulled together for your benefit.
Customers want

|Features	            |Some Examples from the Solution
|:------                |:------- 
|Resources on-demand    |<ul> <li> Azure Resource Manager based Templatized Solution  </li> </ul>
|DevOps Manageability   |<ul> <li> Infrastructure as code </li>  <li> Bastion Host VM for Releases and other management tasks tat can't be done over DMZ network </li> <li> Operations Management Suite and associated solutions</li>  <li>Runbook Automation </li></ul>
|Solution Scalability   |<ul> <li>Azure PaaS familiarity and Scale </li> <li>Solution can be easily extended for multi-region deployments </li> <li> Each layer can be scaled out appropriately </li> </ul>
|Built-in Security      | <ul> <li> End-point protection using SSL  </li> <li> Network segmentation based on service roles</li> <li> DMZ and firewalls </li> <li>End-to-end encryption</li> <li>Active Directory Role Based Access </li> <li>Database Encryption features (TDE, Client-side encryption, data-masking, connection encryption and many more) </li> <li>Disabling deprecated TLS 1.0 and 1.1 across the board </li> <li> Diagnostics storage Encryption </li>  <li>and many more... </li></ul>
|Conforming to compliance standards from get-go|<ul> <li> PCI DSS 3.2 compliance from the outset.<p/> ☛ Please have your QSA review the conformance to your specific Auditing and Implementation standards </li> </ul>
|Integration            |<ul> <li>Azure Active Directory Integration </li> <li>Standardized Azure native Monitoring </li>  </ul>

##  2. Reference Architecture Solution Template Overview
***Solution Templates*** provide customers with a highly automated process to launch enterprise ready first and 3rd party ISV solution stacks on Azure in a pre-production environment. These fully baked stacks enable customers to quickly stand up a PoC or Piloting environments and also integrate it with their systems and customization.

Customers benefit greatly from solution templates because of the ease with which they can stand up enterprise-grade, fully integrated stacks on Azure. The extensive automation and testing of these solutions will allow them to spin up pre-production environments with minimal manual steps and customization.  Most importantly, customers now have the confidence to transition the solution into a fully production-ready environment with confidence.

Per Gartner, 
> ### ⚠ Through 2020, 95 percent of cloud security failures will be the customer's fault
> - Gartner Predictions for 2016 and Beyond.  http://www.gartner.com/newsroom/id/3143718

even through the platform vendors (like Microsoft Azure) are compliant, a customer might not know how to build and manage their applications at scale. Through this solution, our attempt is to simplify the quick deployment of infrastructure.
Here's the Gartner's reference




**Disclaimer:**
> This solution is intended as a pilot and is not production ready.
> Please contact  **<a href="mailto:azurecompliance@avyanconsulting.com" target="_blank">azurepcisamples@avyanconsulting.com</a>** if you need further info or support on this QuickStart solution.


This template is currently going through a review with Microsoft's security and compliance team and post review will be updated with changes.


##  3. Licenses & Costs
In its current state, solution templates come with licenses built-in – there may be a BYOL option included in the future. The solution template will be deployed in the Customer’s Azure subscription, and the Customer will incur Azure usage charges associated with running the solution stack.
The only component that requires Azure Marketplace purchase is Tinfoil Web Vulnerability Assessment. 
We have kept the template disabled in the solution. Please follow instructions in the deployment guide to purchase and enable Tinfoil subscription.

##  4. Target Audience
The target audience for these solution templates are 
* **Business Decision Maker, IT Data Analyst** - or anybody w/i the organization who cares for the managing risk on Business transactions
* **IT Decision Maker & Infrastructure Architects** - or any personnel w/i the organization that's responsible for managing Infrastructure risk
* **IT Decision Maker & Infrastructure Architects** - or any personnel w/i the organization that's responsible for DevOps/IT Configuration management
*  and lastly, but very importantly - **IT professionals** who need to stand-up and/or deploy infrastructure stacks.

##  5. Prerequisites
* Azure Subscription
* Azure user account with AD Global Admin Role on the tenant.
 

## 6. Reference Architecture Diagram
![[] (images/Azure_PaaS_-_PCI_DSS_Reference_Architecture.png)](images/Azure_PaaS_-_PCI_DSS_Reference_Architecture.png)


The diagram above provides the overall deployment architecture for this test drive.
As a part of deployment the template launches the following:

## 7. Technologies Used in the Solution
![[] (images/Technologies_Used.png)](images/Technologies_Used.png)

## 7. Configurations 
Refer to the configuration details in the clickable slidedeck [ Azure PCI PaaS Management Reference Architecture.pptx](documents/Azure_PCI_PaaS_Management_Reference_Architecture.pptx)


![[] (images/Configurations_Summary.png)](images/Configurations_Summary.png)

### 6.2 Deployed Infrastructure

|Resources	        |Description
|------             |-------        
|Web Application    |The <a href="https://azure.microsoft.com/en-us/services/app-service/web/" target="_blank">Web Apps </a>feature in Azure App Service lets developers rapidly build, deploy, and manage powerful websites and web apps. Build standards-based web apps and APIs using .NET, Node.js, PHP, Python, and Java. Deliver both web and mobile apps for employees or customers using a single back end. Securely deliver APIs that enable additional apps and devices
|Azure App Service      |With <a href="https://azure.microsoft.com/en-us/services/app-service/?b=16.52" target="_blank">App Service</a>, Develop powerful applications for any platform or device, faster than ever before. Meet rigorous performance, scalability, security, and compliance requirements using a single back-end.
|Role Based Access Control | Azure <a href="https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-configure" target="_blank">Role-Based Access Control</a> (RBAC) enables fine-grained access management for Azure. Using RBAC, you can grant only the amount of access that users need to perform their jobs. This article helps you get up and running with RBAC in the Azure portal. If you want more details about how RBAC helps you manage access, see What is Role-Based Access Control.
|Azure Active Directory |<a href="https://azure.microsoft.com/en-us/services/active-directory/" target="_blank">Azure Active Directory</a> (Azure AD) is Microsoft’s multi-tenant cloud based directory and identity management service.
|Application Gateway   |<a href="https://azure.microsoft.com/en-us/services/application-gateway/" target="_blank">Azure Application Gateway</a> provides application-level routing and load balancing services that let you build a scalable and highly-available web front end in Azure. You control the size of the gateway and can scale your deployment based on your needs
|Azure DNS      |With <a href="https://azure.microsoft.com/en-us/services/dns/" target="_blank">Azure DNS</a>, you can host your DNS domains in Azure. Manage your DNS records using the same credentials and billing and support contract as your other Azure services. Seamlessly integrate Azure-based services with corresponding DNS updates, streamlining the end-to-end deployment process.
|Virtual Network    |Azure <a href="https://azure.microsoft.com/en-us/services/virtual-network/" target="_blank">Virtual Network</a> provides an isolated and secure environment to run your virtual machines and applications. You can use your private IP addresses and define subnets, access control policies, and more. With Virtual Networks, you can treat Azure just as you would your own datacenter.
|Azure Storage      |<a href="https://azure.microsoft.com/en-us/services/storage/" target="_blank">Azure Storage</a> is the cloud storage solution for modern applications that rely on durability, availability, and scalability to meet the needs of their customers.
|Virtual Machine    |Azure <a href="https://azure.microsoft.com/en-us/services/virtual-machines/?b=16.51a" target="_blank">Virtual Machines (VM)</a> is one of several types of on-demand, scalable computing resources that Azure offers. Typically, you choose a VM when you need more control over the computing environment than the other choices offer
|SQL Database       |<a href="https://azure.microsoft.com/en-us/services/sql-database/?b=16.50" target="_blank">SQL Database</a> is a relational database service in the Microsoft cloud based on the market-leading Microsoft SQL Server engine and capable of handling mission-critical workloads. SQL Database delivers predictable performance at multiple service levels, dynamic scalability with no downtime, built-in business continuity, and data protection — all with near-zero administration
|App Service Environment    |An <a href="https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-intro" target="_blank">App Service Environment</a> is a Premium service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including Web Apps, Mobile Apps, and API Apps.
|Application Insights   |Gain <a href="https://azure.microsoft.com/en-us/services/application-insights/" target="_blank">actionable insights</a> through application performance management and instant analytics
|Log Analytics      |<a href="https://azure.microsoft.com/en-us/services/log-analytics/" target="_blank">Log Analytics</a> is a service in Operations Management Suite (OMS) that helps you collect and analyze data generated by resources in your cloud and on-premises environments.
|OMS Solutions      |7 OMS Solutions <ol> <li>Activity Log Analytics</li> <li>Azure Networking Analytics</li>  <li>Azure SQL Analytics</li> <li>Change Tracking</li> <li>Key Vault Analytics</li> <li>Service Map</li> <li>Security and Audit </li> </ol>
|Key Vault      |Azure <a href="https://azure.microsoft.com/en-us/services/key-vault/" target="_blank">Key Vault</a> helps safeguard cryptographic keys and secrets used by cloud applications and services. By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs)
|Azure Security Center      |With <a href="https://azure.microsoft.com/en-us/services/security-center/" target="_blank">Azure Security Center</a>, you get a central view of the security state of all of your Azure resources. At a glance, verify that the appropriate security controls are in place and configured correctly. And quickly identify any resources that require attention.
|Web Apps Vulnerability Assessment via Tinfoil  |For Azure Web Apps, <a href="https://azure.microsoft.com/en-us/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/" target="_blank">Tinfoil Security</a> is the only security vulnerability scanning option built into the Azure App Service management experience.
|Antimalware extionsion for VMs     |<a href="https://docs.microsoft.com/en-us/azure/security/azure-security-antimalware" target="_blank">Microsoft Antimalware</a> for Azure Cloud Services and Virtual Machines is free real-time protection capability that helps identify and remove viruses, spyware, and other malicious software, with configurable alerts when known malicious or unwanted software attempts to install itself or run on your Azure systems.
|Custom Domain SSL Certificates | Https traffic enabled using <a href="https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-configure-ssl-certificate" target="_blank">custom domain SSL certificate</a>

**Note**:


##  7. Deployment Steps
Please refer to the [this deployment guide](documents/DeploymentGuide.docx) for the detailed instructions on deploying this template successfully.
You can click the "deploy to Azure" button at the beginning of this document or follow the instructions for command line deployment using the scripts in the root of this repo.

***Please refer to parameter descriptions if you need more information on what needs to be provided as an input.***
The deployment takes about approximately 45mins. Once it is deployed there are few minor manual steps to 

Deployment Parallalization is acheived through ARM templates dependencies pipeline.
An example deployment timeline is depicted here

<nbsp/><nbsp/> ![[] (images/ARM_template_deployment_timeline.png)](images/ARM_template_deployment_timeline.png)


## 8. Configuration
### 8.1 Configuration Guides

You can use [this detailed guide](documents/DeploymentGuide.docx) to configure the components in the solution.

## 9. Management & Operations
**Operations Dashboard**

<nbsp/><nbsp/> ![[] (images/OMS_Workspace_and_Solutions.png)](images/OMS_Workspace_and_Solutions.png)

**SSL Verification**

<nbsp/><nbsp/> ![[] (images/SSL_Gateway.png)](images/SSL_Gateway.png)

## 10. Support
For any support-related issues or questions, please contact us for assistance.





<h3>NOTE</h3>
If you are creating templates that fail to Visualise, this usually indicates invalid JSON - try validating in http://jsonlint.com/











