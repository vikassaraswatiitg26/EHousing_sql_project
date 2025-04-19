# Real Estate Data Cleaning & Transformation with SQL
![E Housing logo](https://github.com/vikassaraswatiitg26/EHousing_sql_project/blob/main/EHousing_logo.jpeg)

## Objective:
    # 🏡 eHousing Data Cleaning & Transformation using SQL

This project demonstrates how to clean, transform, and prepare real estate property data for analysis using SQL. The dataset contains information about property sales, ownership, addresses, land value, and more.

---

## 📌 Project Objectives

· Standardize and clean date formats  
· Fill missing property addresses using joins  
· Split full addresses into separate columns (Street, City)  
· Standardize categorical values (e.g., Yes/No columns)  
· Identify and remove duplicate records  
· Drop irrelevant or unused columns  

---

## 🧰 Tools Used

· PostgreSQL (SQL syntax)  
· Window functions  
· Common Table Expressions (CTEs)  
· String manipulation functions  
· Data type conversion  

---

## 🗂️ Table Structure

```sql
CREATE TABLE eHousing (
    UniqueID INT,
    ParcelID VARCHAR(100),
    LandUse VARCHAR(100),
    PropertyAddress VARCHAR(250),
    SaleDate DATE,
    SalePrice INT,
    LegalReference TEXT,
    SoldAsVacant VARCHAR(50),
    OwnerName VARCHAR(200),
    OwnerAddress VARCHAR(250),
    Acreage DECIMAL,
    TaxDistrict VARCHAR(100),
    LandValue INT,
    BuildingValue INT,
    TotalValue INT,
    YearBuil INT,
    Bedrooms INT,
    FullBath INT,
    HalfBath INT
);

