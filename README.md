# Population at Risk For Trachoma

## Table of Contents
- [Project Overview](#project-overview)
- [Tools](#tools)
- [Data Sources](#data-sources)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis using SQL](#data-analysis-using-sql)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)

### Project Overview

Neglected Tropical Diseases (NTDs) are a group of infectious diseases causing severe health problems like anemia, blindness, chronic pain, infertility, and disfigurement, predominantly affecting millions in tropical regions such as Africa, Asia, and South and North America. NTDs trap many victims in poverty due to their inability to work and the severe social stigma they face. Despite the existence of affordable interventions and promising new technologies, NTDs remain underfunded and insufficiently addressed in global research and development. Trachoma is one of all the NTDs.

Trachoma is a major contagious eye disease caused by the Bacterium Chlamydia trachomatis that can lead to blindness. It's a public health issue in more than 40 countries and is responsible for 1.9 million cases of blindness or visual impairment.

This SQL-based project aims to compile and analyze sample of global data on trachoma disease to understand population's risk, impact, and trends year-wise within a country.

### Tools

- MYSQL Server - Data manipulation and Analysis
  - [Download tool here](https://dev.mysql.com/downloads/installer/)
  
### Data Sources

I have collected a dataset from [Our World in Data](https://ourworldindata.org/grapher/number-treated-for-trachoma). 

Note: After downloading, open the file and change the column names into a short name according to the data and MYSQL naming convention to make SQL coding short to write and easy to understand. 

Population at Risk for Trachoma: The primary dataset used for this project is the [dataset_file](https://github.com/rajarapuraj/SQL_Project/blob/main/population-at-risk-of-trachoma-vs-receiving-treatment.csv), containing year wise population count within a specific country/continent that is collected by the World Health Organization - Global Health Observatory (2024). 

Then, I've created a schema or database on MYSQL server to perform EDA on the data. Now, let's do some manipulation on data to manage null values, and finally performing some basic analysis on the dataset to answer key questions about the trachoma population and to take necessary action further.

### Data Cleaning/Preparation

In the initial data prepation phase, I've performed the following tasks:

A. Removing of duplicates 

B. Stadardizing the data 

C. Managing Null values or blank values 

D. Removing empty or unwanted columns 

Here is the sample code...

```sql
	WITH Duplicates_CTE AS
		(
		  SELECT * ,
		  ROW_NUMBER() OVER(
		  PARTITION BY Country, `Code`, `Year`, Trachoma_Risk, Antibiotics_Treatment, Operated) AS Row_Num
		  FROM   trachoma_data_staging
		)
	SELECT *
	FROM   Duplicates_CTE
	WHERE  Row_Num > 1;
```

Please [click here](https://github.com/rajarapuraj/SQL_Project/blob/main/Trachoma_SQL_Project.sql) for detail SQL codes performed on the dataset.

### Exploratory Data Analysis

EDA involved exploring the trachoma population data to answer key questions, such as:

1. What is the total population that is at risk for trachoma?
2. Which country population is at high risk?
3. What is the total population treated with antibiotics for trachoma?
4. Which country population are treated high with antibiotics?
5. What is the total population get operated for trachoma?
6. Which country population is high operated for trachoma?

### Data Analysis using SQL

Here I'm including one of all the interesting codes/features worked with

```sql
	SELECT Country, Total_Trachoma_Risk AS High_Trachoma_Risk
	FROM (
	    SELECT   Country, SUM(Trachoma_Risk) AS Total_Trachoma_Risk
	    FROM     trachoma_data_staging
	    GROUP BY Country
	) AS Subquery
	ORDER BY Total_Trachoma_Risk DESC;
```

### Results/Findings

Finally, the exploratory data analysis (EDA) on the trachoma dataset provided critical insights into the global landscape of this neglected tropical disease. The analysis reveals that a total of 5.27 billion people are at risk for trachoma worldwide, with Africa having the highest at-risk population and Algeria the lowest. Out of the at-risk population, 643.5 million people have been treated with antibiotics, with the highest number of treatments occurring in Africa and the lowest in Oman. Additionally, 38.9 million people have undergone surgical operations for trachoma, with Africa again leading and Vanuatu at the lowest. Despite these efforts, the overall number of trachoma patients has been gradually decreasing from 2013 to 2022, with the exception of a spike in 2018. These findings underscore the importance of sustained investment in public health strategies and interventions to further reduce the burden of trachoma globally.

### Recommendations

Based on the analysis, I recommend the following actions:
- Need to increase funding and resources for high-risk regions like Africa, which ensures the distribution of antibiotics and surgical interventions, ultimately reducing the prevalence of the disease.
- Should strengthen public health initiatives by focusing on increasing awareness, improving sanitation, and providing access to necessary medical treatments in low-treatment countries like Oman and Vanuatu.
- Implement continuous monitoring and rapid response mechanisms to address spikes in trachoma cases, particularly highlighted by the 2018 increase, ensuring sustained reductions through robust surveillance systems.





  
  
   
