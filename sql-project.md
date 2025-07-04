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
- **Using Draw.io & Flaticon**

## SQL Project 6: Project Setup - Git, Naming & Database Creation | Data Engineer Portfolio Project

This video focuses on **setting up a data engineering project**, covering essential initial steps like defining a project structure, establishing naming conventions, setting up a Git repository, and creating the initial database and schemas in SQL Server.

Here's a breakdown of the key topics:

- **Project Structure and Layers**:
    
    - The project follows a **three-layer architecture**: Bronze, Silver, and Gold.
    - Major epics are defined as building each layer: "Build Bronze Layer," "Build Silver Layer," and "Build Gold Layer".
    - Tasks within each epic generally follow a pattern: analyzing, coding, testing, documenting, and committing work to the Git repository.
    
- **Defining Naming Conventions**:
    
    - **Importance**: Defining a naming convention early prevents inconsistency and chaos, especially with multiple developers. It saves time by avoiding the need to rename everything later.
    - **When to Define**: At the early phase of the project.
    - **General Rules**:
        - **Snake case** is chosen for this project: all letters in a word are lowercase, and words are separated by an underscore (e.g., `customer_info`).
        - **Decide on a single language** for the project (e.g., English).
        - **Avoid using SQL reserved words** as object names (e.g., do not name a table "table"). These rules apply to everything: tables, columns, stored procedures, etc..
    - **Specific Rules for Table Names per Layer**:
        - **Bronze Layer**: Tables follow the `SourceSystem_Entity` rule (e.g., `CRM_CustomerInfo`). The name starts with the source system (e.g., CRM, ERP), followed by an underscore, and then the entity or table name.
        - **Silver Layer**: Exactly the same as the Bronze layer, as no renaming or new data modeling occurs.
        - **Gold Layer**: Since new data models are built and multiple sources are integrated, the source system name is not used. Names must be **meaningful, business-aligned**, starting with a **category prefix**. Examples include:
            - `Fact_Sales` (for fact tables).
            - `Dim_Customers` or `Dim_Products` (for dimension tables, using `dim_`).
            - `Agg_Customers` or `Agg_SalesMonthly` (for aggregated tables, using `agg_`).
    - **Specific Rules for Column Names**:
        - **Surrogate Keys (in Gold Layer)**: Follow the pattern `TableName_Key` (e.g., `customer_key` for a surrogate key in the `Dim_Customers` table).
        - **Technical/Metadata Columns**: Columns added by the data engineer (not from source systems) should start with the prefix `dw_` (e.g., `dw_LoadDate`) to distinguish them from original columns.
    - **Specific Rules for Stored Procedures**: ETL scripts responsible for loading data should start with `load_` followed by the layer name (e.g., `load_bronze`, `load_silver`).
    
- **Git Repository Creation and Structure**:
    
    - **Purpose of Git**: Provides a safe place to store code, track changes, enable team collaboration, allow rollbacks if something goes wrong, and serves as a portfolio piece for job applications.
    - **Creation Steps**:
        - Create a new repository (e.g., "SQL Data Warehouse Project").
        - Add a description (e.g., "Building a modern data warehouse with SQL Server").
        - Choose visibility (public/private).
        - Add a **README file**.
        - Select a license, such as the **MIT license**, which allows freedom of use and modification of code.
    - **Repository Structure**: Create main folders such as `datasets`, `documents`, `scripts`, and `tests`.
    - **README File**: Acts as the homepage of the repository, written in **Markdown (.md)** format. It should include a project description, welcome message, project requirements, licensing information, and a section about the author.
    
- **Database and Schema Creation in SQL Server**:
    
    - **Creating the Database**:
        - First, switch to the `master` system database using `USE master`.
        - Then, create the new database using `CREATE DATABASE DataWarehouse`.
        - Switch to the newly created database using `USE DataWarehouse`.
    - **Creating Schemas**:
        - Schemas act as **folders or containers** to organize objects within the database.
        - Three schemas are created, one for each layer: `CREATE SCHEMA bronze`, `CREATE SCHEMA silver`, `CREATE SCHEMA gold`.
        - The `GO` command is used as a **separator** in SQL scripts, ensuring each command is fully executed before the next.
    - **Best Practices for Database Scripts**:
        - **Check for existing database**: Before creating a database, it's crucial to check if it already exists and drop it if it does, to avoid errors during recreation (e.g., `IF EXISTS(SELECT 1 FROM sys.databases WHERE name = 'DataWarehouse') DROP DATABASE DataWarehouse;`).
        - **Add a header comment**: Each script should start with a header comment explaining its purpose, as this helps anyone (including yourself later) understand the script's function without detailed memory.
        - **Include warnings**: Especially for scripts that can destroy data (like dropping a database), warnings should be clearly stated in the header comments to prevent accidental data loss.
        - **Add inline comments**: Use comments within the code to explain specific sections or steps.
    - **Committing the Work**: Once the database and schemas are created, the SQL script (e.g., `init_database.sql`) is committed to the `scripts` folder in the Git repository.

