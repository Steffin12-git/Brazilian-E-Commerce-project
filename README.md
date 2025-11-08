# \# 🛒 Brazilian E-Commerce Project (Olist)

# 

# \### 🚀 \*End-to-End Azure Data Engineering Pipeline Using ADF | ADLS Gen2 | Databricks | Synapse | Power BI\*

# 

# ---

# 

# \## 📖 Project Overview

# 

# This project demonstrates a \*\*complete cloud-based data engineering workflow\*\* using the \*\*Brazilian E-Commerce Public Dataset by Olist\*\*.

# It integrates \*\*multiple Azure services\*\* to ingest, transform, enrich, and visualize e-commerce data in a \*\*Medallion Architecture\*\* (Bronze → Silver → Gold).

# 

# Data is ingested from various sources — \*\*GitHub, MySQL, MongoDB\*\* — and processed through a pipeline built using \*\*Azure Data Factory\*\*, \*\*Azure Databricks\*\*, \*\*Azure Synapse Analytics\*\*, and finally visualized in \*\*Power BI\*\*.

# 

# ---

# 

# \## 🧩 Project Architecture

# 

# !\[Project Structure](Structure%20and%20flow/Project%20Structure.png)

# 

# \*\*Architecture Flow\*\*

# 

# 1\. \*\*Data Sources\*\* → GitHub (JSON), SQL DB (MySQL via Files.io), NoSQL (MongoDB via Files.io)

# 2\. \*\*Azure Data Factory\*\* → Extracts and ingests data into ADLS Gen2 (Bronze)

# 3\. \*\*Azure Databricks\*\* → Transforms \& enriches data (Silver)

# 4\. \*\*Azure Synapse Analytics\*\* → Models \& aggregates data (Gold)

# 5\. \*\*Power BI\*\* → Connects to Synapse for visualization and reporting

# 

# ---

# 

# \## 🧠 Technologies \& Tools Used

# 

# | Category                     | Tools / Services                              |

# | ---------------------------- | --------------------------------------------- |

# | \*\*Cloud Platform\*\*           | Microsoft Azure                               |

# | \*\*Storage\*\*                  | Azure Data Lake Storage Gen2                  |

# | \*\*Orchestration\*\*            | Azure Data Factory (ADF)                      |

# | \*\*Processing\*\*               | Azure Databricks with Apache Spark            |

# | \*\*Data Warehouse\*\*           | Azure Synapse Analytics (Serverless SQL Pool) |

# | \*\*Visualization\*\*            | Power BI                                      |

# | \*\*Databases\*\*                | MySQL (Filess.io)  •  MongoDB (Filess.io)     |

# | \*\*Version Control / Source\*\* | GitHub (HTTP JSON metadata + datasets)        |

# 

# ---

# 

# \## 🗂 Dataset Description

# 

# Dataset: \*\*\[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)\*\*

# 

# | File                                    | Description                                 |

# | --------------------------------------- | ------------------------------------------- |

# | `olist\_customers\_dataset.csv`           | Customer details                            |

# | `olist\_geolocation\_dataset.csv`         | Geographical mapping                        |

# | `olist\_order\_items\_dataset.csv`         | Products in each order                      |

# | `olist\_order\_payments\_dataset.csv`      | Payment methods and values                  |

# | `olist\_order\_reviews\_dataset.csv`       | Customer reviews and ratings                |

# | `olist\_orders\_dataset.csv`              | Main order information                      |

# | `olist\_products\_dataset.csv`            | Product metadata                            |

# | `olist\_sellers\_dataset.csv`             | Seller details                              |

# | `product\_category\_name\_translation.csv` | Category translations (loaded from MongoDB) |

# 

# ---

# 

# \## ☁️ Azure Setup \& Account Structure

# 

# !\[Azure Account Classification](Structure%20and%20flow/Azure%20account%20classifiation.png)

# 

# All resources were organized under a single \*\*Resource Group\*\* within an Azure subscription using a structured hierarchy:

# 

# \* \*\*Subscription Type:\*\* Azure Free Trial (upgraded to Pay-As-You-Go with Spending Cap)

# \* \*\*Resources Created:\*\*

# 

# &nbsp; \* Azure Data Factory

# &nbsp; \* Azure Data Lake Storage Gen2

# &nbsp; \* Azure Databricks (Workspace + Compute)

# &nbsp; \* Azure Synapse Analytics (Workspace + Serverless SQL Pool)

# &nbsp; \* Power BI Service connection

# 

# ---

# 

# \## 🧱 Medallion Architecture

# 

# !\[Medallion Architecture](Structure%20and%20flow/medallion%20architecture.png)

# 

# | Layer      | Purpose                                          | Storage Format  |

# | ---------- | ------------------------------------------------ | --------------- |

