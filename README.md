# Real Estate Data Cleaning & Transformation with SQL
![E Housing logo](https://github.com/vikassaraswatiitg26/EHousing_sql_project/blob/main/EHousing_logo.jpeg)

## Objective:

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


```
## 🛠️ Data Cleaning Steps
1. Standardize Date Format
```
  ALTER TABLE eHousing
           ADD SalesDateConverted DATE;
  UPDATE eHousing
           SET SalesDateConverted = SaleDate::date;
```

2. Fill Missing Property Addresses Using Self-Join
```
UPDATE eHousing a
      SET PropertyAddress = COALESCE(a.PropertyAddress, b.PropertyAddress)
FROM eHousing b
WHERE a.ParcelID = b.ParcelID
  AND a.UniqueID <> b.UniqueID
  AND a.PropertyAddress IS NULL;
```

3. Split Full Address into Street and City

```
ALTER TABLE eHousing
        ADD PropertySplitAddress VARCHAR(100);
ALTER TABLE eHousing
        ADD PropertySplitCity VARCHAR(100);

UPDATE eHousing
SET PropertySplitAddress = SUBSTRING(PropertyAddress FROM 1 FOR POSITION(',' IN PropertyAddress)-1),
    PropertySplitCity = SUBSTRING(PropertyAddress FROM POSITION(',' IN PropertyAddress)+1);

```

4.  Standardize 'SoldAsVacant' Column Values

```
UPDATE eHousing
SET SoldAsVacant = CASE
    WHEN SoldAsVacant = 'Y' THEN 'Yes'
    WHEN SoldAsVacant = 'N' THEN 'No'
    ELSE SoldAsVacant
END;
```

5.  Remove Duplicates Using CTE + ROW_NUMBER()

```
WITH rownumcte AS (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference
               ORDER BY UniqueID
           ) AS row_num
    FROM eHousing
)
DELETE FROM eHousing
WHERE UniqueID IN (
    SELECT UniqueID FROM rownumcte WHERE row_num > 1
);

```

6.  Drop Unused Columns

```
ALTER TABLE eHousing
DROP COLUMN OwnerAddress,
DROP COLUMN TaxDistrict,
DROP COLUMN PropertyAddress,
DROP COLUMN SaleDate;

```

📊 Output: Cleaned Dataset

 After all transformations, the data is now:

  • Clean, consistent, and analysis-ready 
  • Duplicate-free
  • Enriched with split address columns
  • Standardized in categorical values

📈 Future Enhancements

  • Create dashboards in Power BI or Tableau
  • Perform price trend analysis by year and region
  • Add geolocation-based insights

