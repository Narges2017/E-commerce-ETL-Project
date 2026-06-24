# 🛒 E-commerce ETL Project


[![Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Lakehouse-blue)](https://learn.microsoft.com/fabric/)
[![Spark](https://img.shields.io/badge/Apache%20Spark-Delta%20Lake-orange)](https://spark.apache.org/)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)


An end-to-end **Extract, Transform, Load (ETL)** pipeline for e-commerce data built on **Microsoft Fabric Lakehouse** using the **Medallion 
Architecture** (Bronze → Silver → Gold layers).


---


## 📌 Project Overview


This project demonstrates a modern data engineering workflow for processing e-commerce transaction data:


- **Ingest** raw data into the **Bronze** layer
- **Clean & transform** data in the **Silver** layer  
- **Model** data into a star schema (**Fact + Dimensions**) in the **Gold** layer


The pipeline is designed to run in **Microsoft Fabric** notebooks with **Apache Spark** and **Delta Lake**.


---


## 🏗️ Architecture


```
Raw Data (CSV/Parquet)
        ↓
   ┌─────────────┐
   │   Bronze    │  ← Raw ingested data (save_as_bronze.ipynb)
   └─────────────┘
        ↓
   ┌─────────────┐
   │   Silver    │  ← Cleaned & enriched data (process_data.ipynb)
   └─────────────┘
        ↓
   ┌─────────────┐
   │    Gold     │  ← Star schema (Fact + Dimensions) (create_fact_and_dims.ipynb)
   └─────────────┘
```


---


## 🛠️ Technologies Used


- **Microsoft Fabric** (Lakehouse + Notebooks)
- **Apache Spark** (PySpark)
- **Delta Lake** (ACID transactions, time travel)
- **Medallion Architecture** (Bronze / Silver / Gold)
- **Jupyter Notebooks**


---


## 📁 Project Structure


```
E-commerce-ETL-Project/
├── notebooks/
│   ├── save_as_bronze.ipynb          # Ingest raw data into Bronze layer
│   ├── process_data.ipynb            # Clean & transform data (Silver layer)
│   └── create_fact_and_dims.ipynb    # Build Fact & Dimension tables (Gold layer)
├── pipelines/                        # (Optional) Data pipelines / orchestration
├── reports/                          # Power BI reports or dashboards
├── docs/                             # Documentation & diagrams
├── .gitignore
└── README.md
```


---


## ✅ Prerequisites


- Microsoft Fabric workspace with **Lakehouse** item
- Appropriate **Fabric capacity** (F8 or higher recommended for development)
- Source e-commerce dataset (e.g., transactions, customers, products)
- Basic knowledge of PySpark and Delta Lake


---


## 🚀 How to Run


### 1. Setup in Microsoft Fabric


1. Create a new **Lakehouse** in your Fabric workspace.
2. Attach the Lakehouse to a new **Notebook**.
3. Upload your source data (CSV/Parquet) into the Lakehouse **Files** section or use shortcuts.


### 2. Run the Notebooks (in order)


| Order | Notebook                        | Purpose                              | Recommended Mode      |
|-------|----------------------------------|--------------------------------------|-----------------------|
| 1     | `save_as_bronze.ipynb`          | Load raw data into Bronze layer     | `mode("overwrite")`   |
| 2     | `process_data.ipynb`            | Clean, validate, enrich data        | -                     |
| 3     | `create_fact_and_dims.ipynb`    | Create Fact & Dimension tables      | -                     |


> **Important**: Always use `.mode("overwrite")` or `CREATE OR REPLACE TABLE` when rerunning notebooks to avoid `TABLE_OR_VIEW_ALREADY_EXISTS` e


### 3. Capacity Tips (Common Issue)


If you see **`TooManyRequestsForCapacity`** error:
- Go to **Monitoring hub** → Cancel stuck Spark jobs
- Check **Workspace settings → Job management**
- Wait 2–5 minutes and retry
- Consider using a larger capacity (F32+) during active development


---


## 📊 Notebooks Description


### 1. `save_as_bronze.ipynb`
- Reads raw e-commerce transaction files
- Saves them as a Delta table: `bronze_transactions`
- Adds metadata columns (`_ingest_timestamp`, source file, etc.)


### 2. `process_data.ipynb`
- Data quality checks and cleaning
- Handling nulls, duplicates, data type casting
- Business logic enrichment
- Output to Silver layer tables


### 3. `create_fact_and_dims.ipynb`
- Dimensional modeling (Kimball methodology)
- Creates:
  - Fact table(s) (e.g., `fact_transactions`)
  - Dimension tables (Customer, Product, Date, etc.)
- Final analytics-ready Gold layer


---


## 🔄 Data Flow Summary


| Layer   | Table Example             | Characteristics                     |
|---------|---------------------------|-------------------------------------|
| Bronze  | `bronze_transactions`     | Raw + metadata, append/overwrite    |
| Silver  | `silver_transactions`     | Cleaned, validated, business rules  |
| Gold    | `fact_sales`, `dim_customer`, `dim_product` | Star schema, aggregated, ready for BI |


---


## ⚠️ Known Issues & Solutions


| Error                                      | Cause                              | Solution |
|--------------------------------------------|------------------------------------|----------|
| `TABLE_OR_VIEW_ALREADY_EXISTS`             | Table already exists               | Use `.mode("overwrite")` or `CREATE OR REPLACE TABLE` |
| `TooManyRequestsForCapacity` (HTTP 430)    | Capacity limit reached             | Cancel jobs in Monitoring hub, wait, or upgrade capacity |
| Livy session creation failed               | Too many concurrent notebooks      | Stop other notebooks, use `%stop_session` |


---


## 📈 Future Improvements


- [ ] Add incremental loading logic for Bronze layer
- [ ] Implement Delta Live Tables / Spark Job Definitions
- [ ] Add data quality framework (Great Expectations / Soda)
- [ ] Automate pipeline with Fabric Data Factory / Pipelines
- [ ] Add Power BI semantic model + reports


---


## 🤝 Contributing


Contributions are welcome! Please open an issue or submit a pull request.


---


## 📄 License


This project is licensed under the MIT License.


---


## 👩‍💻 Author


**Narges**  
E-commerce ETL Project using Microsoft Fabric


---


> **Note**: This project was built as a learning exercise for modern data engineering practices on Microsoft Fabric Lakehouse.


---





