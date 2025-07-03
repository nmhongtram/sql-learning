## SQL Project 1: Intro to SQL Project
Introduce an **exciting project to build a modern SQL data warehouse from scratch**. The project aims to not only teach how to build such a data warehouse but also how these types of projects are **implemented in real-world companies**.

**Instructor Background:**

- The instructor is **Baraa Zini**.
- He has **built more than five successful data warehouse projects** in various companies.
- Currently, he is **leading big data and BI projects at Mercedes-Benz**.
- The project promises to share **real skills and real knowledge from complex projects**.

**Key Outcomes and Benefits of the Project:**

- By the end, participants will have a **professional portfolio project to showcase their new skills**, for instance, on LinkedIn.
- **Everything is offered for free**, with no hidden costs.

**Skills Gained for Various Data Roles:**

- As a **Data Architect**, you will learn to **design a modern data architecture** following best practices.
- As a **Data Engineer**, you will write code to **clean, transform, load, and prepare data for analysis**.
- As a **Data Modeler**, you will learn the basics of **data modeling** and create a new data model from scratch for analysis.
- As a **Data Analyst or Data Scientist**, you will practice **answering more than 20 real-world business questions** using the data warehouse built.

**Tools and Compatibility:**

- The project primarily uses **SQL Server**.
- However, if you prefer other databases like **MySQL or Postgres, you can follow along just fine**.
## SQL Project 2: Data Warehouse Basics Explained | Data Engineer Portfolio Project
Provide a **fundamental understanding of what a data warehouse is** and why companies choose to build such data management systems before diving into specific tools and cool technologies.

**What is a Data Warehouse?** According to Bill Inmon, often called the "father of the data warehouse," a data warehouse is a **subject-oriented, integrated, time-variant, and nonvolatile collection of data designed to support the Management's decision-making process**.

- **Subject-oriented**: It focuses on a specific business area like sales, customers, or finance.
- **Integrated**: It combines data from multiple source systems, not just one.
- **Time-variant**: It retains historical data.
- **Nonvolatile**: Once data enters the data warehouse, it is neither deleted nor modified.

**Problems Without Proper Data Management (Scenario 1):** Without a real data management system like a data warehouse, companies face several significant issues:

- **Time-consuming manual processes**: Data analysts spend days or weeks manually collecting and transforming raw data into reports, which can take weeks or even months.
- **Inconsistent data status**: Users consume multiple reports with different data statuses (e.g., one report is 40 days old, another 10 days, making real decision-making difficult).
- **Manual process is slow and stressful**: More employees involved increase human errors, leading to bad decisions.
- **Difficulty handling Big Data**: If sources generate massive amounts of data, data analysts struggle to collect it, potentially breaking the process and preventing fresh data generation.
- **Chaotic integrated reports**: Merging data manually from multiple sources for an integrated report is extremely chaotic, time-consuming, and full of risk.

**Benefits of a Data Warehouse (Scenario 2):** A data warehouse addresses these issues by providing a **single point of truth** for analysis and reporting:

- **Automated processes**: The data team no longer manually collects data; an **ETL (Extract, Transform, Load) process** extracts, transforms, and loads data into the data warehouse.
- **Speed and Freshness**: Data can be loaded from sources to reports in hours or even minutes, eliminating long waiting times.
- **Integrated data**: The data warehouse brings all sources together in one place, making reporting much easier.
- **Historical data**: It allows access to historical data.
- **Consistent data status**: All reports consume data from this single source of truth, ensuring consistent data status across all reports.
- **Big Data handling**: Modern data warehouses on cloud platforms can easily handle massive amounts of data from various sources.
- **Reduced human error**: Automation significantly reduces human errors.
- **Improved decision-making**: Companies can count on professional and fresh reports to make good and fast decisions.

**Roles in a Data Warehouse Environment:**

- **Data Engineer**: Builds the **ETL component** and the data warehouse, accessing sources, scripting ETLs, and building the database.
- **Data Analyst**: Consumes the data warehouse, builds data models and reports, and shares them with stakeholders based on requirements.

