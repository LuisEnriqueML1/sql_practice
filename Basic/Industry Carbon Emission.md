# SQL

## Why SQL, Python and R? 🐍

In this exercise, I wanted to challenge myself by using Python and a SQL module to work with data. To make things even more interesting, I decided to create a final graph using R, taking advantage of the unique benefits that each language offers.

## Objective
The main objective of this task is to find the number of different companies and their total carbon footprint for each industry group. We want to focus on the most recent year in the database. To achieve this, we need to write a query that will give us three columns: industry group, number of companies, and total industry footprint. The total industry footprint should be rounded to one decimal place. Finally, we want the results to be sorted from highest to lowest based on the total industry footprint.

By doing this, we can gain insights into which industry groups have the highest carbon footprints and how many companies are contributing to them. This information can be valuable for understanding the environmental impact of different industries and identifying areas where improvements can be made.

## Project Development
### 📦 Modules
```
import pandas as pd
import sqlite3
import numpy as np
```

* Pandas is like a helpful assistant that allows us to easily work with data.
* SQLite. We can write SQL queries to retrieve the exact data we're looking for.
* Numpy, which is like a mathematical wizard.


### 📊 Data Loading

To begin, the first line of code loads the xlsx file. This means that it retrieves the file and prepares it for further actions. 
Moving on to the second line, it provides us with a print statement that gives us some indication or information. This could be something like a message or a prompt for the user. 
Next, a variable called "n" is created to serve as an index. This index is used in a loop, which means that it will repeat a certain set of instructions for each item in a list. In this case, the loop will iterate over the column names and display information about them. 


```
df = pd.read_excel("Carbon.xlsx")
print("Information about columns")
n = 0
for i in df.columns:
    print(f"Index: {n}  Name: {i}")
    n += 1
```

### 🔌 SQL Connection

This way, we tell Python that we want to manipulate the data using the DataFrame we just loaded via SQL.
```
conn = sqlite3.connect(':memory:')
df.to_sql('df', conn, index=False, if_exists='replace')
```

### 🔍 Queries
We start with a test to see the available information:
```
query = '''
SELECT *
FROM df
LIMIT 3
'''
# Execute the query
result = pd.read_sql_query(query, conn)
print(result)
```
We create a variable named query, which queries all columns of the DataFrame with a limit of 3 rows.

Next is to perform the task of this document, which I break down as follows:

Three columns are needed: the first is the industry, the second is the number of companies, and the third is the footprint· The data must be sorted by the last column and rounded· So far, it doesn't seem complicated, except that we need the data from the most recent year· This can be approached in two ways:

1. The first way is to query to find the latest year and write it in a WHERE clause like WHERE year = 2019·
2. The second way assumes that this query can always return the latest year whenever it is executed, without needing to write it as in the first method·

To have a query that can contain high-quality information and is less prone to errors, the second method is chosen· 

```
query = '''
SELECT 
  Industrygroup as industry_group, 
  count(
    distinct(Company)
  ) as num_companies, 
  round(
    SUM(Carbonfootprint), 
    1
  ) as Total_industry_footprint 
  
FROM 
  df
   
WHERE 
  Yearofreporting in (
    select 
      max (Yearofreporting) 
    from 
      df
  )
   
group by 
  1 
  
order by 
  3 desc

'''
result = pd.read_sql_query(query, conn)
result

```


