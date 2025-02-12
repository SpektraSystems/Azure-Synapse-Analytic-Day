# Hands-On-Lab: SQL Datawarehouse with Syanpse

### Overall Estimated Duration: 4 hours

## Overview

In this lab, you will use a pipeline with parallel activities to bring data into the Data Lake, transform it, and load it into the Azure Synapse SQL Pool. You will also monitor the progress of the associated tasks.

Once data is properly understood and interpreted, moving it to the various destinations where processing steps occur is the next big task. Any modern data platform must provide a seamless experience for all the typical data wrangling actions like extractions, parsing, joining, standardizing, augmenting, cleansing, consolidating, and filtering.

Azure Synapse Analytics provides two significant categories of features - data flows and data orchestrations (implemented as pipelines). They cover the whole range of needs, from design and development to triggering, execution, and monitoring.

## Objective

This lab provides hands-on experience in building a modern data warehouse using Azure Synapse Analytics. Participants will ingest, transform, and load data using Synapse Notebooks, Data Flows, and Pipelines, while also learning to monitor pipeline execution and Spark application performance.

- **Validate lab environment**: Ensure the Azure Synapse environment is correctly set up.
- **Data Ingestion**: Load data into Azure Synapse Analytics and Azure Data Lake Storage Gen2.
- **Explore and modify a notebook**: Use Synapse Notebooks to process and transform data.
- **Explore, modify, and run a Pipeline containing a Data Flow**: Perform ETL operations using Data Flows.
- **Monitor pipelines**: Track execution status, analyze logs, and troubleshoot errors.
- **Monitor Spark applications**: Identify performance metrics and optimize Spark workloads.
  
## Prerequisites

Participants should have the following prerequisites:

- **Basic familiarity with Azure services**: Understanding of Azure Synapse Analytics, Data Lake Storage, and Azure Monitor.
- **Fundamental knowledge of data processing**: Awareness of ETL (Extract, Transform, Load) concepts and structured data handling.
- **No prior experience with Synapse Pipelines required**: This lab introduces low-code and code-based approaches for data processing.
- **Access to an Azure Synapse Analytics workspace**: Ensure you have the necessary permissions to work with Pipelines, Notebooks, and Spark Pools.

## Architechture

This lab follows a modern data warehouse architecture using Azure Synapse Analytics to ingest, process, and store data efficiently. Data is ingested from multiple sources, including Azure Data Lake Storage Gen2, Azure SQL Database, and external APIs. Synapse Pipelines handle ETL (Extract, Transform, Load) processes, while Synapse Notebooks enable data transformation and machine learning operations using Apache Spark. Data Flows provide a low-code approach for scalable data transformations within Synapse Pipelines. Monitoring tools like Azure Monitor, Log Analytics, and Synapse Studio help track pipeline execution, analyze Spark performance, and troubleshoot errors to ensure efficient data processing.

## Architechture Diagram

![](media/finalarch.png)

## Explanation of Components

The architecture for this lab involves several key components:

- Azure Synapse Analytics : A unified analytics platform that enables large-scale data integration, transformation, and analysis using SQL pools, Spark pools, and Synapse Pipelines.
- **Azure Data Lake Storage Gen2** : A scalable storage solution designed for big data analytics, used to store raw and processed data before loading it into Synapse.
- **Synapse Pipelines** : A data integration tool that automates ETL (Extract, Transform, Load) operations, enabling seamless data movement between sources and destinations.
- **Synapse Notebooks** : Interactive notebooks powered by Apache Spark, used for data exploration, transformation, and machine learning tasks.
- **Data Flows** : A low-code ETL solution within Synapse Pipelines that allows users to visually design and execute data transformation processes.
- **Spark Pools** : A distributed computing environment within Synapse Analytics, used for executing Spark-based workloads efficiently.
- **Azure Monitor & Log Analytics** : Tools that provide real-time monitoring, diagnostics, and performance tracking for Synapse Pipelines and Spark applications.
- **Synapse Studio** : A web-based development environment for managing and orchestrating Synapse resources, including Pipelines, Notebooks, and Data Flows.
  
## Getting Started with Lab

Welcome to the PL-900 Microsoft Power Platform Fundamentals Lab! We've prepared an interactive environment for you to explore Power Apps, Power Automate, and Power BI. 

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **Lab Guide** will be right at your fingertips within your web browser.

   ![](./media/i3.jpg)  

## Virtual Machine & Lab Guide

In the integrated environment, the lab VM serves as the designated workspace, while the lab guide is accessible on the right side of the screen.

**Note:** Kindly ensure that you are following the instructions carefully to ensure the lab runs smoothly and provides an optimal user experience.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.

   ![Create storage by clicking confirm.](./media/i4.jpg)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
   ![](./media/i5.jpg)
 
## Managing Your Virtual Machine
 
Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!
 
   ![](./media/i7.jpg)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

   ![](./media/zoomoutin.png)

## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:
- Email Support: labs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next** from the lower right corner to move on to the next page.

![](./media/i8.jpg)

### Happy Learning!!
