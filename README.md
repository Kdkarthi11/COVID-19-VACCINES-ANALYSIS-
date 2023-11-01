
# Covid - 19 Vaccine Analysis

To understand how effective vaccines are at preventing the virus, identify areas that need more vaccinations, and make informed decisions to protect public health.

## Required libraries

->pip install pandas

->pip install seaborn

->pip install matplotlib

->pip install plotly
## Dataset

https://www.kaggle.com/datasets/gpreda/covid-world-vaccination-progress
## View the Dataset

->Load the dataset into a DataFrame

df=pd.read_csv('Documents/country_vaccinations.csv')

-> View the first few rows of the dataset

df
## Data Preprocessing

•	Handle missing data by replacing NaN values with zeros.


•	Reset the index.


•	Convert the 'date' column to a datetime format for ease of handling.

## Data Visualizations


•	Select specific countries (e.g., Bangladesh, India, China, Pakistan) for analysis.

•	Analyze and visualize total and daily vaccinations for these countries.

•	Compare vaccination efforts by plotting relevant graphs.

## Key Findings

•	The analysis showed the progress of COVID-19 vaccinations in specific countries 
(Bangladesh, India, China, Pakistan).

•	Total and daily vaccinations were visualized over time to track the vaccination
 efforts in these countries.

•	Comparative analysis revealed the top countries in terms of total vaccinations and vaccinations per 100 people.

•	The top vaccines used in different countries were identified and visualized.

## Usage/Examples

```python



#import the required libraries
#import the required dataset
#view the dataset

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
get_ipython().run_line_magic('matplotlib', 'inline')
df=pd.read_csv('Documents/country_vaccinations.csv')
df.head()




df1=df.dropna()
print(df1)




df1= df.reset_index()
print(df1)



df.info()





df.describe()





df.isnull().sum()





df.fillna(0, inplace = True)
df.drop(df.index[df['iso_code'] == 0], inplace = True)





df.isnull().sum()





#The date is in the 'object' format. Let us change it to Datetime format for easy handling and plotting.
df['date'] =  pd.to_datetime(df['date'], format='%Y-%m-%d')




df.columns





df.drop(["people_fully_vaccinated","daily_vaccinations_raw","people_vaccinated_per_hundred",
       "people_fully_vaccinated_per_hundred","daily_vaccinations_per_million","source_name","source_website"],axis=1)




#BANGALADESH
df_BGD = df[df["iso_code"] == 'BGD'].copy()
df_BGD





#Drop the dates with missing values, previously NaN that we filled with 0. 
df_BGD.drop(df_BGD.index[df_BGD['total_vaccinations'] == 0], inplace = True)





#Plot total vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_BGD, x="date", y="total_vaccinations")
plt.title("Total vaccinations in the BGD")
plt.xticks(rotation=45)
plt.show()





#Plot daily vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_BGD, x="date", y="daily_vaccinations")

plt.xticks(rotation=90)
plt.title("Daily vaccinations in the BGD")





#INDIA
df_IND = df[df["iso_code"] == 'IND'].copy()
df_IND=df_IND.head(10)
df_IND




#Drop the dates with missing values, previously NaN that we filled with 0. 
df_IND.drop(df_IND.index[df_IND['total_vaccinations'] == 0], inplace = True)





#Plot total vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_IND, x="date", y="total_vaccinations")
plt.title("Total vaccinations in the IND")
plt.xticks(rotation=45)
plt.show()





#Plot daily vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_IND, x="date", y="daily_vaccinations")

plt.xticks(rotation=90)
plt.title("Daily vaccinations in the IND")





#CHINA
df_CHN = df[df["iso_code"] == 'CHN'].copy()
df_CHN=df_CHN.head(20)
df_CHN





#Drop the dates with missing values, previously NaN that we filled with 0. 
df_CHN.drop(df_CHN.index[df_CHN['total_vaccinations'] == 0], inplace = True)





#Plot total vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_CHN, x="date", y="total_vaccinations")
plt.title("Total vaccinations in the CHN")
plt.xticks(rotation=45)
plt.show()





#Plot daily vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_CHN, x="date", y="daily_vaccinations")

plt.xticks(rotation=90)
plt.title("Daily vaccinations in the CHN")





#PAKISTAN
df_PAK = df[df["iso_code"] == 'PAK'].copy()
df_PAK=df_PAK.head(20)
df_PAK




#Drop the dates with missing values, previously NaN that we filled with 0. 
df_PAK.drop(df_PAK.index[df_PAK['total_vaccinations'] == 0], inplace = True)





#Plot total vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_PAK, x="date", y="total_vaccinations")
plt.title("Total vaccinations in the PAK")
plt.xticks(rotation=45)
plt.show()





#Plot daily vaccinations as a function of date
plt.figure(figsize=(18,6))
sns.lineplot(data=df_PAK, x="date", y="daily_vaccinations")

plt.xticks(rotation=90)
plt.title("Daily vaccinations in the PAK")





#Group by total vaccinations given by country and sort descending to identify the top 10 countries. 
vacc_by_country = df.groupby('country').max().sort_values('total_vaccinations', ascending=False)
vacc_by_country = vacc_by_country.iloc[:10]
vacc_by_country





#Now sort by total vaccinations per 100
vacc_by_country = vacc_by_country.sort_values('total_vaccinations_per_hundred', ascending=False)
vacc_by_country




plt.figure(figsize=(18, 6))
plt.bar(vacc_by_country.index, vacc_by_country.total_vaccinations_per_hundred)

plt.xticks(rotation = 90)
plt.ylabel('Vaccinations per 100')
plt.xlabel('Country')
plt.show()





total_vacc_by_country = df.groupby('country').max().sort_values('total_vaccinations', ascending=False)
total_vacc_by_country = total_vacc_by_country.iloc[:10]
total_vacc_by_country





plt.figure(figsize=(16, 7))
plt.bar(total_vacc_by_country.index, total_vacc_by_country.total_vaccinations)

plt.title('Total vaccinations per country')
plt.xticks(rotation = 90)
plt.ylabel('Total vaccinations')
plt.xlabel('Country')
plt.show()





#Sort by total vaccinations delivered by countries and group by vaccines. 
vacc_names_by_country = df.groupby('vaccines').max().sort_values('total_vaccinations', ascending=False)
vacc_names_by_country.head()




#Get the top 10 vaccines by country for easy plotting
vacc_names_by_country = vacc_names_by_country.iloc[:10]
vacc_names_by_country
     





#Reset index to move vaccines from being index to a column. 
#This makes it easy for us to plot using Seaborn, especially if we want to sort by country. 
vacc_names_by_country=vacc_names_by_country.reset_index()
vacc_names_by_country





plt.figure(figsize=(12,8))

sns.barplot(data = vacc_names_by_country, x='vaccines', y = 'total_vaccinations', hue = 'country', dodge=False)
plt.xticks(rotation=90)




## Used By

This project is used by the following companies:

- Serum Institute of India (SII)
- AstraZeneca
- Oxford


## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?

 COVID-19 vaccine data analysis can be a valuable learning experience and a practical application of data analysis skills. To overcome challenges, a combination of data science techniques, domain knowledge, and careful consideration of ethical and practical issues is essential.


## Conclusion

  In the challenging landscape of the COVID-19 pandemic, the analysis of vaccine data has proven to be an indispensable tool. It has enabled us to understand the effectiveness of vaccines, identify areas where vaccinations are needed most, and make informed decisions. With the power of data science, Python, and innovative technologies, we've gained crucial insights that guide our response to the pandemic. As we continue this journey, data-driven analysis remains a cornerstone in our collective effort to combat COVID-19 and protect public health.