## SQL Project 7: Build The Bronze Layer - Data Ingestion | Data Engineer Portfolio Project

This video focuses on **building the Bronze Layer** in a data engineering project, emphasizing the critical initial steps of data ingestion and best practices for creating a robust ETL (Extract, Transform, Load) process. The Bronze layer is characterized by a **full load strategy** (truncating and then inserting data), **no data transformations**, and **no creation of new data models**.

### 1. Analyzing the Source System

Before writing any code, it's crucial to **understand the source system**. This involves:

- **Interviewing source system experts** to gain knowledge about the data's nature, which helps design correct scripts and avoid mistakes.
- **Asking common questions**, including:
    - **Business Context & Ownership**: Understanding the story behind the data and who is responsible for it (e.g., IT departments).
    - **Business Process Supported**: What business process the data supports (e.g., customer transactions, supply chain, finance reporting) to understand its importance.
    - **System & Data Documentation**: Checking for existing documentation (e.g., data models, column descriptions, data catalogs), which serves as learning material and saves time.
    - **Technical Architecture & Technology Stack**: How data is stored (on-premise like SQL Server, Oracle; or cloud like Azure, AWS).
    - **Integration Capabilities**: How data can be extracted (e.g., APIs, Kafka, file extraction, direct database connection).
    - **Data Extraction Strategy**: Whether to perform an **incremental load or a full load**. For the Bronze layer, a full load (truncate and insert) is chosen.
    - **Data Scope & Historization**: What data is needed (e.g., all data, last 10 years) and if historical data is already in the source or needs to be built in the data warehouse.
    - **Expected Size of Extracts**: Understanding data volume (megabytes, gigabytes, terabytes) to ensure the right tools and platform are used.
    - **Data Volume Limitations & Performance Impact**: Assessing if large extracts might degrade the source system's performance, especially for older systems. Being responsible not to impact database performance if direct access is granted.
    - **Authentication & Authorization**: How to access data (tokens, keys, passwords).
- **Understanding metadata and schema** of the incoming data by asking technical experts or exploring the data itself.

### 2. Building Bronze Layer Tables (DDL Scripts)

- **Creating Tables**: Tables are created in the `bronze` schema within the `DataWarehouse` database.
- **Naming Conventions**:
    - **Table names** in the Bronze layer follow the `SourceSystem_Entity` rule (e.g., `CRM_CustomerInfo`, `ERP_ProductInfo`). This allows quick identification of the source system.
    - **Column names** in the Bronze layer are **one-to-one** exactly like the source system's column names (e.g., `ID`, `Key`, `CreateDate`).
- **Robust DDL Scripts**: Include a check to `DROP TABLE` if it `EXISTS` before `CREATE TABLE`. This prevents errors when re-running scripts and ensures a clean table creation from scratch. SQL Server uses `IF OBJECT_ID IS NOT NULL DROP TABLE` where 'U' signifies a user-defined table.

### 3. Data Ingestion using BULK INSERT

- The **`BULK INSERT`** method is chosen for loading data from files (like CSVs) into the database. It's **very fast** because it loads massive amounts of data in one operation, unlike row-by-row inserts.
- **Syntax and Specifications**:
    - `BULK INSERT [Schema].[TableName] FROM 'FilePath'`.
    - The `WITH` clause is used to define file handling specifications:
        - `FIRSTROW = 2`: Skips the header row in the file, as it's not actual data.
        - `FIELDTERMINATOR = ','`: Specifies the delimiter (separator) between fields (e.g., comma, semicolon, pipe, hash).
        - `TABLOCK`: An optional setting to improve performance by locking the entire table during the load operation.
- **Data Quality Checks (Post-Ingestion)**:
    - Verify that data exists in each column and is in the correct column to detect common data shifting errors (e.g., `FirstName` appearing in `Key` column).
    - **Compare row counts**: The number of rows in the loaded Bronze table should be one less than the source file due to skipping the header.
- **Full Load Implementation**: To ensure data is always refreshed and duplicates are avoided, a `TRUNCATE TABLE` command is executed immediately before `BULK INSERT`. This empties the table and loads the entire file content from scratch, making the Bronze layer a **refreshable copy** of the source.

