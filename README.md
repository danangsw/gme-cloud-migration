## gme-cloud-migration

# Galactus Manufacturing Enterprise: Cloud Migration

This cloud migration strategy is submitted for a fictional company which named Galactus Manufacturing Enterprise (GME). This document covers steps of cloud migration around on-premise infrastructure, application and database migration. As well as detail designing of a high level architecture that bring together all the guidelines and decisions around fault tolerance, high availability and disaster recovery, security as well as an agile application development lifecycle using CI/CD tools that emphasize automation.

## Assumptions

This article uses Microsoft Azure cloud services with all the advantages that the cloud provides in terms of speed and flexibility, minimized costs, performance, and reliability. Azure also provides a comprehensive solution for the cloud adoption barriers. For example, using Azure cloud resources like Azure Backup to protect on-premise resources, or using Azure Analytics to gain insights into on-premise workloads.

This scenario demonstrates how Azure solutions provide the end-to-end cloud migration strategy comperehensively for Galactus Manufacturing Enterprise (GME).

The GME team has make complete list of what the business want to achieve with this migration, migration goals as well as on-premise deployment list.

### Business motivations

- **Address business growth**. GME is growing, causing extra pressure on on-premise workloads and infrastructure.
- **Increase efficiency**. GME needs to remove unnecessary procedures, and streamlines process for developers and users (operations). The business needs IT to be fast and not waste time and money, thus delivering faster on customer requirements.
- **Increase agility**. GTE IT team needs to more responsive to the needs of business. It must be able to react faster than the changes in the market, to enable the success in a global economy. It mustn't get in the way, or become a business blocker.
- **Scale**. As the business grows successfully, the IT team must provide systems that are able to grow at the same pace.
- **Improve cost models**. GTE wants to lessen capital requirements in the IT budget. GME wants to use cloud abilities to scale and reduce the need of expensive hardware.
- **Lower licensing cost**. GTE wants to minimize cloud costs.

### Migration requirements

- **Move to cloud quickly**. Start moving to cloud as quickly as possible.
- **Compile a full inventory**. Complete inventory of all applications, databases and VMs.
- **Assess and classify apps**. Fully take advantage of the cloud. With assumption that all apps or services will run as PaaS. IaaS will be used when PaaS is not appropriate.
- **Train and move to DevOps**. Move to DevOps model. Provide training and reorganize the teams as necessary.

### Current deployments

| Items | Volumes   | Details   |
|-------|-----------|-----------|
| **Workloads** | More than 3,000 apps    | Apps run on VMs. Apps are Windows-based, SQL-based, and OSS LAMP-based |
| **Databases** | Around 8,000   | Databases include SQL Server, MySQL and PostgreSQL |
| **VMs** |  More than 35,000   | VMs run VMware hosts and managed by VCenter servers.  |

## Migration process

Let's determine a four-phases approach for the migration process:

- **Phase 1: Assess.** Discover the current assets, and figure out whether they are suitable for migration to cloud.
- **Phase 2: Migrate.** Move the assets to cloud. How they move apps and objects to cloud will depend on the app and what they want to achieve.
- **Phase 3: Optimize.** After moving to cloud, improving and streamline the resources for maximum performancy and efficiency.
- **Phase 4: Secure and manage.** Using cloud security and management resources and services to govern, secure, and monitor its cloud app in the cloud.

The stage of the assesment and migration process will be different across the organization. For best pratices, optimization and security/management will be ongoing over time.

## Phase 1: Assess

Starting the assess process by discovering and assessing on-premises apps, data, and infrastructure. 

### Inventory discovery

- Discovering apps, maps depedencies accross apps, and decide on migration order on priority.
- As the assess process, it will build out a comprehensive inventory of apps and resources. Along with the new inventory, use and update the existing Configuration Management Database (CMDB) and Service Catalog.
    - The CMDB holds technical configuration for the assessed apps.
    - The Service Catalog documents the operational details of apps, including associated business partners and Service Level Agreements (SLAs).

### Discover apps

GME runs a thousands of apps across a range of servers. In addition to the CMDB and Service Catalog, GME needs discovery and assessment tools.

- The tools must provide a mechanism that can be feed assessment data into the migration process.
- The tools must provide data that help build up an intelligent inventory of physical assets and virrual resources. Data should include profile information, and metric perfomance.
- This complete inventory of assets and assosiated metadata will be used to define mugration plan.

