# Hospital Billing System Analysis

## Project Overview
This project demonstrates the processing and analysis of medical billing data using **SQL Server** and **Power Query**. It involves cleaning data from an Excel file, transforming it into a suitable format, and importing it into a SQL Server database for analytical queries. The project also includes an **Entity-Relationship (ER)** model to design the database schema and establish table relationships using **SQL Server Management Studio (SSMS)**.

## Project Objectives
- **Data Extraction**: Convert Excel data into CSV format using Power Query.
- **Data Cleaning**: Address issues such as incorrect data types, punctuation, and extra spaces in hospital names.
- **Database Design**: Create an ER model for tables (Patients, Hospitals, Doctors, Billing, Medical Conditions).
- **Data Analysis**: Execute SQL queries to derive insights, such as patient counts by medical condition, average billing amounts, and multiple admissions.

## Data Structure
The dataset includes the following columns:
- **Name**: Patient name
- **Age**: Patient age
- **Gender**: Patient gender
- **Blood Type**: Patient blood type
- **Medical Condition**: Patient's medical condition
- **Date of Admission**: Admission date
- **Admission Type**: Type of admission (Emergency, Elective, Urgent)
- **Test Result**: Medical test result
- **Medication**: Prescribed medication
- **Doctor**: Doctor's name
- **Hospital**: Hospital name
- **Insurance**: Insurance provider
- **Billing Amount**: Billing amount

The data was converted to CSV, imported into SQL Server, and organized into related tables.

## Technologies Used
- **Power Query**: For data cleaning and transformation.
- **SQL Server**: For data storage and querying.
- **SQL Server Management Studio (SSMS)**: For database management and table relationships.
- **GitHub**: For project storage and sharing.

## Key SQL Queries
Below are examples of SQL queries performed:
1. List distinct hospital names:
   ```sql
   SELECT DISTINCT HospitalName
   FROM Hospitals
   ORDER BY HospitalName;
   ```
2. Sort patients by age (oldest to youngest):
   ```sql
   SELECT PatientName, Age
   FROM Patients
   ORDER BY Age DESC;
   ```
3. Calculate average billing amount per admission:
   ```sql
   SELECT AVG(BillingAmount)
   FROM Admissions
   GROUP BY AdmissionID;
   ```
4. List patients treated at 'Cairo Hospital' using JOIN:
   ```sql
   SELECT p.PatientName
   FROM Patients p
   INNER JOIN Admissions a ON p.PatientID = a.PatientID
   INNER JOIN Hospitals h ON a.HospitalID = h.HospitalID
   WHERE h.HospitalName = 'Cairo Hospital';
   ```
5. Use CTE to show patients over 40 admitted as 'Urgent':
   ```sql
   WITH UrgentPatients AS (
       SELECT p.PatientName, p.Age, d.DoctorName, h.HospitalName
       FROM Patients p
       INNER JOIN Admissions a ON p.PatientID = a.PatientID
       INNER JOIN Doctors d ON a.DoctorID = d.DoctorID
       INNER JOIN Hospitals h ON a.HospitalID = h.HospitalID
       WHERE p.Age > 40 AND a.AdmissionType = 'Urgent'
   )
   SELECT * FROM UrgentPatients;
   ```

## Challenges and Solutions
1. **Data Type Issues**:
   - **Challenge**: Data imported from Excel had incorrect data types.
   - **Solution**: Reassigned data types in CSV and reimported into SQL Server.
2. **Hospital Name Cleaning**:
   - **Challenge**: Hospital names contained punctuation and extra spaces.
   - **Solution**: Used Power Query with assistance from AI tools to clean the data.

## How to Run the Project
1. Clone the repository and download the CSV files.
2. Use Power Query to clean the data if needed.
3. Import the data into SQL Server using SSMS.
4. Execute the SQL queries provided in the project files.
5. Ensure tables are linked with foreign keys as per the ER model.

## Repository Structure
- `/data`: Contains raw and cleaned CSV files.
- `/sql`: Contains SQL query files.
- `/docs`: Includes ER model and other documentation.
- `README.md`: This file.

## Requirements
- **SQL Server**: For running the database.
- **SSMS**: For database management.
- **Power Query**: For data cleaning.
- **Excel**: For viewing raw data.

## Additional Notes
- The project can be extended to include more analyses, such as treatment costs by insurance provider or medical condition.
- The database design is flexible and scalable for adding new tables or queries.