### 4. Stored Procedure Creation and Best Practices

To facilitate daily execution and organization, all bronze layer loading scripts are encapsulated within a **Stored Procedure**.

- **Naming Convention**: The stored procedure is named `load_bronze` and is placed in the `bronze` schema (e.g., `bronze.load_bronze`).
- **Improved Messaging**: The stored procedure includes `PRINT` statements to provide clear output messages during execution:
    - Main message: "Loading the bronze layer".
    - Section separators for each source system (e.g., "Loading CRM tables", "Loading ERP tables").
    - Action-specific messages for each table (e.g., "Truncating table...", "Inserting data into..."). This improves debugging clarity.
- **Error Handling (`TRY...CATCH`)**:
    - The core logic is wrapped in a `BEGIN TRY...END TRY` block.
    - A `BEGIN CATCH...END CATCH` block is used to handle errors. In case of failure, it can print informative messages like `ERROR_MESSAGE()`, `ERROR_NUMBER()`, and `ERROR_STATE()` functions. It can also be designed to log errors to a table.
- **Performance Monitoring (Load Duration)**:
    - **Importance**: Measuring execution time is crucial for large data warehouses to identify bottlenecks and optimize performance.
    - **Implementation**:
        - Declare `start_time` and `end_time` variables of `DATETIME` type.
        - Set `start_time = GETDATE()` before beginning the load for each table and `end_time = GETDATE()` after its completion.
        - Calculate the duration using `DATEDIFF(second, start_time, end_time)` and print the `Load Duration` for each table.
        - Similarly, calculate and print the `Total Load Duration` for the entire bronze layer batch. While local execution might show 0 seconds due to speed, in real-world scenarios with different servers and larger data, this will be significant.

### 5. Data Flow Diagram and Git Commit

- **Data Flow Diagram (DFD)**:
    - A simple visual diagram is created to **map the flow of data**, showing where it originates and where it lands.
    - It helps create **data lineage**, which is essential for analyzing issues and understanding the origin of data across multiple layers.
    - The diagram visually connects source systems (e.g., CRM, ERP folders with their respective files) to the corresponding tables within the Bronze layer.
- **Committing Code to Git Repository**:
    - The developed DDL scripts and the stored procedure script are committed to the Git repository.
    - A structured folder system is used (e.g., `scripts/bronze/`).
    - Each script includes a **header comment** explaining its purpose, parameters (if any), and an example of how to execute it.
    - Using Git provides a safe place to store code, track changes, enable collaboration, allow rollbacks, and serve as a portfolio piece.

This comprehensive approach demonstrates how to **engineer a complete ETL pipeline**, focusing not just on loading data but also on organization, debugging, performance measurement, and error handling for a professional data warehouse.

## SQL Project 8: Build The Silver Layer - Clean & Transform Data | Data Engineer Portfolio Project

This lecture focuses on **building the Silver Layer** in a data engineering project, which is the crucial stage for **cleansing and transforming raw data** from the Bronze layer to prepare it for further analysis and reporting. The main objective of the Silver layer is to have **clean and standardized data**.

The process for building the Silver Layer is structured into several key phases:
### 1. Analyzing and Exploring Data in the Bronze Layer

Before initiating any coding for the Silver layer, it is paramount to **explore and understand the content of the data** residing in the Bronze layer. Unlike the Bronze layer, where the focus was solely on data ingestion, the Silver layer requires a deep understanding of the data's content, relationships between tables, and potential quality issues.

Key aspects of this analysis include:

- **Understanding Data Content and Relationships**: Exploring tables (e.g., `CRM_CustomerInfo`, `ERP_ProductInfo`, `CRM_SalesDetails`) to grasp their content and how they relate to each other. This involves querying a sample of data, such as `SELECT TOP 1000` rows, to avoid impacting the system with large queries.
- **Creating Documentation (Data Model/Integration Model)**: It is highly recommended to visually document the data model and the relationships discovered. This helps to consolidate understanding and serves as a reference, preventing forgetting details after a while. Examples from the lecture show documenting `CRM_CustomerInfo`, `ERP_ProductInfo`, and `CRM_SalesDetails` tables, including their primary keys and how they connect (e.g., `Product Key` for `SalesDetails` to `ProductInfo`, `Customer ID` for `SalesDetails` to `CustomerInfo`, `Customer Key` from `ERP_Cost` to `CRM_CustomerInfo`). It was also observed that `ERP_ProductInfo` contains historical data for product costs, indicated by `Start` and `End` dates.
- **Identifying Data Characteristics**: This includes noting low cardinality columns (e.g., `Marital Status`, `Gender`, `Product Line`, `Country`, `Category`, `Subcategory`, `Maintenance`) where consistency checks are crucial, and identifying columns that can be used for joins (e.g., `Product Key`, `Customer ID`).

