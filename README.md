# WORK - LAM

This repository contains extracts of my code that I developped during an internship as a Data Analyst in a telecom start-up. Two types are present :
- Files having their names start with "SMS" are pieces of the SQL code that I used to analyse, calculate and sort all SMS-related data, and add them to a global (or aggregate) table, which will be the basis for the company's reporting dashboards.

- The "Script" file contains Python code allowing the import, processing and export to a SQL database all relevant information pertaining to the Finance departement, which used to be in an Excel File resulting of a financial management software.



## FOCUS  : SQL ##
### SMS_Update_meta :

All SMS-related data is received monthly, this data for the month "M" is added at the beginning of the month "M+1". There needs to be an automated processing script for them.
In order to achieve that, a "Meta" table was created in the database. It identifies all different tables, and has them assigned with a "Processed" value (O or 1), depending on whether their data was processed and added to the aggregate table.
Update_meta is used to update this "Meta" table by collecting the names of all other tables and adding the new ones with a "Processed" value of 0.


### SMS_Populate_ag :

This Stored Procedure ("SP") focuses on tables that have been added to the "Meta" table and that have a "Processed" value of 0. It enables the processing of this new data (via other stored procedures) and its addition to the aggregate table.
An update to the "Meta" table, and more specifically the "Processed" value, will close this step and ensure that all data have been processed.


### SMS_Insert_sms_ag :

This stored procedure will enable the processing of all available data on a specific SMS table, depending on previously-set criteria (Client name, Phone area code, SMS status, etc) and also the integration of this data to the corresponding aggregate table.




## FOCUS : Python ##
### Script_finance :

This script was built for processing data from the Finance Departement, which were initially an Excel file which could not be directly imported and processed in the database due to formating modifications handled by their software.
Its goal is to provide the department with a centralized management view and database, and allow for the standardization of all dashboarding solutions in the company. 
In this script, the Excel file is imported, its timeframes and corresponding subtotals (which will be used as validation tools) are saved, data is processed and saved in the database.