# | \*\*Bronze\*\* | Raw data ingestion from ADF                      | CSV             |

# | \*\*Silver\*\* | Cleaned and transformed data from Databricks     | Parquet         |

# | \*\*Gold\*\*   | Aggregated and business-ready tables via Synapse | Parquet / Views |

# 

# ---

# 

# \## 🔁 Data Pipeline Flow

# 

# \### 1️⃣ Azure Data Factory – Data Ingestion

# 

# \* \*\*Linked Services\*\*

# 

# &nbsp; \* GitHub (JSON containing file URLs)

# &nbsp; \* MySQL (Filess.io)

# &nbsp; \* ADLS Gen2 (for storage output)

# 

# \* \*\*Workflow Pipeline\*\*

# 

# &nbsp; \* Lookup → reads JSON metadata from GitHub

# &nbsp; \* ForEach Activity → iterates over file list

# &nbsp; \* Copy Data → dynamically copies each CSV to ADLS Gen2 Bronze folder

# &nbsp; \* Separate Copy Data activity for MySQL data

# 

# 🗃 \*\*Output:\*\* All raw files land in `/bronze` container.

# 

# ---

# 

# \### 2️⃣ Azure Databricks – Data Transformation \& Enrichment

# 

# \* Connected Databricks to ADLS using Unity Catalog and Managed Identity.

# \* Read CSV files from Bronze → performed data cleaning and joins using PySpark.

# \* Installed and used `pymongo` to connect to MongoDB and load the translation dataset.

# \* Combined all datasets into a final DataFrame using Spark joins on `order\_id`, `customer\_id`, `product\_id`, and `seller\_id`.

# \* Wrote cleaned data to Silver layer in Parquet format.

# 

# 🪶 \*\*Output:\*\* `/silver` container with clean and joined datasets.

# 

# ---

# 

# \### 3️⃣ Azure Synapse Analytics – Data Modeling \& Aggregation

# 

# \* Created a Serverless SQL Database.

# \* Configured \*\*External Data Source\*\*, \*\*File Format\*\*, and \*\*Database Scoped Credential\*\* (using Managed Identity).

# \* Queried data from ADLS Silver and created \*\*views\*\* and \*\*aggregated tables\*\*.

# \* Saved final business data into the Gold folder.

# 

# 🪙 \*\*Output:\*\* `/gold` container ready for reporting.

# 

# ---

# 

# \### 4️⃣ Power BI – Visualization \& Insights

# 

# \* Connected Power BI to Synapse using \*\*Serverless SQL Endpoint\*\*.

# \* Loaded data from Gold views for dashboards and KPIs.

# \* Visualized sales performance, delivery patterns, payment trends, and customer satisfaction.

# 

# 🧩 \*\*Visualization Folder:\*\* `/visulisation`

# 

# ---

# 

# \## 🔗 Dataset Schema Model

# 

# !\[Dataset Schema Model](Structure%20and%20flow/Dataset%20schema%20model.png)

# 

# This ER diagram illustrates how datasets are joined on `order\_id`, `customer\_id`, `seller\_id`, and `product\_id`.

# 

# ---

# 

# \## 📚 Folder Structure

# 

# ```

# Brazilian-E-Commerce-project/

# │

# ├── Azure input file/                 → JSON metadata and scripts

# ├── notebook/                         → Databricks notebooks (Spark, PyMongo)

# ├── Raw dataset/                      → Original Kaggle CSV files

# ├── Structure and flow/               → Architecture and pipeline images

# │     ├── Azure account classifiation.png

# │     ├── Azure data factory.png

# │     ├── Dataset schema model.png

# │     ├── medallion architecture.png

# │     └── Project Structure.png

# ├── visulisation/                     → Power BI dashboards and exports

# └── README.md                         → Project documentation

# ```

# 

# ---

# 

# \## 🧮 Key Learnings

# 

# \* Implementing \*\*Medallion Architecture\*\* with ADLS Gen2

# \* Dynamic pipeline creation in ADF using parameters and ForEach

# \* Managed Identity authentication between Azure services

# \* Data transformation in Databricks with PySpark and MongoDB integration

# \* Building a Serverless SQL Data Warehouse in Synapse

# \* Connecting Power BI to Synapse for live analytics

# 

# ---

# 

# \## 🚀 Future Enhancements

# 

# \* Automate pipeline trigger with event-based scheduling

# \* Add data-quality checks in ADF and Databricks

# \* Use Azure Monitor for pipeline logging and alerts

# \* Extend visualizations to Azure Fabric or Tableau

# \* Implement ML models in Databricks for sales prediction

# 

# ---

# 

# \## 🙌 Acknowledgment

# 

# Dataset credit: \[Olist – Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

# 

# Project executed and documented by \*\*Steffin Thomas\*\*

# 

# ---

