# Table of Contents
1. [Overlaps](#overlaps)
1. [Abbreviations and common expressions](#abbreviations-and-common-expressions)
    1. [Executive titles](#executive-titles)
1. [Partner companies](#partner-companies)
    1. [Centra](#centra)
    1. [Voyado](#voyado)
    1. [klaviyo](#klaviyo)
    1. [Rule](#rule)
    1. [Triggerbee](#triggerbee)
    1. [Grebban](#grebban)
    1. [Panagora](#panagora)
1. [Common problems and solutions](#common-problems-and-solutions)
    1. [Currency rates](#currency-rates)
    1. [Creating new platform](#creating-new-platform)
    1. [To access ib-kube:](#to-access-ib-kube)
        1. [Windows](#windows)
1. [ib platform on windows through wsl](#ib-platform-on-windows-through-wsl)
    1. [Setup IB-platform on Windows through WSL 2](#setup-ib-platform-on-windows-through-wsl-2)
1. [ib platform on windows through wsl](#ib-platform-on-windows-through-wsl)
    1. [Intro](#intro)
    1. [Setup Windows](#setup-windows)
        1. [VS code  ](#vs-code)
        1. [Ubuntu Subsystem](#ubuntu-subsystem)
        1. [Docker](#docker)
    1. [Setup in WSL](#setup-in-wsl)
        1. [Clone Repository](#clone-repository)
    1. [Clickhouse](#clickhouse)
    1. [Yarn](#yarn)
    1. [vGPU](#vgpu)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Overlaps

[*Back to top*](#table-of-contents)

# Abbreviations and common expressions
* API  
An application programming interface is a connection between computers or between computer programs. It is a type of software interface, offering a service to other pieces of software.
* CRM  
Customer Relationship Management (CRM) is a strategy that companies use to manage interactions with customers and potential customers. CRM helps organisations streamline processes, build customer relationships, increase sales, improve customer service, and increase profitability.* ERP system
* Cold Calling  
Cold calling is a technique in which a salesperson contacts individuals who have not previously expressed interest in the offered products or services. Cold calling typically refers to solicitation by phone or telemarketing, but can also involve in-person visits, such as with door-to-door salespeople.
* POC  
Proof of concept (POC)
* MRR  
Monthly Recurrent Revenue (MRR)
* Ad-hoc  
Something ad hoc is put together on the fly for one narrow, pressing, or special purpose.
* BI  
Business intelligence (BI) comprises the strategies and technologies used by enterprises for the data analysis and management of business information.
* B2B - Business-to-business
* B2C - business-to-consumer
* D2C - Direct to consumer
* EAN - European Article Number, no longer officially used as GTIN has replaced it, enabling the standard globally.
* GTIN - Global Trade Item Number and is a GS1 number used to give products and packaging a globally unique identity. The number identifies products ...
* LTV (Lifetime Value) is an estimate of the average revenue that a customer will generate throughout their lifespan as a customer.
* CLV - Customer Lifetime Value
* Cohort analysis - an analytical technique that categorizes and divides data into groups with common characteristics prior to analysis.
* Customer segments  
Customer segmentation is the process by which you divide your customers up based on common characteristics
* OKR (“objectives and key results”) are a goal setting methodology that can help teams set measurable goals.
* AOV - Average order value (AOV) tracks the average dollar amount spent each time a customer places an order.
* Churn Analysis is the evaluation of a company's customer loss rate in order to reduce it. Also referred to as customer attrition rate, churn can be minimized by assessing your product and how people use it.

* RFM Analysis - “RFM” stands for recency, frequency and monetary value. RFM analysis is a way to use data based on existing customer behavior to predict how a new customer is likely to act in the future. An RFM model is built using three key factors:
how recently a customer has transacted with a brand
how frequently they’ve engaged with a brand
how much money they’ve spent on a brand’s products and services
* Price sensitivity  
Price sensitivity is the degree to which demand changes when the cost of a product or service changes.
* Basket Analysis  
Market basket analysis is a data mining technique used by retailers to increase sales by better understanding customer purchasing patterns. It involves analyzing large data sets, such as purchase history, to reveal product groupings, as well as products that are likely to be purchased together.
* VAT (moms)  
A value-added tax (VAT), known in some countries as a goods and services tax
I sverige moms (ofta 25%)
* COGS  
Cost of goods sold (COGS) refers to the direct costs of producing the goods sold by a company. This amount includes the cost of the materials and labor directly used to create the good. It excludes indirect expenses, such as distribution costs and sales force costs.
* SKU  
A stock-keeping unit (SKU) is a scannable bar code, most often seen printed on product labels in a retail store. The label allows vendors to automatically track the movement of inventory. The SKU is composed of an alphanumeric combination of eight-or-so characters.
* GTIN

* Agg / Aggregation
* Embedding
* Query
* GDPR - general data regulation protection.

[*Back to top*](#table-of-contents)

## Executive titles

*alphabetical (CEO on top)*

* CEO - Chief Executive Officer (VD) | Responsible for the overall success of a business entity or other organization and for making top-level managerial decisions.
* CCO - Chief Commercial Officer | Responsible for the commercial strategy and the development of an organization. It typically involves activities relating to marketing, sales, product development and customer service.
* CFO - Chief Financial Officer | Responsibile for managing the company's finances, including financial planning, management of financial risks, record-keeping, and financial reporting.
* CIO - Chief Information Officer | Responsible for the management, implementation, and usability of information and computer technologies.
* CPO - Chief Product Officer | Responsible for various product-related activities in an organization. They focus on bringing the product strategy to align with the business strategy and to deploy that throughout the organization.
* CTO - Chief Technical Officer | Responsible for developing, implementing, managing and evaluating the company's technology resources.
* CXO - Chief Experience Officer | Responsible for a company's overall experience and interactions with customers. They help the company drive the entire CX, from products to services, end-to-end.

[*Back to top*](#table-of-contents)

# Partner companies

[*Back to top*](#table-of-contents)

## Centra
info

[*Back to top*](#table-of-contents)

## Voyado
info

[*Back to top*](#table-of-contents)

## klaviyo
info

[*Back to top*](#table-of-contents)

## Rule
info

[*Back to top*](#table-of-contents)

## Triggerbee
info

[*Back to top*](#table-of-contents)

## Grebban
ecomm agency. designed our platform fall 2021. project is not implemented and used in production yet. 

[*Back to top*](#table-of-contents)

## Panagora
info

[*Back to top*](#table-of-contents)

# Common problems and solutions

[*Back to top*](#table-of-contents)

## Currency rates
The `Concat` row we use as an identifier to match the date an interaction was made in order to get a valid currency rate conversion. 

Steps:  
1. Create a new source called currency_rates with “currency_tag” as id, now paste the query provided further down under “Query” 
2. Modify the url in the query to gather the currencies found in the dataset you’re working with (Remove/add for example EUR, NOK)
3. The `target` should be edited to match the most common currency. For example a Swedish small local business should have SEK as target, and a Norwegian company should have NOK as target.  
4. The `from_date` is changed to match the first transaction in the dataset the customer has. To do this, go to the source where you want to add currency rates (for example model - interactions), create a new query and make the same connection as query 1, in the new query, paste: SELECT MIN(ts) AS min_ts FROM import file, picture below for reference! Copy this timestamp, go to a unixtimestamp converted and check what date this is, and edit the `from_date`. DO NOT SAVE THE NEW QUERY
5. At the end of the query you want to add currency rates to, add the following row: 
LEFT JOIN `currency_rates` AS cr on cr.currency_tag = step1.currency_tag

<img width="629" alt="image" src="https://user-images.githubusercontent.com/102239423/163122069-c5faa8d9-b228-447f-8a88-e0ba10e0d6b9.png">

This results in the following: 

<img width="632" alt="image" src="https://user-images.githubusercontent.com/102239423/163122129-5c76dc7a-4d0e-40c6-9c4a-7a07fe2021cd.png">

Query:
```
SELECT 

    concat(`date`, currency) AS currency_tag,
    `date` AS `date`,
    currency AS currency,
    conv_date AS conv_date,
    conv AS conv
```

[*Back to top*](#table-of-contents)

## Creating new platform
- [ ] Open ib-kube repo
- [ ] Check customer’s domain name, match platform name with theirs
- [ ] Create new file in pkg/settings/k8s with name platformname.go
- [ ] Paste content from another platform with recent build
- [ ] Redefine:  
  - [ ] Var name to platform name  
  - [ ] Name:
  - [ ] Subdomain:
  - [ ] Check available ingress (max 15)
  - [ ] Ingress: to available ingress

- [ ] Follow ingress definition (Ctrl click Ingress variable)
- [ ] Copy ingress IP (used for dns record) (skicka IP till christian)
- [ ] Add/remove Args for centra or other integrations
- [ ] Verify tag (commit version)
- [ ] Adjust cpu limit and memory parameters if needed
- [ ] Save File

- [ ] Open pkg/setting/k8s/k8s.go
- [ ] Add variable for platform data to Platforms variable by appending to list
- [ ] Save File

- [ ] Open terminal  in VS code and run git pull
- [ ] Then run make yaml (ignore errors)

- [ ] Go to Source Control
- [ ] Commit your changes with message (e.g. “created platform _NAME_ on _COMMIT VERSION_”
- [ ] Push to repo

- [ ] [Request someone to] run “make k8s” 
- [ ] [Request someone to] add the DNS registry
- [ ] [Request someone to] add to k8s ml registry

[*Back to top*](#table-of-contents)

## To access ib-kube:

[*Back to top*](#table-of-contents)

### Windows
  * Install WSL 2  
    * https://pureinfotech.com/install-windows-subsystem-linux-2-windows-10/  
    * https://code.visualstudio.com/blogs/2019/09/03/wsl2  
  * Boot Ubuntu  
  * Install VS Code  
  * Git clone ib-kube  
  * Cd ib-kube  
  * Run command ``code .``  
  * Done  

[*Back to top*](#table-of-contents)

# ib platform on windows through wsl

[*Back to top*](#table-of-contents)

## Setup IB-platform on Windows through WSL 2

Intro  
Setup Windows  
VS code  
Ubuntu Subsystem  
Docker  
Clickhouse  
Yarn  
vGPU  

[*Back to top*](#table-of-contents)

# ib platform on windows through wsl

[*Back to top*](#table-of-contents)

## Intro
In short, Windows can run the InfoBaleen platform in a Linux subsystem and open it using a Linux browser, just as a normal application within Windows itself. This document summarizes the steps needed as of November 2021.

[*Back to top*](#table-of-contents)

## Setup Windows

[*Back to top*](#table-of-contents)

### VS code  
The preferred editor for this is Microsoft’s Visual Studio Code. It provides cross platform functionality so that we can edit code in the Linux environment (or any other remote machine) directly from Windows. It can be downloaded here:  

	https://code.visualstudio.com/  

In the process, you can check the boxes for adding VS Code to the file context menu and folder context menu. This lets you open a file or directory in VS Code by right clicking it in explorer.

[*Back to top*](#table-of-contents)

### Ubuntu Subsystem
Open Microsoft Store and search for Ubuntu. Install the latest LTS (Long Term Support), at the moment of writing 20.04, and run it. 

[*Back to top*](#table-of-contents)

### Docker
The Docker client has support for Linux subsystems in Windows. Open the link and follow the **Download** and the **Install** instructions.   

	https://docs.docker.com/desktop/windows/wsl/   

[*Back to top*](#table-of-contents)

## Setup in WSL

[*Back to top*](#table-of-contents)

### Clone Repository
Launch Ubuntu and navigate to where you want to place the cloned directory (ls to view directory, cd to change directory, mkdir to create new directory). Clone the repository by:
```
	git clone git@bitbucket.org:infobaleen/ib-platform.git
```

If you have permission issues, contact a colleague for assistance. 

[*Back to top*](#table-of-contents)

## Clickhouse

[*Back to top*](#table-of-contents)

## Yarn

[*Back to top*](#table-of-contents)

## vGPU

[*Back to top*](#table-of-contents)