**Analogy: Data Warehouse as a Busy Restaurant Kitchen** The video uses a restaurant analogy to explain the data warehouse process:

- **Raw ingredients (data)** arrive from suppliers (sources).
- They are **cleaned, chopped, organized, and stored** (preparation phase, like ETL's transformation).
- When an order (report/analysis request) comes in, the **prepared ingredients** are quickly grabbed to create a perfect dish (report/analysis).
- The data warehouse is like the kitchen where raw data is cleaned, sorted, and stored, ready to be served up exactly when needed.
## SQL Project 3: ETL Process Explained | Data Engineer Portfolio Project
A comprehensive explanation of the **ETL process (Extract, Transform, Load)**, which is a core component of data warehousing projects. Building the ETL component typically consumes almost **90% of the effort** in such projects.

**What is ETL?** ETL is the process of moving data from a **source system** to a **target destination** (e.g., database tables or a data warehouse).

**The Three Stages of ETL:**

1. **Extract (E)**:
    - **Purpose**: Identify and pull the necessary data from the source system **without changing anything**; it's a one-to-one copy of the source data.
    - **Methods of Extraction**:
        - **Pulling data**: The data warehouse system fetches data from the source.
        - **Pushing data**: The source system sends data to the data warehouse.
    - **Types of Extraction**:
        - **Full Extraction**: All records from tables are loaded every day.
        - **Incremental Extraction**: Only new or changed data is identified and loaded daily, making it a smarter approach.
    - **Techniques for Extraction**: Manually, connecting to a database with a query, parsing files, connecting to APIs, event-based streaming (e.g., Kafka), Change Data Capture (CDC), or web scraping.
    
2. **Transform (T)**:
    - **Purpose**: Take the extracted data and perform manipulations and transformations to **reshape it into a new format and shape** suitable for analysis and reporting. This is often a "heavy working" process.
    - **Types of Transformations**:
        - **Data Enrichment**: Adding values to datasets.
        - **Data Integration**: Combining data from multiple sources into one data model.
        - **Deriving New Columns**: Creating new columns based on existing ones.
        - **Data Normalization**: Mapping coded source values to more user-friendly values for analysis.
        - **Business Rules and Logic**: Defining criteria to build new columns based on business requirements.
        - **Data Aggregation**: Aggregating data to a different granularity.
        - **Data Cleansing**: Removing duplicates, filtering data, handling missing or invalid values, removing unwanted spaces, casting data types, and detecting outliers.
    
3. **Load (L)**:
    - **Purpose**: Take the prepared (transformed) data and **insert it into its final destination**, such as a data warehouse.
    - **Processing Types**:
        - **Batch Processing**: Loading data in one big batch, typically scheduled once or twice a day.
        - **Stream Processing**: Processing changes from the source system as soon as possible to achieve real-time data warehousing (a challenging task).
    - **Load Methods**:
        - **Full Load**: Similar to full extraction. Database methods include:
            - **Truncate and Insert**: Emptying the table completely and then inserting everything from scratch.
            - **Upsert (Update Insert)**: Updating existing records and inserting new ones.
            - **Drop, Create, and Insert**: Dropping the entire table, recreating it, and then inserting data.
        - **Incremental Load**: Similar to incremental extraction. Methods include:
            - **Upserts (Update and Insert)**: Updating or inserting statements into tables.
            - **Only Inserts (Append)**: Adding data to the table without updates, especially if the source is a log.
            - **Merge (Update, Insert, and Delete)**: Similar to upsert but also includes deletions.
    - **Slowly Changing Dimensions (SCD)**: This concept deals with the **historization of tables** in data warehousing:
        - **SCD0 (No Historization)**: No changes are tracked; nothing is updated.
        - **SCD1 (Overwrite)**: Records are updated with new information, overwriting old values, which means history is lost.
        - **SCD2 (Add Historization)**: Each change from the source system results in new records being inserted. Old data is made inactive, and the new record becomes active, preserving history.

**ETL in Real Projects:** In real projects, data architectures often have **multiple layers** (e.g., raw, staging, transformed). The full ETL process isn't always used between every layer; sometimes only specific components (Extract, Transform, or Load) are applied depending on the data architecture design. For example, data might be extracted and loaded directly to a first layer without transformation to see it as is.

**ETL Methods Used in This Specific Project:** 

- **Extraction**:
    - Method: **Pull extraction**.
    - Type: **Full extraction**.
    - Technique: **Passing files** to the data warehouse.
- **Transformation**: The project will cover **all types of transformations** discussed, as they are commonly faced in data projects.
- **Load**:
    - Processing Type: **Batch processing**.
    - Load Method: **Full load** (due to full extraction).
    - Technique: **Truncate and inserts**.
    - Historization: **SCD1 (overwrite)** will be used, meaning the content of the data warehouse will be updated.

The video concludes the theoretical part of understanding data warehousing and prepares the audience to set up their environment for the project.
## SQL Project 4: Notion Project Plan & Set Up Your Environment | Data Engineer Portfolio Project

**Setting up the project environment** and creating an initial **project plan using Notion**. The instructor emphasizes that project planning is a crucial, often overlooked, step for successful complex projects like data warehouses.

### Project Resources and Tools Setup

To begin the project, several materials and tools need to be downloaded and accounts created:

- **Project Files**:
    - You need to **download all project files** from a provided link in the description. This will give you a zip file containing the repository structure and, most importantly, the **datasets**.
    - The datasets include two sources: **CRM and ERP**, each with three CSV files. These will be the data used for the project.
    - It's recommended to store these data files in a location on your PC where they won't be lost.
- **Project Tools (Required)**:
    - **SQL Server Express**: A local server where your database will reside.
    - **SQL Server Management Studio (SSMS)**: A client tool to interact with the database and run queries.
    - **Draw.io**: A free and useful tool for drawing diagrams like data models, data architecture, and data lineage.
- **Optional Tools & Resources**:
    - **GitHub Repository**: A link to the instructor's repository is provided. You will learn its structure and create your own repository during the project.
    - **Notion**: A free tool used for project management in this course. It helps organize ideas, plans, and resources in one place. Creating a free account is recommended to follow along and build your project plan.

### Project Planning with Notion

The video highly recommends creating a project plan, especially for complex data warehouse projects. According to Gartner reports, **over 50% of data warehouse projects fail**, and a clear project plan is key to success in such complex endeavors.

Here's how to set up your project plan in Notion:

- **Create a New Page**: Name it "Data Warehouse Projects".
- **Define Main Phases (Epics)**:
    - Create an **inline database table** (using `/database in-line`) and call it "Project Epics" (or stages, phases).
    - Epics are large tasks requiring significant effort.
    - The initial project epics include: **Requirements Analysis, Designing Data Architecture, and Project Initialization**.
- **Define Subtasks**:
    - Create another **inline database table** called "Project Tasks".
    - **Link the "Project Tasks" table to the "Project Epics" table** using a "Relation" property (two-way relation). This allows you to assign specific tasks to their corresponding epics.
    - Break down each epic into smaller, manageable tasks. For example, "Design Data Architecture" can include tasks like "Choose data management approach," "Brainstorm and Design the layers". "Project Initialization" can include "Create Git repo," "Prepare the structure," and "Create the database and the schemas".
- **Track Progress**:
    - Add a **checkbox property** to the "Project Tasks" table to mark tasks as completed.
    - Add a **"Rollup" property** to the "Project Epics" table. Configure it to reference the "Project Tasks" table's checkbox property and use the "Percent checked" calculation. This will display a **progress bar** for each epic, showing how much of it has been completed.
- **Organize and Customize**:
    - Rename columns and add icons to epics and tasks for better visual appeal and organization.
    - **Group the "Project Tasks" table by epics** (using the three dots -> Group -> Group by Epics). This creates sections for each epic, allowing you to expand and minimize tasks, providing a clearer overview of the project structure.
    - You can manually sort the epics as well.

While professional tools like Jira are used in companies, Notion is an excellent, free alternative for personal projects. Having a clear plan, seeing the big picture, and marking tasks as complete can significantly boost satisfaction and motivation throughout the project.

### Initial Project Plan Details (Upcoming Steps)

The initial plan for the project will cover the following key steps, which will be further detailed as more information becomes available:

1. **Requirements Analysis**: The first step is to analyze and understand the project requirements.
2. **Designing Data Architecture**:
    - Choose the data management approach.
    - Brainstorm and design the layers of the data warehouse.
    - Draw the data architecture to ensure a clear understanding of its structure.
3. **Project Initialization**:
    - Create detailed project tasks (adding more epics and tasks).
    - Establish naming conventions for consistency across the project.
    - Create a Git repository and prepare its structure for committing work.
    - Write the first script to create the database and schemas.

The video concludes by setting the stage to begin the "Requirements Analysis" epic, which is the first step in the project.
## SQL Project 5: Design Data Architecture for Your Data Warehouse | Data Engineer Portfolio Project

This video focuses on **designing data architecture** and **building a data warehouse** as part of a data engineering project.

### I. Analyzing Requirements for the Data Warehouse

- **Importance of Requirement Analysis**: It is crucial to understand the specific type of data warehouse to build, as blindly implementing can lead to unnecessary features and wasted time. Discussions with stakeholders are essential to define exactly what needs to be built`.
- **Project Objective**: The primary goal is to **develop a modern data warehouse using SQL Server to consolidate sales data**, enabling analytical reporting and informed decision-making. This is a data engineering task.
- **Key Specifications**:
    - **Data Sources**: Data will be imported from two source systems: **ERP and CRM**, provided as **CSV files**.
    - **Data Quality**: It is necessary to **clean and fix data quality issues** before data analysis, acknowledging that raw data is typically messy.
    - **Integration**: Both sources must be **combined into a single, user-friendly data model** designed for analytics and reporting.
    - **Historization**: The focus is on the **latest data sets, with no need for historization**; historical data does not need to be built in the database.
    - **Documentation**: **Clear documentation of the data model** must be provided to support business users and analytical teams, making data consumption easier.
- **Platform**: The chosen platform for this project is **SQL Server**.

### II. Designing Data Architecture: Choosing a Data Management Approach

- **Analogy**: Designing data architecture is likened to **creating a blueprint for a house**; a data architect ensures data flow, integration, and access are functional, scalable, and easy to maintain.
- **Role of a Data Architect**: They design how data will flow, integrate, and be accessed, ensuring the data warehouse is not only functional but also **scalable and easy to maintain**.
- **Four Major Data Management Approaches**:
    1. **Data Warehouse**:
        - Suitable for **structured data**.
        - Builds **solid foundations for reporting and business intelligence**.
    2. **Data Lake**:
        - **More flexible**; stores structured, semi-structured, and unstructured data (e.g., database tables, blogs, images, videos).
        - Suitable for **advanced analytics or machine learning** in addition to reporting.
        - Can become a "data swamp" if too unorganized.
    3. **Data Lakehouse**:
        - A **modern approach** combining the flexibility of a data lake with the structure and organization of a data warehouse.
    4. **Data Mesh**:
        - A **decentralized approach** where multiple departments or domains build and share data products.
        - Addresses bottlenecks of centralized systems.
- **Selected Approach for this Project**: The **Data Warehouse approach** was chosen.

### III. Designing Data Architecture: How to Build the Data Warehouse

- **Four Methodologies for Building a Data Warehouse**:
    1. **Inmon Approach**:
        - Involves three layers: **Staging** (raw data lands), **Enterprise Data Warehouse** (data modeled in third normal form to create a new, integrated data model), and **Data Marts** (small, topic-focused subsets designed for reporting tools like Power BI or Tableau).
    2. **Kimball Approach**:
        - A **faster approach** that skips the Enterprise Data Warehouse, going directly from the Staging layer to Data Marts.
        - Can lead to **chaos and repeated transformations** over time due to a lack of focus on the big picture.
    3. **Data Vault**:
        - Similar to Inmon but introduces more standards and rules.
        - The central layer is split into **Raw Vault** (original data) and **Business Vault** (business rules and transformations).
    4. **Medallion Architecture**:
        - Consists of three layers: **Bronze, Silver, and Gold**.
        - It is described as **very easy to understand and build**, and is the favored approach for this project.
- **Selected Methodology for this Project**: The **Medallion Architecture** was chosen.

### IV. Medallion Architecture Layers Detailed

- **Bronze Layer**:
    - **Main Objective**: Stores **raw, unprocessed data** exactly as it comes from the sources. Its purpose is for **traceability and debugging**, allowing data engineers to investigate issues by going back to the untouched source data.
    - **Object Type**: **Tables**.
    - **Load Method**: **Full load** using the "truncate and insert" method. This is chosen for its speed and ease.
    - **Transformations**: **No transformations**; data remains untouched and unmanipulated, even if it's bad.
    - **Data Modeling**: "As-is" from the source systems; the original data model is not broken.
    - **Target Audience**: **Only data engineers**.
    
- **Silver Layer**:
    - **Main Objective**: Stores **clean and standardized data**.
    - **Object Type**: **Tables**.
    - **Load Method**: **Full load**.
    - **Transformations**: Focuses on **basic transformations** like data cleansing, standardization, normalization, deriving new columns, and data enrichment. **No business rules** are applied here; those are pushed to the next layer.
    - **Data Modeling**: "As-is" from the source systems; the original data model is not broken.
    - **Target Audience**: **Data engineers, data analysts, and data scientists**. Business users are typically not given access.
    
- **Gold Layer**:
    - **Main Objective**: Contains **business-ready data** for consumption by business users and analysts. It is designed for purposes such as reporting, analytics, machine learning, and AI.
    - **Object Type**: Best practice suggests using **views** because they are virtual, dynamic, and do not require a separate load process, offering speed.
    - **Load Method**: No load process is needed for views.
    - **Transformations**: Focuses on **business transformations**, including data integrations between source systems, data aggregations, and applying business logic/rules to build a data model ready for business intelligence.
    - **Data Modeling**: Can follow a **star schema, snowflake schema, or use aggregated objects**.
    - **Target Audience**: **Data analysts and business users**.

### V. Secret Principle: Separation of Concerns

- **Definition**: This principle dictates **breaking down a complex system into smaller, independent parts**, where each part is responsible for a **specific, non-duplicated task**. Components of the architecture must not duplicate tasks.
- **Importance**: It prevents mixing everything, which is a common mistake in large projects, fostering a **robust architecture**.
- **Application in Medallion Architecture**:
    - Data cleansing is strictly done in the Silver layer, while business transformations are only in the Gold layer. No business transformations are allowed in Silver, and no data cleansing in Gold.
    - Data ingestion occurs exclusively in the Bronze layer; direct loading to Silver from source systems is not allowed, preventing duplication of ingestion tasks across layers.

### VI. Drawing the Data Architecture

- **Visual Representation**: A typical diagram includes three main layers or containers:
    1. **Source System Layer**: Shows data origins, such as **CRM and ERP CSV files** located in folders. Descriptions include **CSV file type** and **files in folder interface**.
    2. **Data Warehouse Layer**: Contains the **Bronze, Silver, and Gold layers**. Each layer is detailed with its **main objective** (e.g., raw data, clean & standardized data, business-ready data), **object type** (table/view), **load method** (batch processing, full load, truncate and insert), **transformation types** (none, basic, business), and **data modeling approach** (as-is, star schema, snowflake, aggregated objects). A database icon visually represents these layers.
    3. **Consume Layer**: Represents end-users and tools that consume the data, such as **Business Intelligence and Reporting tools like Power BI or Tableau**, ad-hoc analysis via **SQL queries**, and for **machine learning purposes**. Arrows indicate the flow of data from left to right through the layers.
- **Technology**: **SQL Server** is the chosen technology for building this data warehouse.