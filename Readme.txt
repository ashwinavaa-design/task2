#1: import libaris
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns


#2: Load Dataset
df = pd.read_csv("cleaned_employee_data.csv")

# clean column names
df.columns = df.columns.str.strip().str.lower()

print("Dataset Loaded")
print(df.head())


#3: Basic Dataset Information
print("\nShape of Dataset:", df.shape)

print("\nColumns:")
print(df.columns)

print("\nDataset Info:")
print(df.info())


#4: Descriptive Statistics
print("\nStatistical Summary:")
print(df.describe())


#6: Univariate Analysis (One Column)
  # Histogram (Numeric Data)
for col in numeric_cols:
    plt.figure()
    df[col].hist()
    plt.title(f"{col} Distribution")
    plt.xlabel(col)
    plt.ylabel("Count")
    plt.show()

  # Bar Chart (Categorical Data)
for col in categorical_cols:
    plt.figure()
    df[col].value_counts().plot(kind='bar')
    plt.title(f"{col} Count")
    plt.show()

#7: SQL-Type Analysis (GroupBy)
for col in categorical_cols:
    print(f"\nGrouping by {col}")
    print(df.groupby(col)[numeric_cols[0]].mean())


#8: Multivariate Analysis 
     #Scatter Plot (Numeric vs Numeric)
   if len(numeric_cols) >= 2:
     plt.figure()
     sns.scatterplot(x=numeric_cols[0], y=numeric_cols[1], data=df)
     plt.title(f"{numeric_cols[0]} vs {numeric_cols[1]}")
     plt.show()
    #Box Plot (Categorical vs Numeric)
   if len(categorical_cols) > 0 and len(numeric_cols) > 0:
     plt.figure()
     sns.boxplot(x=categorical_cols[0], y=numeric_cols[0], data=df)
     plt.title(f"{numeric_cols[0]} by {categorical_cols[0]}")
     plt.show()


#9: Correlation Analysis
 plt.figure()
sns.heatmap(df[numeric_cols].corr(), annot=True)
plt.title("Correlation Matrix")
plt.show() 	


#10: Business Insights (Print Statements)
print("\n🔍 Key Insights:")

for col in numeric_cols:
    print(f"\n{col}:")
    print("Average:", df[col].mean())
    print("Max:", df[col].max())
    print("Min:", df[col].min())


#11: Final Output
print("\n Task 2 (EDA & Business Intelligence) Completed Successfully!")