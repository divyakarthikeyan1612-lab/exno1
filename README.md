# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt

df = pd.read_csv("Loan_data.csv")

print(df.head())
print(df.tail())
print(df.info())
print(df.describe())

print("Missing values:\n", df.isnull().sum())

df.fillna({
    'Gender': 'Male',
    'Married': 'Yes',
    'Self_Employed': 'No',
    'Credit_History': 1.0
}, inplace=True)

df['LoanAmount'].fillna(df['LoanAmount'].mean(), inplace=True)
df['Loan_Amount_Term'].fillna(df['Loan_Amount_Term'].mean(), inplace=True)

df.fillna(method='ffill', inplace=True)
print("After cleaning:\n", df.isnull().sum())
sns.boxplot(x=df['LoanAmount'])
plt.title("Loan Amount Before Outlier Removal")
plt.show()
df.plot.scatter(x='ApplicantIncome', y='LoanAmount',
                title="Before Outlier Removal")
plt.show()
Q1 = df['LoanAmount'].quantile(0.25)
Q3 = df['LoanAmount'].quantile(0.75)
IQR = Q3 - Q1

print("IQR:", IQR)

outliers = df[(df['LoanAmount'] < (Q1 - 1.5 * IQR)) |
              (df['LoanAmount'] > (Q3 + 1.5 * IQR))]

print("Outliers:\n", outliers['LoanAmount'])
cleaned_df = df[~((df['LoanAmount'] < (Q1 - 1.5 * IQR)) |
                  (df['LoanAmount'] > (Q3 + 1.5 * IQR)))]
sns.boxplot(x=cleaned_df['LoanAmount'])
plt.title("After IQR Outlier Removal")
plt.show()
cleaned_df.plot.scatter(x='ApplicantIncome', y='LoanAmount',
                        title="After IQR Outlier Removal")
plt.show()
z = np.abs(stats.zscore(df['LoanAmount']))

print("Z-scores:\n", z)

df_z = df[z < 3]

print("After Z-score removal:\n", df_z.head())

df_z.plot.scatter(x='ApplicantIncome', y='LoanAmount',
                  title="After Z-score Outlier Removal")
plt.show()
```
<img width="748" height="287" alt="image" src="https://github.com/user-attachments/assets/c103c476-7cf1-4173-85d5-a152e96fa180" />
<img width="757" height="408" alt="image" src="https://github.com/user-attachments/assets/dbe03507-4fb2-40ce-a84c-7109771f1669" />
<img width="505" height="413" alt="image" src="https://github.com/user-attachments/assets/9f05a3a7-94cd-4bfc-af27-9ede5fd20d16" />
<img width="750" height="359" alt="image" src="https://github.com/user-attachments/assets/de446f3f-e0b1-4bc3-87f9-e2396cb53cd9" />
<img width="368" height="396" alt="image" src="https://github.com/user-attachments/assets/bbb18223-24ba-4691-94da-6be779ecab85" />
<img width="272" height="408" alt="image" src="https://github.com/user-attachments/assets/d45e8267-0cb0-4f72-9bb9-3ddd33f9030a" />
<img width="682" height="415" alt="image" src="https://github.com/user-attachments/assets/9cdba7af-e37a-40c4-9285-97f393c27ce0" />
<img width="693" height="89" alt="image" src="https://github.com/user-attachments/assets/8deca563-5138-4e7c-8f34-815d1bad633a" />
<img width="568" height="295" alt="image" src="https://github.com/user-attachments/assets/6b1f8b36-b681-4576-8ddf-cb42f0196939" />
<img width="580" height="142" alt="image" src="https://github.com/user-attachments/assets/a5103315-4bc9-4567-8ddf-91874c64fe0c" />
<img width="183" height="305" alt="image" src="https://github.com/user-attachments/assets/2f927a37-ea2c-4181-a308-6ddf63aac7be" />
<img width="347" height="29" alt="image" src="https://github.com/user-attachments/assets/77f41a8b-ba68-4b7f-9e93-041227369e3e" />
<img width="532" height="297" alt="image" src="https://github.com/user-attachments/assets/ee37cfd4-7544-4ecb-9d42-ef33fe5f9728" />
<img width="564" height="131" alt="image" src="https://github.com/user-attachments/assets/fed01ff2-704f-44a6-a5a3-c9dc9791ed79" />
<img width="521" height="311" alt="image" src="https://github.com/user-attachments/assets/37c06dcb-5378-4ea0-ae06-d400f6d3db83" />
<img width="541" height="113" alt="image" src="https://github.com/user-attachments/assets/47ad814c-ac2f-4237-9a4c-5ffdb1eab306" />
<img width="445" height="213" alt="image" src="https://github.com/user-attachments/assets/e93feba7-8487-49f7-96f2-de9c65d86fcb" />
<img width="544" height="238" alt="image" src="https://github.com/user-attachments/assets/31ab74e6-6396-41cf-8bb0-c8defc7b6bfc" />
<img width="286" height="110" alt="image" src="https://github.com/user-attachments/assets/a3e89ae7-9cb7-42ce-a854-06d8456dd2ae" />
<img width="608" height="295" alt="image" src="https://github.com/user-attachments/assets/2868a41f-558c-4ab6-b9e8-629adb2d6835" />
<img width="586" height="136" alt="image" src="https://github.com/user-attachments/assets/bc188dd5-2116-4120-a1e1-284d0aa0bb20" />

# Result
The program for identifying and removing outliers using IQR and Z-score methods has been successfully executed, improving data quality.
