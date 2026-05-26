
# olist-medallion-pipeline
End-to-end medallion architecture using ADF + ADB + PySpark + Delta Lake
# 🏗️ Olist E-Commerce Medallion Pipeline

End-to-end data engineering project implementing 
medallion architecture on Azure.

## 🛠️ Tech Stack
- **Orchestration** : Azure Data Factory (ADF)
- **Transformation** : Azure Databricks (ADB) + PySpark
- **Storage**        : Azure Data Lake Storage Gen2
- **Format**         : Delta Lake (Bronze / Silver / Gold)
- **Source Data**    : Olist Brazilian E-Commerce (Kaggle)

## 🏛️ Architecture
CSV Files (Kaggle)
↓
ADLS Gen2 (Bronze Raw)
↓ ADF Copy Activity
ADLS Gen2 (Bronze Parquet)
↓ ADB PySpark Notebook
ADLS Gen2 (Bronze Delta)
↓ ADB PySpark Notebook
ADLS Gen2 (Silver Delta)
↓ ADB PySpark Notebook
ADLS Gen2 (Gold Delta)
↓
Power BI Dashboard

## 📁 Project Structure

├── adf/                    # ADF pipeline JSON templates
│   ├── pipeline/
│   ├── dataset/
│   └── linkedService/
├── databricks/             # PySpark notebooks
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── data/sample/            # Sample data for testing
└── docs/                   # Architecture diagrams

## 🥉 Bronze Layer
- Ingests 9 raw CSV files from ADLS
- Converts CSV → Parquet → Delta format
- Adds audit metadata columns
- Registers as Hive tables

## 🥈 Silver Layer
- Deduplicates and cleanses all tables
- Joins orders + customers + payments + reviews
- Adds business flags (is_late_delivery, delivery_delay_days)
- Outputs 2 analysis-ready Delta tables

## 🥇 Gold Layer
- **Revenue Mart** : Monthly trends, state analysis, payment breakdown
- **RFM Mart**     : Customer segmentation (Champions → Lost)
- **Product Mart** : Category and product performance

## 📊 Dataset
- Source : [Olist Brazilian E-Commerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- Size   : ~120MB, 9 CSV files, 100K+ orders

## 🚀 How to Run
1. Clone this repo
2. Upload CSVs to ADLS bronze/raw/ folders
3. Configure ADF Linked Services
4. Run PL_Master_Orchestrator pipeline
5. Validate Gold tables in ADB

