# Cleaning Audible Data in Python

This project focuses on cleaning and transforming a dataset of audiobooks downloaded from [Audible.in], covering titles from **1998 to 2025 (including pre-planned releases)**.  
The primary goal is to practice **data cleaning techniques in Python** using the pandas library — preparing messy, real-world text and numeric data for analysis.

---

## 📂 Dataset Information

**File:** `data/audible_raw.csv`  
**Columns:**
- `name` – Name of the audiobook  
- `author` – Audiobook's author  
- `narrator` – Audiobook's narrator  
- `time` – Duration (hours and minutes)  
- `releasedate` – Publication date  
- `language` – Language of the audiobook  
- `stars` – Average rating (out of 5) and number of ratings  
- `price` – Price in INR (Indian Rupee)

---

## 🧹 Data Cleaning Workflow

### **Task 1: Loading and Inspecting the Data**
- Imported data using pandas and explored its structure with `.info()` and `.head()`.

### **Task 2: Cleaning Text Columns**
- Removed prefixes like **“Writtenby:”** and **“Narratedby:”** from `author` and `narrator`.

### **Task 3: Splitting Ratings Data**
- Extracted star ratings and number of reviews from the combined `stars` column.  
- Replaced *“Not rated yet”* with `NaN` and created two new columns:  
  - `rating_stars`  
  - `n_ratings`  
- Converted both to float and dropped the original `stars` column.

### **Task 4: Correcting Data Types**
- Converted:
  - `price` → float  
  - `rating_stars` → category  
  - `releasedate` → datetime  
- Cleaned inconsistent text values like “Free” and commas in price before conversion.

### **Task 5: Extracting Duration**
- Standardized time text formats (`hr`, `hrs`, `min`, `mins`) and handled “Less than 1 minute”.  
- Extracted hours and minutes to calculate a new `time_mins` column (total duration in minutes).

### **Task 6: Validating Ranges**
- Inspected distributions with histograms and `.describe()`.  
- Standardized the `language` column’s capitalization.  
- Added a conversion of prices to USD (using **1 USD = 0.012 INR**).

### **Task 7: Handling Duplicates**
- Checked for duplicates using:
  ```python
  audible.duplicated(subset=['name','author','narrator','time_mins','price']).sum()
- Kept the latest release using keep='last'

### **Task 8: Managing Missing Data**
- Used `.isna().sum()` to identify missing values.
- Retained unrated audiobooks to avoid biasing the price distribution.

### **Task 9: Saving the Clean Dataset**
- Exported the cleaned data:
  ```python
    audible.to_csv("data/audible_clean.csv", index=False)

---

## 🛠️ Tools & Libraries
- Python
- Pandas
- NumPy
- Matplotlib (for exploratory visualizations)

---

## 📊 Key Outcomes
- Cleaned text and numeric fields for consistency.
- Extracted structured data from mixed-format columns.
- Ensured valid data types for accurate analysis.
- Created a reusable, analysis-ready dataset of Audible audiobooks.

---