### Identify classifications

The common categories to classify assets in the inventory.

| Category  | Assigned value    | Details           |
|-----------|-------------------|-------------------|
| Business group    | List of business group names  | Which business group is responsible for the inventory item?   |
| POC candidate     | Yes/No                        | Can the app be used as a POC or early adopter for the cloud migration |
| Technial dept     | None/Some/Severe              | Is the inventory item running or using an out-of-support product, platform or operating system    |
| Firewall implications | Yes/No                    | Does the app communicate with internet or outside traffic? Does it integrate with a firewall? |
| Security issues   | Yes/No                        | Are there known security issues with the app? Does the app use unencrypted data or out-of-date platforms?  |

### Discover app dependencies

As the part of the assessment process, GME needs to identify where apps are running, figure out the dependecies and connections with them.

GME maps the environment in steps.

1. Discovering how servers and machines map to individual apps, network locations, and groups.
2. With previous information, Identifying apps that have few dependencies, and are thus suitable for a quick migration.
3. Using mapping to identify more complex depedencies, and communication between app servers. Grouping these server logically to represent apps, and plan a migration strategy based on these groups.

With apps and services mapping completed, GME can ensure that all app components are identified and accounted for when building the migration plan.

![GitHub Logo](/content/dependency-map.png)

[Image source](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-scale)

### Evaluate apps

Evaluating assessment and mapping results to figure out how to migrate each app in the Service Catalog. 

Providing additional classification to the inventory.


| Category  | Assigned value    | Details           |
|-----------|-------------------|-------------------|
| Business group    | List of business group names  | Which business group is responsible for the inventory item?   |
| POC candidate     | Yes/No                        | Can the app be used as a POC or early adopter for the cloud migration |
| Technial dept     | None/Some/Severe              | Is the inventory item running or using an out-of-support product, platform or operating system    |
| Firewall implications | Yes/No                    | Does the app communicate with internet or outside traffic? Does it integrate with a firewall? |
| Security issues   | Yes/No                        | Are there known security issues with the app? Does the app use unencrypted data or out-of-date platforms?  |
| Migration strategy    | Rehost/Refactor/Rearchitect/Rebuild   | What kind of migration is needed for the app? How will the app be deployed in Azure? |
| Technical complexity  | 1-5   | How complex is the migration? This value should be defined by the DevOps teams and relevant partners.   |
| Business criticality  | 1-5   | How important is the app for the business? For example, a small workgroup app might be assigned a score of one, while a critical app used across the organization might be assigned a score of five. This score will affect the migration priority level.  |
| Migration priority  | 1/2/3 | What is the migration priority for the app? |
| Migration risk    | 1-5   | What is the migration risk level for the app? This value should be defined by the DevOps teams and relevant partners.   |

### Figure out costs