### 2. Building Silver Layer Tables (DDL Scripts)

The Silver layer will contain tables that are generally **identical in structure to the Bronze layer**, with few modifications.

- **Naming Conventions**: Tables reside in the `silver` schema.
- **Full Load Strategy**: The way data is loaded from Bronze to Silver is a **full load**, meaning the table is `TRUNCATE`d and then new data is `INSERT`ed. This ensures data is always refreshed and prevents duplicates.
- **Metadata Columns**: A crucial addition to every table in the Silver layer (and generally in a data warehouse) are **metadata columns**. These columns are not from source systems but are added by data engineers to provide extra information for each record.
    - **Purpose**: They are a great tool for tracking data issues, understanding data lineage (from which file/source data originated), identifying gaps, and facilitating debugging.
    - **Naming Convention**: They follow a `DW_` prefix (e.g., `DW_create_date`).
    - **Automation**: Columns like `DW_create_date` are often automatically populated by the database using `GETDATE()` as a `DEFAULT` value, so they don't need to be specified in ETL scripts.
- **DDL Modification**: While largely copied from Bronze, DDL scripts for Silver tables may need adjustments for:
    - **Schema change**: `bronze.TableName` becomes `silver.TableName`.
    - **Adding metadata columns** (e.g., `DW_create_date DATETIME2 DEFAULT GETDATE()`).
    - **New derived columns**: If new columns are derived during transformation (e.g., `Category ID` from `Product Key`), they must be added to the DDL.
    - **Data type changes**: If data types are transformed (e.g., `DATETIME` to `DATE`, `INTEGER` to `DATE`), the DDL must reflect these changes.

### 3. Data Transformation and Cleansing

This is the core activity of the Silver layer. The approach is to first **detect data quality issues** in the Bronze layer, and **only then write transformations** to fix them. The lecture covers various types of data transformations:

- **1. Removing Duplicates**:
    - **Issue**: Primary keys with duplicate values or `NULL`s.
    - **Detection**: Aggregate the primary key and use `HAVING COUNT > 1` or `OR PrimaryKey IS NULL`.
    - **Transformation**: Use **Window Functions** like `ROW_NUMBER() OVER (PARTITION BY PrimaryKey ORDER BY CreateDate DESC)`. This allows picking the **latest record** for a duplicate primary key by sorting by a timestamp (e.g., `Creation Date`). This is a type of **data filtering**.
- **2. Handling Unwanted Spaces (Trimming)**:
    - **Issue**: Leading or trailing spaces in string values.
    - **Detection**: Compare the original string to its `TRIM()`ed version (`ColumnName <> TRIM(ColumnName)`).
    - **Transformation**: Apply the `TRIM()` function to the string columns (e.g., `TRIM(FirstName)`, `TRIM(LastName)`).
- **3. Data Normalization/Standardization**:
    - **Issue**: Coded values or abbreviations (e.g., 'F' for Female, 'M' for Male, 'DE' for Germany).
    - **Transformation**: Use `CASE WHEN` statements to **map coded values to meaningful, user-friendly descriptions** (e.g., `CASE WHEN Gender = 'F' THEN 'Female' WHEN Gender = 'M' THEN 'Male' ELSE 'Not Available' END`). It's a good practice to use `UPPER()` and `TRIM()` on the source column within the `CASE WHEN` to handle varying cases or hidden spaces. A "quick form" of `CASE WHEN` can be used for simple direct mappings.
- **4. Handling Missing Values**:
    - **Issue**: `NULL`s, empty strings, or zeros in columns where they are not expected.
    - **Transformation**: Replace missing values with a **standard default value** (e.g., 'Not Available', 'Unknown', '0'). Functions like `ISNULL()` can be used for this. For zeros, `NULLIF()` can convert them to `NULL` before further handling.
- **5. Deriving New Columns**:
    - **Issue**: Needed information is embedded within an existing column or needs to be calculated.
    - **Transformation**: Create new columns based on calculations or transformations of existing ones. Examples include:
        - Extracting `Category ID` from `Product Key` using `SUBSTRING()` (`SUBSTRING(ProductKey, 1, 5)`).
        - Extracting the rest of the `Product Key` dynamically using `SUBSTRING()` and `LEN()` (`SUBSTRING(ProductKey, 7, LEN(ProductKey))`).
        - Removing unwanted parts of an ID like 'NAS' prefix using `SUBSTRING()` with `CASE WHEN`.
