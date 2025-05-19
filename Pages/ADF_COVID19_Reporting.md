# COVID-19 Reporting Project using Azure Data Factory

This project demonstrates how Azure Data Factory (ADF) is used to orchestrate data ingestion, transformation, and publishing for COVID-19 reporting, powered by Azure services such as Blob Storage, Data Lake Storage Gen2, and Azure SQL Database.

## 🧩 Architecture Overview

The solution ingests data from the ECDC website and population datasets stored in Azure Blob. These are processed and stored in Azure Data Lake Gen2. ADF Data Flows handle transformation logic, with final output written to Azure SQL Database for reporting.

## 🚀 Ingestion Pipelines

There are dedicated pipelines for ingesting population data and ECDC COVID-19 statistics. The ECDC ingestion uses a `Lookup` and `ForEach` pattern to dynamically pull multiple files from HTTP endpoints and load them into Data Lake.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(89).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(89).png?raw=true" alt="Ingestion Flow" />
  </a>
</div>


<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(90).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(90).png?raw=true" alt="Ingestion Validation" />
  </a>
</div>

## 🛠 Data Transformation

Two data flows are used:

**Cases & Deaths Data Flow** filters for Europe, selects required columns, performs a pivot, enriches data with country codes from a lookup file, and loads into a processed dataset.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(85).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(85).png?raw=true" alt="Transform Cases Data Flow" />
  </a>
</div>

**Hospital Admissions Data Flow** enriches and splits data into weekly and daily summaries using aggregation, sorting, pivoting, and sink transformations.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(86).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(86).png?raw=true" alt="Transform Hospital Admissions Flow" />
  </a>
</div>

Both data flows use a country lookup dataset pointing to a CSV file in the Azure Data Lake.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(87).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(87).png?raw=true" alt="Country Lookup Dataset" />
  </a>
</div>

## 🧪 Processing Pipelines

These pipelines trigger the respective data flows, running them on AutoResolveIntegrationRuntime with configurable compute sizes and verbose logging.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(91).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(91).png?raw=true" alt="Processing Flow" />
  </a>
</div>

## 🗃 SQL Export

Two pipelines prepare data for export to SQLite, using wildcard datasets to collect all processed files and make them ready to import into SQL database.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(93).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(93).png?raw=true" alt="SQLite Case Export" />
  </a>
</div>

## ✅ Monitoring

Monitoring of pipeline executions is shown using ADF Studio's runtime views, with status on each activity including lookup, copy, and ForEach executions.

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(94).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(94).png?raw=true" alt="Pipeline Monitoring" />
  </a>
</div>

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

<div style="border: 2px solid #ccc; padding: 5px; display: inline-block;">
  <a href="/images/Covid19ReportingADF/Screenshot%20(95).png?raw=true">
    <img src="/images/Covid19ReportingADF/Screenshot%20(95).png?raw=true" alt="Linked Services" />
  </a>
</div>
