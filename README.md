# Task-1-Data-Cleaning-and-Preprocessing
# 🩺 Medical Appointment No Show — Data Cleaning & Preprocessing

## 📘 Project Overview
This project focuses on **cleaning and preprocessing** the *Medical Appointment No Show* dataset from Kaggle.  
The dataset contains information about medical appointments in Brazil and whether patients showed up for their appointments.  

The goal of this task is to identify and fix common data issues such as **missing values, duplicates, inconsistent formatting, and incorrect data types**, preparing the dataset for analysis or modeling.

---

## 🎯 Objective
- Handle missing and duplicate data  
- Standardize column names and text values  
- Correct date formats and data types  
- Remove outliers (e.g., invalid ages)  
- Save and summarize the cleaned dataset  

This task was performed as part of a **Data Analyst Internship - Task 1**.

---

## 🧰 Tools Used
- **Excel** – for manual data exploration and basic cleaning  
- **Python (Google Colab)** – for automated data cleaning using Pandas  

---

## 📂 Dataset Description
The dataset (from [Kaggle - Medical Appointment No Shows](https://www.kaggle.com/joniarroba/noshowappointments)) typically includes:

| Column | Description |
|--------|-------------|
| `PatientId` | Unique identifier for the patient |
| `AppointmentID` | Unique ID for the appointment |
| `Gender` | Male or Female |
| `ScheduledDay` | Date and time the appointment was scheduled |
| `AppointmentDay` | Date of the actual appointment |
| `Age` | Age of the patient |
| `Neighbourhood` | Location of the hospital |
| `Scholarship` | Indicates if the patient is enrolled in a welfare program |
| `Hipertension`, `Diabetes`, `Alcoholism`, `SMS_received` | Patient health or communication indicators |
| `No-show` | Whether the patient showed up (`No`) or missed (`Yes`) the appointment |

---

## 🧹 Data Cleaning Steps (in Python)

```python
import pandas as pd

# Step 1: Load data
df = pd.read_csv("/content/MedicalAppointmentNoShows.csv")

# Step 2: Check missing values
df.isnull().sum()

# Step 3: Remove duplicates
df = df.drop_duplicates()

# Step 4: Standardize text
df['Gender'] = df['Gender'].str.lower().str.strip()
df['No-show'] = df['No-show'].str.strip().str.lower()

# Step 5: Convert dates
df['ScheduledDay'] = pd.to_datetime(df['ScheduledDay'])
df['AppointmentDay'] = pd.to_datetime(df['AppointmentDay'])

# Step 6: Fix column names and types
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')
df['age'] = df['age'].astype(int)

# Step 7: Handle invalid ages
df = df[(df['age'] >= 0) & (df['age'] <= 120)]

# Step 8: Save cleaned data
df.to_csv("/content/MedicalAppointmentNoShows_Cleaned.csv", index=False)
print("✅ Cleaned dataset saved successfully!")
```

---

## 🧾 Summary of Cleaning Actions

| Step | Action | Result |
|------|---------|--------|
| 1 | Checked missing values | None found / handled using median |
| 2 | Removed duplicates | Ensured unique records |
| 3 | Cleaned text data | Consistent lowercase and no spaces |
| 4 | Converted date columns | Uniform datetime format |
| 5 | Renamed columns | snake_case style |
| 6 | Fixed data types | Corrected int and datetime |
| 7 | Removed outliers | Ages between 0–120 |
| 8 | Saved cleaned file | Ready for analysis |

---



## 🧠 Key Learnings
- Handling missing, inconsistent, and duplicate data using **Pandas**  
- Working with **date/time formats** in Python and Excel  
- Importance of **data preprocessing** before visualization or modeling  

---

