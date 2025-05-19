
# COVID-19 Reporting Project using Azure Data Factory

This project demonstrates how Azure Data Factory (ADF) is used to orchestrate data ingestion, transformation, and publishing for COVID-19 reporting, powered by Azure services such as Blob Storage, Data Lake Storage Gen2, and Azure SQL Database.

## 🧩 Architecture Overview

The solution ingests data from the ECDC website and population datasets stored in Azure Blob. These are processed and stored in Azure Data Lake Gen2. ADF Data Flows handle transformation logic, with final output written to Azure SQL Database for reporting.

## 🚀 Ingestion Pipelines

There are dedicated pipelines for ingesting population data and ECDC COVID-19 statistics. The ECDC ingestion uses a `Lookup` and `ForEach` pattern to dynamically pull multiple files from HTTP endpoints and load them into Data Lake.

[![Ingestion Flow](/images/Covid19ReportingADF/Screenshot%20(89).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(89).png?raw=true)
[![Ingestion Validation](/images/Covid19ReportingADF/Screenshot%20(90).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(90).png?raw=true)

## 🛠 Data Transformation

Two data flows are used:

**Cases & Deaths Data Flow** filters for Europe, selects required columns, performs a pivot, enriches data with country codes from a lookup file, and loads into a processed dataset.

[![Transform Cases Data Flow](/images/Covid19ReportingADF/Screenshot%20(85).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(85).png?raw=true)

**Hospital Admissions Data Flow** enriches and splits data into weekly and daily summaries using aggregation, sorting, pivoting, and sink transformations.

[![Transform Hospital Admissions Flow](/images/Covid19ReportingADF/Screenshot%20(86).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(86).png?raw=true)

Both data flows use a country lookup dataset pointing to a CSV file in the Azure Data Lake.

[![Country Lookup Dataset](/images/Covid19ReportingADF/Screenshot%20(87).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(87).png?raw=true)

## 🧪 Processing Pipelines

These pipelines trigger the respective data flows, running them on AutoResolveIntegrationRuntime with configurable compute sizes and verbose logging.

[![Processing Flow](/images/Covid19ReportingADF/Screenshot%20(91).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(91).png?raw=true)

## 🗃 SQL Export

Two pipelines prepare data for export to SQLite, using wildcard datasets to collect all processed files and make them ready to import into SQL database.

[![SQLite Case Export](/images/Covid19ReportingADF/Screenshot%20(93).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(93).png?raw=true)

## ✅ Monitoring

Monitoring of pipeline executions is shown using ADF Studio's runtime views, with status on each activity including lookup, copy, and ForEach executions.

[![Pipeline Monitoring](/images/Covid19ReportingADF/Screenshot%20(94).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(94).png?raw=true)

## 📦 Data Sources

- COVID-19 case and death data from ECDC
- Hospital admissions from ECDC
- Population by age from Eurostat

## 🔌 Linked Services

The project uses four key linked services that connect ADF to various data sources and sinks:

- Azure Blob Storage (`ls_ablob_testcovid19sa`) for source population data.
- Azure Data Lake Gen2 (`ls_adl_testcovid19dl`) for raw and processed storage.
- HTTP (`ls_http_opendata_ecdc_europe_eu`) to ingest ECDC COVID-19 data.
- Azure SQL Database (`ls_testcovid19db`) as the final reporting database.

[![Linked Services](/images/Covid19ReportingADF/Screenshot%20(95).png?raw=true)](/images/Covid19ReportingADF/Screenshot%20(95).png?raw=true)
