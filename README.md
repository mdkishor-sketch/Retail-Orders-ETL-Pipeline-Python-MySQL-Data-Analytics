# 🛒 Retail Orders Data Analysis

A comprehensive data analysis project that demonstrates the complete data pipeline from data acquisition to database storage using Python, Kaggle API, and MySQL.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Data Pipeline](#data-pipeline)
- [Database Schema](#database-schema)
- [Analysis Insights](#analysis-insights)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This project analyzes retail orders data from Kaggle, performs data cleaning and transformation using Pandas, and stores the processed data in a MySQL database for further analysis. The dataset contains 9,994 retail orders with information about products, customers, pricing, and geographical data.

## ✨ Features

- **Automated Data Download**: Uses Kaggle API to automatically download the latest dataset
- **Data Cleaning**: Handles null values, standardizes column names, and ensures data quality
- **Data Transformation**: 
  - Calculates discount amounts from discount percentages
  - Computes sale prices after discounts
  - Derives profit margins
  - Converts date formats to database-compatible types
- **Database Integration**: Automatically creates tables and imports data to MySQL
- **Error Handling**: Robust handling of missing values and data inconsistencies

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| **Python 3.13** | Core programming language |
| **Pandas** | Data manipulation and analysis |
| **Kaggle API** | Dataset download automation |
| **MySQL** | Relational database storage |
| **mysql-connector-python** | MySQL database connectivity |
| **SQLAlchemy** | Database ORM and connection management |
| **Jupyter Notebook** | Interactive development environment |

## 📁 Project Structure
```
Retail-Orders-Analysis/
│
├── Retail-orders.ipynb       # Main Jupyter notebook
├── README.md                 # Project documentation
├── requirements.txt          # Python dependencies
├── .gitignore               # Git ignore file
│
└── data/                    # Data directory (gitignored)
    └── orders.csv           # Downloaded dataset
```

## 🚀 Installation

### Prerequisites
- Python 3.8 or higher
- MySQL Server 8.0 or higher
- Kaggle account with API credentials

### Step 1: Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/retail-orders-analysis.git
cd retail-orders-analysis
```

### Step 2: Install Dependencies
```bash
pip install pandas mysql-connector-python sqlalchemy kaggle jupyter
```

Or use requirements.txt:
```bash
pip install -r requirements.txt
```

### Step 3: Set Up MySQL Database
```sql
CREATE DATABASE retail;
```

## ⚙️ Configuration

### 1. Kaggle API Setup
1. Go to https://www.kaggle.com/account
2. Scroll to **API** section
3. Click **Create New API Token**
4. Set credentials in your notebook:
```python
import os
os.environ['KAGGLE_USERNAME'] = 'your_username'
os.environ['KAGGLE_KEY'] = 'your_api_key'
```

### 2. MySQL Connection
Update the connection string in the notebook:
```python
engine = create_engine('mysql+mysqlconnector://root:YOUR_PASSWORD@localhost/retail')
```

## 📖 Usage

### Option 1: Run Jupyter Notebook
```bash
jupyter notebook Retail-orders.ipynb
```

### Option 2: Run Cells Step-by-Step
1. **Download Data**: Execute cell to download from Kaggle
2. **Extract Files**: Unzip the downloaded dataset
3. **Load & Clean**: Read CSV and handle null values
4. **Transform**: Create calculated columns
5. **Import to MySQL**: Load data into database

## 🔄 Data Pipeline
```
┌─────────────────┐
│  Kaggle API     │
│  Download       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Extract ZIP    │
│  File           │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Load CSV       │
│  with Pandas    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Data Cleaning  │
│  - Handle NULLs │
│  - Rename cols  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Transform      │
│  - Discount     │
│  - Sale Price   │
│  - Profit       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Load to MySQL  │
│  Database       │
└─────────────────┘
```

## 🗄️ Database Schema

### Table: `retail_orders`

| Column | Type | Description |
|--------|------|-------------|
| `order_id` | INT | Unique order identifier |
| `order_date` | DATE | Date when order was placed |
| `ship_mode` | VARCHAR(50) | Shipping method |
| `segment` | VARCHAR(50) | Customer segment |
| `country` | VARCHAR(50) | Country of delivery |
| `city` | VARCHAR(100) | City of delivery |
| `state` | VARCHAR(50) | State/Province |
| `postal_code` | VARCHAR(20) | Postal/ZIP code |
| `region` | VARCHAR(50) | Geographic region |
| `category` | VARCHAR(50) | Product category |
| `sub_category` | VARCHAR(50) | Product sub-category |
| `product_id` | VARCHAR(50) | Product identifier |
| `cost_price` | DECIMAL(10,2) | Cost to company |
| `list_price` | DECIMAL(10,2) | Original price |
| `quantity` | INT | Number of units |
| `discount_percent` | INT | Discount percentage |
| `discount` | DECIMAL(10,2) | **Calculated**: Discount amount |
| `sale_price` | DECIMAL(10,2) | **Calculated**: Final sale price |

### Calculated Columns
```python
discount = list_price × discount_percent × 0.01
sale_price = list_price - discount
profit = sale_price - cost_price
```

## 📊 Analysis Insights

### Data Overview
- **Total Orders**: 9,994
- **Date Range**: 2022-2023
- **Categories**: Furniture, Office Supplies, Technology
- **Regions**: South, West, East, Central

### Key Findings
- Dataset contains orders from multiple customer segments (Consumer, Corporate, Home Office)
- Various shipping modes available (Standard, Second Class, First Class, Same Day)
- Discount percentages range from 0% to higher values
- Geographical coverage across United States

⭐ **Star this repository if you find it helpful!**
