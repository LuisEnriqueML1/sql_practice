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

