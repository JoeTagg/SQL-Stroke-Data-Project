# SQL Stroke Data Project

### Introduction/Overview

In this project, I set about using SQL to analyse stroke prediction data. The dataset for this was taken from Kaggle [here](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset/data), and included the following attribute information:

1) id: unique identifier
2) gender: "Male", "Female" or "Other"
3) age: age of the patient
4) hypertension: 0 if the patient doesn't have hypertension, 1 if the patient has hypertension
5) heart_disease: 0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease
6) ever_married: "No" or "Yes"
7) work_type: "children", "Govt_jov", "Never_worked", "Private" or "Self-employed"
8) Residence_type: "Rural" or "Urban"
9) avg_glucose_level: average glucose level in blood
10) bmi: body mass index
11) smoking_status: "formerly smoked", "never smoked", "smokes" or "Unknown"*
12) stroke: 1 if the patient had a stroke or 0 if not

*Note: "Unknown" in smoking_status means that the information is unavailable for this patient

This was a step-up in complexity compared to previous SQL projects, incorporating new syntax such as: JOINs / UNION / CASE WHEN / HAVING / CTEs / CAST / Window Functions etc.

I once again used the in-browser data tool [csvfiddle.io](https://www.csvfiddle.io). The link to the workspace, and other project files, can be found in this repo.

### Query 1: View first 10 entries from entire dataset

Goal: Get familiar with the dataset, understand the columns featured and the types of data (INTEGER/VARCHAR/DOUBLE etc.). A quick COUNT(*) reveals there's 5000+ rows of data, so I limited this query to only 10. I noted in the BMI column there was "N/A" recorded as a value, which meant the column wouldn't be recognised as a DOUBLE/FLOATING (decimal) data type. This would cause an issue later. 

<img width="300" alt="image" src="https://github.com/user-attachments/assets/18b91249-6abf-4dd5-a730-ff02908f47e5">
<img width="789" alt="image" src="https://github.com/user-attachments/assets/22681fb7-4b4c-4b94-986f-eaefc209b7be">

### Query 2: List patients who had a stroke

Goal: Not so much of an analysis, but an easy way to pull off a list of patients recorded has having had a stroke

<img width="300" alt="image" src="https://github.com/user-attachments/assets/873d8719-a605-4a10-af6d-de8c387bebfa">
<img width="773" alt="image" src="https://github.com/user-attachments/assets/dcf1caaf-eb26-4e64-8f5b-717ce75d884a">

### Query 3.1: Total number of patients who had a stroke

Goal: Followed by a count of those records. 249 patients in total, from our entire dataset (5k+), recorded has having had a stroke

<img width="300" alt="image" src="https://github.com/user-attachments/assets/0cb6cbfc-7150-4a56-824e-c58798b524af">
<img width="200" alt="image" src="https://github.com/user-attachments/assets/6bce23ee-0ef2-4475-a1d3-86c0249343c8">

### Query 3.2: Percentage of strokes/no strokes from dataset

Goal: I then used the CASE WHEN expression and some arithmetic operators to understand the % split of strokes/no strokes. Roughly 5% of the patients in the dataset are recorded as having had a stroke. There wasn't geographic information about the dataset, who was targeted etc., but it would be interesting to compare these percentages to population averages, in a country/community and so on.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/19a693c5-c2c5-4c8d-acf1-9eb2d7a79e8a">
<img width="750" alt="image" src="https://github.com/user-attachments/assets/cdf142c2-c96d-4c22-b23d-3aa26f7cd01b">

### Query 4: Average age of patients by gender

Goal: This query calculated the average age of all patients by gender. I believe the AVG expression in SQL is the mean, so we won't get an idea of the actual spread and distribution of those ages. But it's a good starting point, and we can see that for both Male and Female is roughly the same. It also captured the average age of the 'Other category' as considerably lower. I ran a new query to filter just records classed as 'Other' and it turns out there was just one.

<img width="400" alt="image" src="https://github.com/user-attachments/assets/199bd986-dc41-45cc-bb13-fc13efc3625b">
<img width="300" alt="image" src="https://github.com/user-attachments/assets/b9b26d42-0fa7-4063-be41-bc6e6d53d579">

### Query 5.1: Create table for patient demographic information

Goal: I then wanted to make use of the JOIN clauses, but with only one data set/table, I had to improvise and create pretend tables from the existing data. This first one represents a table of just demographic information for each patient. I'm imagining that a healthcare organisation might keep patient demographic information in one location, and medical information in another. And those would be joined on the unique 'id' field present in both.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/d337a8ec-9c48-41f5-b260-fc5ab70c0eaa">
<img width="500" alt="image" src="https://github.com/user-attachments/assets/f7607092-13ef-4722-a3f9-175e6f823c2c">

### Query 5.2: Create table for patient medical information

Goal: This table represents the dataset for patient medical information.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/724202cb-3fef-4983-9340-a0efc5c9ce2a">
<img width="518" alt="image" src="https://github.com/user-attachments/assets/93b0e10a-7185-47be-8185-4df79402a068">

### Query 5.3: Combine demographic & medical tables

Goal: And now we get to the JOIN. If I'd had the two tables imported, I'd have been able to refer to them in the FROM statements. In this case, I repeated the reference to the 'stroke_data' table and selected the necessary columns. I assigned 'p' to the demographic patient info, and 'm' for the medical patient info. The 'tables' were joined, and the 'id' fields used as the field to match ON, ensuring correct reconciliation and no duplicate values.

<img width="392" alt="image" src="https://github.com/user-attachments/assets/23a59b69-7e33-4a33-92c3-b75c10dd775c">
<img width="719" alt="image" src="https://github.com/user-attachments/assets/9bc044d5-f555-464d-944b-dabba2e718dc">

### Query 6: Categorise ages into groups

Goal: I used the CASE expression to define names for age groups, which had themselves been defined using the WHERE clause. Not so much an analysis as data preparation and transformation.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/05cd05a4-b76f-43c0-9a68-7fa06e9fd1b3">
<img width="500" alt="image" src="https://github.com/user-attachments/assets/ff8c735f-99c2-4f9c-8b0c-9241c54f9d64">

### Query 7.1: Calculate average bmi over 25 by work type (FAILED)

Goal: I wanted to explore possible links between BMI (Body Mass Index) and work type. I'd forgotten about the 'N/A' values lurking in the bmi column, making the data type VARCHAR. Because these text values were mixed in with the proper decimal number values, it meant that calculating an average wasn't possible. Thus, query 7.2

<img width="500" alt="image" src="https://github.com/user-attachments/assets/99c2cef2-94e2-43e3-95dd-030da1b75b65">
<img width="580" alt="image" src="https://github.com/user-attachments/assets/e11678ff-1c9c-4972-ae7a-d7844e47017f">

### Query 7.2: Calculate average bmi over 25 by work type (CORRECTED)

Goal: I then used used the CAST function to assign the 'bmi' column the data type of 'Float' (decimal number). I also added a WHERE clause to remove instances of bmi equalling either N/A or a blank. There's perhaps not much to glean in the way of insights. BMI was quite static across all employment types. Interestingly, 'never_worked' was lower by 4-5 points. A quick check of the main dataset, and it was confirmed that the majority of these records were teenagers. It makes sense that they might be marked as not working. There is a missing work_type of 'children', which isn't showing as all of them had a BMI of 21 or less.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/83e92ac7-2c46-4aaa-b605-ded3c51a1536">
<img width="500" alt="image" src="https://github.com/user-attachments/assets/2139f261-8f93-4773-ac31-11022b035461">

### Query 8: Combine active smoker and non-smoker information

Goal: Another query focused on daa

<img width="400" alt="image" src="https://github.com/user-attachments/assets/c34f6835-9586-4d81-b43f-e06eb38ea54d">
<img width="400" alt="image" src="https://github.com/user-attachments/assets/2ca9280f-a590-4b4d-a1a4-4ce1d54283f9">

### Query 9: Calculate average glucose level for patients over 50

Goal: xxx

<img width="700" alt="image" src="https://github.com/user-attachments/assets/3bda09f1-c9c8-4b36-8c14-c7894507e0f2">
<img width="400" alt="image" src="https://github.com/user-attachments/assets/2c4d818e-b754-46d8-ac5a-f50b63f65957">

### Query 10: Change average glucose level data type and compare results

Goal: xxx

<img width="550" alt="image" src="https://github.com/user-attachments/assets/0341a4fc-8d3e-4905-88ed-c7d480927a7f">
<img width="650" alt="image" src="https://github.com/user-attachments/assets/386941d8-17ba-42e9-9478-539efc41605a">

### Query 11.1: Running/moving average of glucose levels by age

Goal: xxx

<img width="600" alt="image" src="https://github.com/user-attachments/assets/a5209741-5b9c-4e1b-9a5b-b9905710406a">
<img width="550" alt="image" src="https://github.com/user-attachments/assets/11098932-5e5a-43b7-8295-a033874aba0d">

### Query 11.2: Average glucose level by age

Goal: xxx

<img width="600" alt="image" src="https://github.com/user-attachments/assets/72d5f8b8-e3c1-4c38-813b-2ee34502ce4b">
<img width="550" alt="image" src="https://github.com/user-attachments/assets/0c26560a-3048-4e8b-af4f-9d658563aa88">

### Query 12: Number of stroke cases by residence type and smoking status

Goal: xxx

<img width="600" alt="image" src="https://github.com/user-attachments/assets/8a3f5ed8-1aa2-47fc-ba2c-931dd9498546">
<img width="550" alt="image" src="https://github.com/user-attachments/assets/fd9ee5bf-9c31-4604-b21d-b8f46f5f6d3b">

### Query 13: Rank patients within their age group based on bmi

Goal: xxx

<img width="450" alt="image" src="https://github.com/user-attachments/assets/22b99222-b478-45ab-abf7-079310351299">
<img width="500" alt="image" src="https://github.com/user-attachments/assets/1a5b773c-3e49-4694-836d-43b49cf7e0cf">

### Query 14: Identify at risk patients

Goal: xxx

<img width="500" alt="image" src="https://github.com/user-attachments/assets/64468bd9-c8d8-472c-84a2-2b9d21d0dfa4">
<img width="400" alt="image" src="https://github.com/user-attachments/assets/ee27292b-2465-42f2-87f4-2c82e99650b5">

### Query 15: Compare hypertension, heart disease, and stroke count against residence type

Goal: xxx

<img width="496" alt="image" src="https://github.com/user-attachments/assets/bcaee135-9e7e-4fcb-8c07-2015265f09af">
<img width="451" alt="image" src="https://github.com/user-attachments/assets/13d01705-070e-479d-b0c1-ff9a344559b0">
<img width="1000" alt="image" src="https://github.com/user-attachments/assets/9a534a9d-9614-4e03-99a3-0058149df633">

### Conclusion

xxxxx


