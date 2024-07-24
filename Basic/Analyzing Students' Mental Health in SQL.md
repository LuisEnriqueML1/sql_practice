# 📊 1. Introduction 

In 2018, a Japanese university with a diverse student body conducted a comprehensive survey. The following year, an ethically and regulatory approved study based on this research was published.

The study found that international students face a higher risk of mental health difficulties compared to the general population. Furthermore, the research identified that social connectedness (belonging to a social group) and acculturative stress (stress associated with adapting to a new culture) are significant predictors of depression. 🧠💔

# 📝 2. Description 

To better understand this problem and find common trends, I used  SQL for exploring and analyzing data  📊.  To make the analysis even more insightful, I also used RStudio. . But it doesn't stop there! I wanted to go a step further and find groups of students who may be more prone to mental health challenges. So, I employed a clever algorithm called K-means clustering using Python. It's like having a robot assistant that can categorize students based on their unique characteristics.🤖 


## 🛢️ 2.1 Dataset
The dataset includes the following variables:

* inter_dom: Indicates the type of student, distinguishing between international and domestic students. 🌍🏠
* japanese_cate: Measures Japanese language proficiency among the students. 🇯🇵🎓
* english_cate: Measures English language proficiency among the students. 🇬🇧🎓
* gender: Indicates the gender of the student. 👩‍🎓👨‍🎓
* academic: Represents the current academic level of the student. 📚
* age: Represents the current age of the student. 🎂
* stay: Represents the current length of stay in years. 🕒
* todep: Total score measuring depression levels. 😞
* tosc: Total score measuring social connectedness. 🤝
* toas: Total score measuring acculturative stress. 🌍🤯

# 🧠 3. The Analysis 

The first step is to get an idea of the data. According to the introduction, higher levels of todep signify major depression, an increase in tosc means more connections with others, and toas indicates higher acculturative stress.

## 🛢 3.1 Data Exploration SQL
Using SQL, we will describe these parameters, focusing on dimensions such as gender, type of student (inter_dom), and language proficiency (japanese_cate and english_cate). This will help us understand the distribution and relationships within the dataset.

### 3.1.1 Look at the data
Using SQL in Python, we write a query to see the first 3 rows of all dataset. 