- **6. Data Type Casting**:
    - **Issue**: Incorrect data types (e.g., dates stored as integers, datetime with unnecessary time component).
    - **Transformation**: Convert data types using `CAST()`. For example, casting an `INTEGER` date (like `YYYYMMDD`) to `DATE` might require an intermediate `VARCHAR` cast in SQL Server (`CAST(CAST(OrderDate AS VARCHAR) AS DATE)`). Casting `DATETIME` to `DATE` to remove time components when only the date is relevant.
- **7. Handling Invalid Data / Business Rules**:
    - **Issue**: Data that violates business rules (e.g., negative costs, end dates before start dates, future birthdates, incorrect calculations like `Sales != Quantity * Price`).
    - **Transformation**: Implement business logic using `CASE WHEN` and other functions to correct or flag invalid data. Examples include:
        - Replacing negative costs with `0` or `NULL`.
        - Fixing overlapping historical dates: using `LEAD()` window function to calculate the `EndDate` based on the `StartDate` of the _next_ record (minus one day) to ensure no overlaps. This is also an example of **data enrichment**, adding value to the data.
        - Invalid date ranges (e.g., `OrderDate > ShippingDate`, `BirthDate > GETDATE()`) can be transformed to `NULL` or corrected based on rules.
        - Recalculating `Sales` or `Price` based on the `Quantity * Price` rule, handling `NULL`s, zeros, or negative values. The `ABS()` function can convert negative numbers to positive for calculations. `NULLIF(Quantity, 0)` can prevent division by zero.
        - Removing specific unwanted characters (e.g., hyphen in `ERP_Location`'s `CID`) using `REPLACE()`.

After transformations, it's crucial to **re-check the data quality in the Silver layer** using the same quality checks performed on the Bronze layer. This validates that the transformations have successfully resolved the issues.

### 4. Stored Procedure Creation and Best Practices

To organize and automate the Silver layer loading process, all cleansing and loading scripts are encapsulated within a **Stored Procedure**.

- **Naming Convention**: The stored procedure is typically named `silver.load_silver`.
- **Encapsulation**: The procedure contains all the `TRUNCATE TABLE` and `INSERT INTO` statements for each Silver table.
- **Best Practices (Mirroring Bronze Layer)**:
    - **Truncate and Insert**: Each `INSERT` statement for a Silver table is preceded by a `TRUNCATE TABLE` to ensure a full load and prevent duplicates.
    - **Improved Messaging**: `PRINT` statements provide clear output messages, indicating the layer being loaded, individual source systems, tables being processed, and specific actions (e.g., "Truncating table...", "Inserting data into...").
    - **Error Handling (`TRY...CATCH`)**: The core logic is wrapped in `BEGIN TRY...END TRY` and `BEGIN CATCH...END CATCH` blocks to gracefully handle and log errors (e.g., printing `ERROR_MESSAGE()`, `ERROR_NUMBER()`, `ERROR_STATE()`).
    - **Performance Monitoring**: `start_time` and `end_time` variables are used with `GETDATE()` and `DATEDIFF()` to calculate and print the `Load Duration` for each table and the total Silver layer load, which is critical for large data volumes.
    - **Consistency**: It's vital to **maintain consistent standards** across all stored procedures (e.g., `load_bronze`, `load_silver`). Any new ideas or redesigns in one procedure should be applied to others to ensure uniformity and ease of understanding for other developers.

### 5. Documentation and Git Commit

The final steps involve updating documentation and committing the code to a Git repository.

- **Extending the Data Flow Diagram (DFD)**: The existing DFD from the Bronze layer is extended to include the Silver layer. This involves visually connecting tables from the Bronze layer to their corresponding tables in the Silver layer, using distinct coloring (e.g., gray for Silver). This creates a **clear data lineage**, allowing quick understanding of data flow across layers without needing to examine scripts.
- **Committing Code to Git**:
    - The developed DDL scripts for the Silver layer (e.g., in `scripts/silver/`) are committed.
    - The stored procedure script for loading the Silver layer is committed.
    - **Quality Check Queries**: Importantly, the queries used to check the quality of the Silver layer are also committed to the repository, often in a dedicated `tests/quality_checks_silver` folder. These serve as reusable tools for ongoing data quality validation.
    - All committed scripts include **header comments** explaining their purpose, parameters, and usage examples.

This structured approach ensures that the Silver layer provides a robust, clean, and standardized dataset, ready for the next stage: the Gold layer, which will involve business rules, aggregations, and integrations. The overall data warehouse flow involves running the Bronze layer load first, followed by the Silver layer load, effectively moving and transforming data through the layers.
