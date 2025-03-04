# SSIS & SQL Server Data Warehousing Project

## Overview
This project is an SSIS (SQL Server Integration Services) ETL (Extract, Transform, Load) solution for ServiceSpot, an IT company that seeks an optimized Data Warehouse to analyze its call center operations. Our solution extracts raw call data, processes and cleanses it, and loads it into a structured data warehouse for insightful reporting.

## Additional Documentation
For a comprehensive breakdown of the project, including detailed execution steps, database schema design, and data processing techniques, refer to the project report: [**SSIS_Project_Report_A23_report.docx**](https://github.com/nguyenpham0297/etl-call-center-data/blob/main/2.%20Solution/SSIS_Project_Report_A23%20_%20report.docx).

## Project Structure
The ETL pipeline consists of three key stages:
1. **Staging Area (STA):** Raw data ingestion from CSV files into SQL Server tables.
2. **Operational Data Store (ODS):** Data cleansing, transformation, and standardization.
3. **Data Warehouse (DWH):** Star schema database for efficient querying and reporting.

## Technologies Used
- **SQL Server** for database management
- **SSIS** for ETL pipeline implementation
- **Visual Studio** for SSIS package development

## Data Sources
- **Call Data (Main Data):** CSV files containing call records from 2018–2020.
- **Lookup Data:** Supplementary datasets including Employees, Call Types, US States, and Call Charges.

## ETL Pipeline Details
### 1. Staging Area (STA)
- Data is loaded into staging tables without transformations.
- Used Foreach Loop Container to process multiple yearly CSV files.
- Implemented truncation before loading to avoid duplicate records.

### 2. Operational Data Store (ODS)
- **Data Cleaning:** Standardized column lengths and data types.
- **Data Transformations:**
  - Split Site column into CityName and StateID.
  - Lookup operations for Employee and Call Type details.
  - Unpivoted Call Charges data for a structured format.
  - Created SLA (Service Level Agreement) status based on wait time.
- **Error Handling:**
  - Invalid records redirected to a `Technical_Rejects` table in the ADM (Administrative) database.

### 3. Data Warehouse (DWH)
- **Schema Design:** Implemented a **Star Schema** with:
  - **Fact Table:** `FactCallData`
  - **Dimension Tables:** `DimEmployees`, `DimDate`, `DimCallCharges`
- **Surrogate Keys:** Used for historical tracking and efficient joins.
- **Truncation Strategy:** Ensured no duplicate data in the Fact table.

## SSIS Packages
The solution consists of the following `.dtsx` SSIS packages:
1. **STA_CallData.dtsx** – Loads call data into the staging area.
2. **STA_CallCharges.dtsx** – Loads call charges.
3. **STA_CallTypes.dtsx** – Loads call type details.
4. **STA_Employees.dtsx** – Loads employee data.
5. **STA_USStates.dtsx** – Loads state details.
6. **ODS_Transformation.dtsx** – Cleans and processes data into ODS.
7. **DWH_Load.dtsx** – Loads transformed data into the Data Warehouse.

## Results & Achievements
- **82724 rows** successfully loaded into the Fact Table with no duplicates.
- Cleaned and standardized data ensures accurate reporting.
- A scalable ETL pipeline that supports future data ingestion.

## Installation & Deployment
To deploy the project, open `Data_Warehousing_A23_Group.sln` in Visual Studio and execute the SSIS packages sequentially. Ensure SQL Server is configured and the necessary databases (`STA`, `ODS`, `DWH`) are created beforehand.

## Contributors
- **Mohammed Danish Mustafa** – Staging Area (STA)
- **Patrick Warui Githendu** – Staging Area (STA)
- **Phuc Nguyen Pham** – Operational Data Store (ODS)
- **Trung Nguyen** – Data Warehouse (DWH)

---
This project provides a robust ETL framework for ServiceSpot’s call center analytics, ensuring data integrity and insightful reporting.