```
query = '''
SELECT *
FROM df
LIMIT 3
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result

```
![image](https://github.com/user-attachments/assets/8b05c5b7-be93-4c5e-8520-185dc91c5253)

### 3.1.2 🎯Averages groups



#### 🌐 Global Averages 
```
query = '''
SELECT 
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
LIMIT 3
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```

* Age of Students: 20.8 years 🎂
* Length of Stay: 2.1 years 🕒
* Total Depression Score (todep): 8.18 😞
* Average Social Connectedness Score (tosc): 37.47 🤝
* Average Acculturative Stress Score (toas): 72.3 🌍🤯
* Total Number of Students: 268 👥



#### 🏠 🌍 Domestic vs. International Students Comparison
```
query = '''
SELECT inter_dom,
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
GROUP BY inter_dom
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```
##### 🏠 Domestic Students 
* Proportion: 25% (67 students)
* Average Age: 20.40 years 🎂
* Average Length of Stay: 2.4 years 🕒
* Total Depression Score (todep): 8.6 😞
* Average Social Connectedness Score (tosc): 37.64 🤝
* Average Acculturative Stress Score (toas): 62.83 🌍🤯
##### 🌍 International Students 
* Proportion: 75% (201 students)
* Average Age: 21.02 years 🎂
* Average Length of Stay: 2.06 years 🕒
* Total Depression Score (todep): 8.04 😞
* Average Social Connectedness Score (tosc): 37.4 🤝
* Average Acculturative Stress Score (toas): 75.56 🌍🤯

#### 👩‍🎓👨‍🎓 Gender Comparison
```
query = '''
SELECT gender,
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
GROUP BY gender
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```
##### 👩‍🎓 Female Students 
* Number of Students: 170
* Average Age: 20 years 🎂
* Average Length of Stay: 2.05 years 🕒
* Total Depression Score (todep): 8.4 😞
* Average Social Connectedness Score (tosc): 37.05 🤝
* Average Acculturative Stress Score (toas): 74.03 🌍🤯
##### 👩‍🎓 Male Students 
* Number of Students: 98
* Average Age: 21.02 years 🎂
* Average Length of Stay: 2.03 years 🕒
* Total Depression Score (todep): 7.8 😞
* Average Social Connectedness Score (tosc): 38.19 🤝
* Average Acculturative Stress Score (toas): 69.04 🌍🤯


#### 🎓📚 Academic Comparison 
```
query = '''
SELECT academic,
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
GROUP BY academic
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```
##### 🎓 Graduated Students 
* Number of Students: 21
* Average Age: 27.6 years 🎂
* Average Length of Stay: 2.3 years 🕒
* Total Depression Score (todep): 5.2 😞
* Average Social Connectedness Score (tosc): 41.19 🤝
* Average Acculturative Stress Score (toas): 76.04 🌍🤯

##### 📚Undergraduate Students 
* Number of Students: 247
* Average Age: 20.29 years 🎂
* Average Length of Stay: 2.1 years 🕒
* Total Depression Score (todep): 8.4 😞
* Average Social Connectedness Score (tosc): 37.15 🤝
* Average Acculturative Stress Score (toas): 72.06 🌍🤯


#### 🇯🇵 Japanese Language Proficiency Comparison 
```
query = '''
SELECT japanese_cate,
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
GROUP BY japanese_cate
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```
##### 📉 Low Proficiency 
* Number of Students: 92
* Average Age: 21.04 years 🎂
* Average Length of Stay: 1.6 years 🕒
* Total Depression Score (todep): 7.9 😞
* Average Social Connectedness Score (tosc): 36.84 🤝
* Average Acculturative Stress Score (toas): 76.85 🌍🤯
##### 📊 Average Proficiency 
* Number of Students: 89
* Average Age: 20.8 years 🎂
* Average Length of Stay: 2.24 years 🕒
* Total Depression Score (todep): 8.44 😞
* Average Social Connectedness Score (tosc): 37.59 🤝
* Average Acculturative Stress Score (toas): 75.35 🌍🤯
##### 📈 High Proficiency 
* Number of Students: 87
* Average Age: 20.68 years 🎂
* Average Length of Stay: 2.6 years 🕒
* Total Depression Score (todep): 8.17 😞
* Average Social Connectedness Score (tosc): 38.01 🤝
* Average Acculturative Stress Score (toas): 64.59 🌍🤯


#### 🇬🇧 English Language Proficiency Comparison 
```
query = '''
SELECT english_cate,
avg(age) avg_age,
avg(stay) avg_stay, 
avg(todep) avg_todep,
avg(tosc) avg_tosc,
avg(toas) avg_toas,
count(*) students
FROM df
GROUP BY english_cate
'''
# Execute the query
result = pd.read_sql_query(query, conn)
result
```
##### 📉 Low Proficiency 
* Number of Students: 22
* Average Age: 21.18 years 🎂
* Average Length of Stay: 2.54 years 🕒
* Total Depression Score (todep): 9.3 😞
* Average Social Connectedness Score (tosc): 37.04 🤝
* Average Acculturative Stress Score (toas): 68.3 🌍🤯
##### 📊 Average Proficiency 
* Number of Students: 80
* Average Age: 20.53 years 🎂
* Average Length of Stay: 2 years 🕒
* Total Depression Score (todep): 8.3 😞
* Average Social Connectedness Score (tosc): 38.47 🤝
* Average Acculturative Stress Score (toas): 67.43 🌍🤯
##### 📈 High Proficiency 
* Number of Students: 166
* Average Age: 20.99 years 🎂
* Average Length of Stay: 2.16 years 🕒
* Total Depression Score (todep): 7.9 😞
* Average Social Connectedness Score (tosc): 37.04 🤝
* Average Acculturative Stress Score (toas): 75.29 🌍🤯


## 3.2 📊 R Graphs
```
GGally::ggpairs(df[,c(1,8,9,10)],
                aes(color = df$inter_dom))
```

![image](https://github.com/user-attachments/assets/889fb273-e5d5-4ee1-8fdd-07ecfebeda11)

Using RStudio, a GGally plot was created to visualize the distributions and relationships between international and domestic students with respect to their todep, tosc, and toas scores. The plot revealed several key insights:


**Distributions:**

* Acculturative Stress (toas): International students have a higher median toas compared to domestic students, indicating greater acculturative stress.

**Correlations:**

* Todep vs. Toas: There is a positive correlation between todep and toas, suggesting that as depression scores increase, acculturative stress also increases.
  
    Overall Correlation: 0.394
  
    Domestic Students: 0.448
  
    International Students: 0.412

* Todep vs. Tosc: There is a negative correlation between todep and tosc, indicating that as depression scores increase, social connectedness decreases.

    Overall Correlation: -0.552

    Domestic Students: -0.598

    International Students: -0.537


## 3.3 👨‍💻 T-Test Results

We used the t.test function in R to determine if the mean scores of todep, tosc, and toas are statistically different between international and domestic students.

```
dom = filter(df, inter_dom == "Dom")
inter = filter(df, inter_dom == "Inter")

t.test(dom$todep, inter$todep)
t.test(dom$tosc, inter$tosc)
t.test(dom$toas, inter$toas)
```

**Todep (Total Depression Score):**

* No significant difference in mean scores between international and domestic students.
* Conclusion: The null hypothesis that the means are equal cannot be rejected for todep.

**Tosc (Total Social Connectedness Score):**

* No significant difference in mean scores between international and domestic students.
* Conclusion: The null hypothesis that the means are equal cannot be rejected for tosc.

**Toas (Total Acculturative Stress Score):**

* Significant difference in mean scores between international and domestic students.
* Conclusion: The null hypothesis that the means are equal is rejected for toas, indicating that international students have significantly higher acculturative stress compared to domestic students.

## 3.4 🚀 Clustering

To perform unsupervised machine learning using K-means clustering, we first upload the dataset into the VSCode environment. Here are the key steps taken:

### 3.4.1 Upload Data:
The dataset is uploaded to the VSCode environment for preprocessing and analysis.

```
import pandas as pd
df = pd.read_csv("C:/users/luise/downloads/students.csv.csv")
df = df[["inter_dom","age","stay","japanese_cate","english_cate","todep","tosc","toas"]]
```

### 3.4.2 Initial Inspection:
The first few columns of the dataset are examined. The dataset includes categorical variables such as inter_dom, japanese_cate, and english_cate. We omitted gender and academic for this clustering analysis.
```
df.head(2)
```
![image](https://github.com/user-attachments/assets/906caa66-f66a-4146-8514-9d8e45baf96a)


### 3.4.3 Data Transformation:
Categorical to Numerical:
* The inter_dom column is transformed into a dummy variable, where a value of 1 indicates an international student and 0 indicates a domestic student.

The japanese_cate and english_cate columns are converted into ordinal values. For example:
* Low proficiency is represented by 1.
* Average proficiency is represented by 2.
* High proficiency is represented by 3.

```
cat_map = {'Low': 1, 'Average': 2, 'High': 3}
df["japanese_cate"] = df["japanese_cate"].replace(cat_map)
df["english_cate"] = df["english_cate"].replace(cat_map)
cols = ["inter_dom"]
data = pd.get_dummies(df, cols, drop_first=True, dtype=float)
data.head(2)
```
![image](https://github.com/user-attachments/assets/f99b104c-e305-4c12-a6e8-ad24945b3c59)


### 3.4.4 Principal Component Analysis (PCA):
To manage the many variables, we applied PCA. The explained variance ratio indicated that two components account for more than 95% of the variance. Thus, two components were chosen for the analysis.
```
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA
import numpy as np
pca2 = PCA().fit(data)
print("Cumulative Prop. sum: ", np.cumsum(pca2.explained_variance_ratio_))
a = np.arange(pca2.n_components_) 
plt.plot(a, pca2.explained_variance_ratio_)
plt.title("PCA Explained Variance Ratio")
```
![image](https://github.com/user-attachments/assets/ccd05c10-3522-4390-ac6d-685b3f6e2636)


### 3.4.5 Selecting the Best Number of Clusters:
We used the K-means algorithm from sklearn and ran tests with different numbers of clusters. Using the elbow method, we identified that 3 clusters provide the best fit for our data.
```
pca = PCA(n_components=2)
principalComponents = pca.fit_transform(data)
principalDf = pd.DataFrame(data = principalComponents,
             columns = ["C1","C2"])
from sklearn.cluster import KMeans
wcss = []
for i in range(1,10):
    km = KMeans(n_clusters=i, init="k-means++", random_state= 42)
    km.fit(data)
    wcss.append(km.inertia_)
plt.plot(range(1,10), wcss, marker = 'o', linestyle = '--')
plt.title("Clusters")
```
![image](https://github.com/user-attachments/assets/0edeaa36-bec3-4176-a6fe-fc2297904b3d)


### 3.4.6 Running the Clustering Algorithm:
We performed K-means clustering with 3 clusters on the PCA-transformed dataset. The resulting plot shows three distinct clusters with sufficient information to classify the students effectively.
```
kmc = KMeans(n_clusters=3, init = "k-means++", random_state=21)
kmc.fit(data)
data["Cluster"] = kmc.labels_
data["C1"] = principalDf["C1"]
data["C2"] = principalDf["C2"]
scatter = plt.scatter(data['C1'], data['C2'], c=data['Cluster'], cmap='viridis', s=100, edgecolors='w')
legend1 = plt.legend(*scatter.legend_elements(), title="Cluster")
plt.gca().add_artist(legend1)
plt.title("Students Clustering")

```
![image](https://github.com/user-attachments/assets/913f0605-6d54-4f98-9b1f-891e77c90336)



### 3.4.7 Cluster Averages:

The final step involved calculating the averages for each cluster. Here are the results:
![image](https://github.com/user-attachments/assets/892b0763-d5c1-4fd3-ac97-d3799f62dc12)

**Summary:**

* Cluster 0: Represents students with moderate Japanese and English proficiency, lower depression scores, higher social connectedness, and lower acculturative stress.
* Cluster 1: Represents students with lower Japanese proficiency, higher depression scores, lower social connectedness, and significantly higher acculturative stress.
* Cluster 2: Represents students with moderate levels of all variables, intermediate depression scores, social connectedness, and acculturative stress.
  
*These clusters provide valuable insights into the different student groups, helping to identify those who may need additional support to prevent depression and improve their overall well-being.*