To figure out costs and the potential savings of Azure migration, GME can use the [Total Cost of Ownership (TCO)](https://azure.microsoft.com/pricing/tco/calculator) calculator to calculate and compare the TCO for Azure to a comparable on-premises deployment.

### Identify assessment tools

GME decides which tool to use for discovery, assessment, and building the inventory. GME identifies a mix of Azure tools and services, native app tools and scripts, and partner tools. In particular, GME is interested in how Azure Migrate can be used to assess at scale.

#### Azure Migrate

The Azure Migrate service helps you to discover and assess on-premises VMware VMs, in preparation for migration to Azure. Here's what Azure Migrate does:
1. Discover: Discover on-premises VMware VMs. 
    - Azure Migrate supports discovery from multiple vCenter Servers (serially), and can run discoveries in separate Azure Migrate projects.
    - Azure Migrate performs discovery by means on a VMware VM running the Migrate Collector. The same collector can discover VMs on different vCenter servers, and send data to different projects.

2. Assess readiness: Assess whether on-premises machines are suitable for running in Azure. Assessment includes: 
    - Size recommendations: Get size recommendations for Azure VMs, based on the performance history of on-premises VMs.
    - Estimated monthly costs: Get estimated costs for running on-premises machines in Azure.

3. Identify dependencies: Visualize dependencies of on-premises machines, to create optimal machines groups for assessment and migration.

[Learn more](https://azure.microsoft.com/en-us/services/azure-migrate) Azure migration service capabilities.

#### Migrate at scale

GME needs to use Azure Migrate correctly given the scale of this migration.
- GME will do an app-by-app assessment with Azure Migrate. This ensures that Azure Migrate returns timely data to the Azure portal.
- Learn more about [deploying Azure Migrate at scale](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment).
- Azure Migrate limits summarized in the following lists.
    - *Create Azure Migrate project* has limitation for *10,000 VMs*.
    - *Discovery* has limitation for *10,000 VMs*.
    - *Assessment* has limitation for *10,000 VMs*.

GME will use Azure Migrate as follows:

- In vCenter GME will organize VMs into folders. This will make it easy for them to focus as they run an assessment against VMs in a specific folder.
- Azure Migrate uses Azure Service Map to assess dependencies between machines. This requires agents to be installed on VMs to be assessed. 
    - By using automated scripts, install the required Windows or Linux agents.
    - By scripting, push the installation to VMs within a vCenter folder.

#### Database tools

GME will use tools specifically for database assessment. Such as the [Data Migration Assistant](https://docs.microsoft.com/en-us/sql/dma/dma-overview?view=sql-server-2017) will help assess SQL Server databases for migration.

The Data Migration Assistant (DMA) can figuring out whether on-premises databases are compatible with a range of Azure database solutions, such as Azure SQL Database, SQL Server running on an Azure IaaS VM, and Azure SQL Managed Instance.

#### Partner assessment tools

[Learn more](https://azure.microsoft.com/en-us/migration/migration-partners/) several other partner tools which can help for assessing the on-premises enviroment for migration to Azure.

## Phase 2: Migrate

## Migration patterns

Strategies for migration to the cloud, by following [Azure migration patterns](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-overview), fall into four broad patterns: ***rehost***, ***refactor***, ***rearchitect***, or ***rebuild***. Let's look at these patterns.

1. **Rehost**
        
    - Often reffered to as a "lift and shift". It migrates your apps "as is".
    - Migrate your existing apps to Azure quickly, it doesn't require code changes.
    - Minimize the risk and cost associated with code changes.
    
    **When to use:**

    - When you need to move the app quicky to the cloud.
    - When you need to move the app without modifying it.
    - When your apps are important for your business, but you don't need immediate changes to app capabilities.
    - When your apps are architected so that they can take the advantages of IaaS model scalability after migration. 

2. **Refactor**

    - Referred to as "Repacking". Basically it will use PaaS cloud model offering.
    - Requires minimal changes to apps.
    - For example: 
        - Migrate existing apps to Azure App Service or Azure Kubernetes Service (AKS).
        - Refactor relational or nonrelational databases to Azure SQL Database Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL, and Azure Cosmos DB.

    **When to use:**

    - When your app can easily be repackaged to work in the cloud.
    - When your existing apps applied a container strategy for the workloads.
    - When you think about the portability of your code base.

3. **Rearchitect**
    - Focus on modifying and extending app functionality and the code base to optimize the app architecture for cloud scalability.
    - For example:
        - Break down the monolithic app into group of microservices for scale easily.
        - Rearchitect relational and nonrelational database to a fully managed solution, such as Azure SQL Database Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL, and Azure Cosmos DB.

    **When to use:**
    
    - When your apps need major updates to incorporate new capabilities or meet market demand.
    - When you need to work effectively on a cloud environment.
    - When you need to apply an innovative cloud DevOps practices.
    - When you need to minimize use of virtual machine in your cloud platform.

4. **Rebuild**
    
    - Rebuilding an app from scratch using cloud platform technologies, it also called "cloud-native" or "born in the cloud" apps.
    - For example:
        - Build greenfield apps with cloud-native technologies like Azure Functions, Azure AI, Azure SQL Database Managed Instance, and Azure Cosmos DB.

    **When to use:**
    
    - When you want rapid development and existing apps have limited capabilities and lifespan.
    - When you are ready to accelerate business innovation (including DevOps practice provided by cloud platform), building new apps using cloud-native technology and take advantage of advancements in AI, Blockchain and IoT.

Data migration must also be considered, especially with the volume of databases. The default approach is to use PaaS services such as Azure SQL Database to take full advantage of cloud features. By moving to a PaaS service for databases, GME will only have to maintain data, leaving the underlying platform to Microsoft.

## Evaluate migration tools

The primarily a couple of Azure services and tools for migration:

- [Azure Site Recovery (SR)](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): Orchestrates disaster recovery, and migrates on-premises VMs to Azure.
- [Azure Database Migration Service (DMS)](https://docs.microsoft.com/azure/dms/dms-overview): Migrates on-premises databases such as SQL Server, MySQL, and Oracle to Azure.

## Azure Site Recovery

Azure Site Recovery is the primary Azure service for orchestrating disaster recovery and migration from within Azure, and from on-premises sites to Azure.

1. Site Recovery enables, orchestrates replication from your on-premises sites to Azure.
2. When replication is set up and running, on-premises machines can be failed over to Azure, completing the migration.

[Learn more](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-rehost-vm) about the best practise for VM rehost.

### Using Azure Site Recovery at scale

GME plans on running multiple "lift and shift" migrations. To ensure this works, Site Recovery will be replicating batches of around 100 VMs at a time. To make sure how this will work, GME needs to perform capacity planning for the proposed Site Recovery migration.

- Gathering information about their traffic volumes. In particular:
    - Determining the rate of change for VMs it wants to replicate.
    - Taking network connectivity from the on-premises site to Azure into account.
- In response to capacity and volume requirements, GME will need to allocate sufficient bandwidth based on the daily data change rate for the required VMs, to meet its recovery point objective (RPO).
- Lastly, figuring out how many servers are needed to run the Site Recovery components that are needed for the deployment.

## Azure Database Migration Service

The Azure Database Migration Service is a fully managed service that enables seamless migrations from multiple database sources to Azure data platforms with minimal downtime.

- DMS integrates functionality of existing tools and services. It uses the Data Migration Assistant (DMA), to generate assessment reports that pinpoint recommendations about database compatibility and any required modifications.
- DMS uses a simple, self-guided migration process, with intelligent assessment that helps address potential issues before the migration.
- DMS can migrate at scale from multiple sources to the target Azure database.
- DMS provides support from SQL Server 2005 to SQL Server 2017.

[Get a more Microsoft tools](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services) for database migration.

### Using DMS at scale

- When provisioning DMS, GME needs to size it correctly and set it to optimize performance for data migrations. GME will select the "business-critical tier with 4 vCores" option, thus allowing the service to take advantage of multiple vCPUs for parallelization and faster data transfer.
- Another scaling strategy for GME is temporarily scale up the Azure SQL or MySQL Database target instance to the Premium tier SKU during the data migration. This minimizes database throttling that could affect data transfer activities when using lower-level SKUs.

## Using another tools

In addition to Site Recovery and DMS, GME can use other tools and services to identify VM information.
- They have scripts to help with manual migrations. These are available in the GitHub repo.

## Phase 3: Optimize

### Azure Cost Management

To make the most optimize of their cloud investment, GME will take advantage of the free Azure Cost Management tool.
- This licensed solution built by Cloudyn, a Microsoft subsidiary, allows GME to manage cloud spending with transparency and accuracy. It provides tools to monitor, allocate, and trim cloud costs.
- Azure Cost Management provides simple dashboard reports to help with cost allocation, showbacks and chargebacks.
- Cost Management can optimize cloud spending by identifying underutilized resources that GME can then manage and adjust.
- [Learn more](https://docs.microsoft.com/azure/cost-management/overview) about the Azure Cost Management.

### Native tools

By scripting, GME can locate unused resources:
- During large migrations, there are often leftover pieces of data such as virtual hard drives (VHDs), which incur a charge, but provide no value to the company. 
- GME will take advantage of work done by Microsoft’s IT department, and consider implementing the Azure Resource Optimization (ARO) Toolkit.
- GME can deploy an Azure Automation account with preconfigured runbooks and schedules to its subscription, and start saving money. Azure resource optimization happens automatically on a subscription after a schedule is enabled or created, including optimization on new resources.
- This provides decentralized automation capabilities to reduce costs. Features include: 
    - Autosnooze Azure VMs based on low CPU.
    - Schedule Azure VMs to snooze and unsnooze.
    - Schedule Azure VMs to snooze or unsnooze in ascending and descending order using Azure tags.
    - Bulk deletion of resource groups on-demand.
- Get started with the ARO toolkit in this [GitHub repo](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### Partner Optimization tools

Partner tools such as [Hanu](https://hanu.com/insight) and [Scalr](https://www.scalr.com/cost-optimization) can be used.

## Phase 4: Security and Manage

### Security

GME will rely on the Azure Security Center for unified security management and advanced threat protection across hybrid cloud workloads.

- The Security Center provides full visibility into, and control over, the security of cloud apps in Azure.
- GME can quickly detect and take action in response to threats, and reduce security exposure by enabling adaptive threat protection.
- [Learn more](https://azure.microsoft.com/services/security-center) about the Security Center.

### Monitoring

GME needs visibility into the health and performance of the newly migrated apps, infrastructure, and data now running Azure. GME will use built-in Azure cloud monitoring tools such as Azure Monitor, Log Analytics workspace, and Application Insights.

- Using these tools GME can easily collect data from sources and gain rich insights. For example, GME can gauge CPU disk and memory utilization for VMs, view applications and network dependencies across multiple VMs, and track application performance.
- GME will use these cloud monitoring tools to take action and integrate with service solutions.
- [Learn more](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) about Azure monitoring.

### Business continuity and disaster recovery

GME will need a business continuity and disaster recovery (BCDR) strategy for their Azure resources.

- Azure provides [built-in BCDR features](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) to keep data safe and apps/services up and running.
- In addition to built-in features, GME wants to ensure that it can recover from failures, avoid costly business disruptions, meet compliance goals, and protect data against ransomware and human errors. To do this: 
    - GME will deploy Azure Backup as a cost-efficient solution for backup of Azure resources. Because it’s built-in, GME can set up cloud backups in a few simple steps.
    - GME will set up disaster recovery for Azure VMs using Azure Site Recovery for replication, failover, and failback between Azure regions that it specifies. This ensures that apps running on Azure VMs will remain available in a secondary region of GME's choosing if an outage occurs in the primary region. [Learn more](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### Continous Integration and Continous Delivery/Deployment

For increasing agility of IT team to more responsive to the needs of business and market demand. GME will adopt the DevOps model to their organization.

GME considers to using Azure DevOps services.

- Empower teams to manage their work with agility and full visibility across products and projects. Define, track, and lay out work with Kanban boards, backlogs custom dashboards and reporting capabilities using Azure Boards.
- Automate testing and practice continuous integration in the cloud with Azure Pipelines, create automatic workflows from idea to production with GitHub Actions, and even bring your Jenkins workloads to the Azure.
- Deploy the applications to any Azure service automatically and with full control to continuously deliver value to customers.
- Implement full stack monitoring, get actionable alerts, and gain insights from logs and telemetry with Azure Monitor. Manage your cloud environment with Azure Automation and tools such as Ansible, Chef, or Puppet. 
- [Learn more](https://azure.microsoft.com/en-us/solutions/devops/) about Azure DevOps services.

## Conclusion

In this scenario, GME planned for a cloud migration at scale. They divided the migration process into four stages. From assessment and migration, through to optimization, security, and management after migration was complete. Mostly, it's important to plan a migration project as a whole process, but to migrate systems within an organization by breaking sets down into classifications and numbers that make sense for the business. By assessing data and applying classifications, and project can be broken down into a series of smaller migrations, which can run safely and rapidly. The sum of these smaller migrations quickly turns into a large successful migration to cloud.

## Reference

1. [Azure best practice: Migrate at scale](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-scale)
2. [What is IaaS](https://azure.microsoft.com/overview/what-is-iaas)
3. [What is PaaS](https://azure.microsoft.com/overview/what-is-paas)
4. [Azure cloud-native](https://azure.microsoft.com/en-us/overview/cloudnative/)
5. [Database Migration Assistant (DMA)](https://docs.microsoft.com/en-us/sql/dma/dma-overview?view=sql-server-2017)
6. [System Center Service Manager (SC-SM)](https://docs.microsoft.com/en-us/system-center/scsm/service-manager?view=sc-sm-2019#main)
7. [Definition Configuration Management Database](https://searchdatacenter.techtarget.com/definition/configuration-management-database)
8. [Azure Migration Overview](https://docs.microsoft.com/en-us/azure/migrate/contoso-migration-overview)
9. [Azure Migrate Overview](https://azure.microsoft.com/en-us/services/azure-migrate/)
10. [Azure Migration Journey](https://azure.microsoft.com/en-us/migration/migration-journey/)
11. [Cloud Migration Checklist](https://azure.microsoft.com/mediahandler/files/resourcefiles/cloud-migration-checklist/Cloud_Migration_Checklist.pdf)