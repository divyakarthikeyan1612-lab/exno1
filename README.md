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
<img width="1245" height="451" alt="image" src="https://github.com/user-attachments/assets/89a78966-c449-42f6-bc12-10677047d059" />
<img width="1243" height="454" alt="image" src="https://github.com/user-attachments/assets/7fef21b1-be8c-4f6d-b87c-aeab8a644738" />
<img width="1242" height="453" alt="image" src="https://github.com/user-attachments/assets/ea2933d8-61e7-46ee-b4a2-555f70b607dc" />
<img width="1242" height="431" alt="image" src="https://github.com/user-attachments/assets/06b75cb7-4e63-4035-a364-ce59dbac7f2e" />
<img width="1242" height="323" alt="image" src="https://github.com/user-attachments/assets/8ed47f92-9003-49ee-9668-6f019b6ab2c7" />
<img width="1239" height="323" alt="image" src="https://github.com/user-attachments/assets/39043b60-8fb9-4db9-861d-58d6749b929c" />
<img width="1243" height="590" alt="image" src="https://github.com/user-attachments/assets/8c8a9600-8161-4f7f-af41-d560c04e0c31" />
<img width="1240" height="587" alt="image" src="https://github.com/user-attachments/assets/0f1bf43d-e032-4537-b5a8-a5d92653c2f7" />
<img width="1245" height="47" alt="image" src="https://github.com/user-attachments/assets/cc4e42c1-6937-4235-b2fd-9bd663e5b58c" />
<img width="1243" height="455" alt="image" src="https://github.com/user-attachments/assets/77e32c73-eec5-44f9-900a-0c11fee74baa" />
<img width="1241" height="594" alt="image" src="https://github.com/user-attachments/assets/23c075d9-2d3c-4e2b-8395-ae7c204d13a3" />
<img width="1241" height="596" alt="image" src="https://github.com/user-attachments/assets/246ba19f-65ee-41a7-93d0-100c97f814e4" />
<img width="1240" height="736" alt="image" src="https://github.com/user-attachments/assets/24f747aa-f349-4578-ab63-6512217f4c80" />
<img width="1243" height="595" alt="image" src="https://github.com/user-attachments/assets/a9d04236-6b33-4571-b04b-2d8d90e1bcc8" />

# Result
The program for identifying and removing outliers using IQR and Z-score methods has been successfully executed, improving data quality.
