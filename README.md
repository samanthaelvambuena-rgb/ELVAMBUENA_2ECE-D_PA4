# ELVAMBUENA_2ECE-D_PA4
Made by: Samantha B. Elvambuena | 2ECE-D

This contains the Programming Assignment 4 for our course "Advance Computer Programming" this A.Y. 2026-2027. This project covers three python problems relevant to the Module 4 - Data Wrangling and Data Visualization.
## Objectives of the Experiment
>At the end of this laboratory activity, the student should be able to:
>1. filter tabular data using several categorical and numerical conditions;
>2. construct focused DataFrames by selecting relevant features;
>3. summarize the relationship between categorical features and a numerical variable; and
>4. communicate a data comparison using clear and correctly labeled plots.
## A. VISAYAS COMMUNICATION DATAFRAME
>Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order:
>Name, Gender, Math, Electronics, Average
>Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

The following functions were used in this problem:

Firstly, PANDAS should be initialized for data wrangling as:
```python
import pandas as pd
```
Then, to read and write **EXCEL** file as there is a provided **board2.xlsx** file which contains the needed information **pd.read_excel()** is used. And I used the word **whole** to store the data.
```python
whole=pd.read_excel('board2.xlsx')
whole
```
Next, to get the average of each students **.mean()** is used and to be able to get the mean from the whole row from each student **(axis=1)** is used. Whereas the function **whole[[]]** to indicate the index that will be needed to get the average, such as **'Math', 'Electronics', 'GEAS', 'Communication'**. To indicate a new column **whole['Average']** is used as label for the Average of the students. 
```python
whole['Average']=whole[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
whole
```
To display the rows for **Hometown** with specifically **Visayas** boolean indexing is used which is also used to find the rows for **Track** with only **Communication**. Next, **.loc** is used to indicate the specific columns needed by providing the specific index **(Name, Gender, Math, Electronics, Average)**. And operator **&** is required to evaluate the True only for records meeting both criteria of the two boolean. Lastly, **VisComm** is used to store the data.
```python
VisComm=whole.loc[(whole['Hometown']=='Visayas')&(whole['Track']=='Communication'),['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm
```
Lastly, to print the number of rows **len()** is used to count the number of rows from **VisComm**.
```python
print('Number of Rows',len(VisComm))
```
## B. VISAYAS FEMALE DATAFRAME
>Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only:
>Name, Track, GEAS, Electronics, Average
>Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.

The following functions were used in this problem:

>Since MATPLOTLIB is already initialized in the first problem we can move on to the next function.

To display the rows for **Hometown** with specifically **Visayas** boolean indexing is used which is also used to find the rows for **Gender** with only **Female**. Next, positional slicing **.loc** is used to indicate the specific columns needed by providing the specific index **(Name, Gender, Math, Electronics, Average)**. And operator **&** is required to evaluate the True only for records meeting both criteria of the two boolean. And **VisFemale** is used to store the data.

```python
VisFemale=whole.loc[(whole['Hometown']=='Visayas')&(whole['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale
```

Lastly, **.loc[(VisFemale['Average']>=60)]** is used to indicate the Average in VisFemale with boolean indexing with the operator **>=** to get the students with at least average of 60.
```python
VisFemale.loc[(VisFemale['Average']>=60)]
```
## C. CATEGORY-AVERAGE VISUALIZATION
>Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.
>a. For each feature, compute the mean of Average for every category using Pandas.
>b. Display the three summary tables.
>c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown.
>d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

The following functions were used in this problem:

>Since MATPLOTLIB is already initialized in the first problem we can move on to the next function.

To return a GroupBy object, grouped by values in column track and index in average **.groupby(' ')[' ']**. Then, to get the mean of the Average **.mean** is used. And **.reset_index()** is used to reset index of DataFrame to row numbers, moving index to columns. Lastly, the data are store in **track_mean, gender_mean, hometown_mean** to be able to display the three summary tables.
```python
track_mean=whole.groupby('Track')['Average'].mean().reset_index()
gender_mean=whole.groupby('Gender')['Average'].mean().reset_index()
hometown_mean=whole.groupby('Hometown')['Average'].mean().reset_index()

print('Mean of Average for TRACK:')
display(track_mean)

print('Mean of Average for GENDER:')
display(gender_mean)

print('Mean of Average for HOMETOWN:')
display(hometown_mean)
```
Fristly, to be able to create a bar chart, matplotlib is use and is initialized using **import matplotlib.pyplot as plt**.
```python
import matplotlib.pyplot as plt
plt.figure(figsize=(15,6))

plt.subplot(1,3,1)
plt.bar(track_mean['Track'], track_mean['Average'])
plt.title('Mean Average by Track')
plt.xlabel('Track')
plt.ylabel('Mean Average Score')

plt.subplot(1,3,2)
plt.bar(gender_mean['Gender'], gender_mean['Average'])
plt.title('Mean Average by Gender')
plt.xlabel('Gender')
plt.ylabel('Mean Average Score')

plt.subplot(1,3,3)
plt.bar(hometown_mean['Hometown'], hometown_mean['Average'])
plt.title('Mean Average by Hometown')
plt.xlabel('Hometown')
plt.ylabel('Mean Average Score')

plt.tight_layout()

plt.text(-8, -10, "Interpretation:", fontsize=15)
plt.text(-8, -14, 'The highest in Track is Communication with an average of 67.975.', fontsize=12)
plt.text(-8, -18, 'The highest in Gender is Male with an average of 67.18333.', fontsize=12)
plt.text(-8, -22, 'The highest in Hometown is Luzon with an average of 68.083333.', fontsize=12)

plt.show()
```

Thank you for reading!

To see the main python program, click this [link](https://github.com/samanthaelvambuena-rgb/ELVAMBUENA_2ECE-D_PA4/blob/main/PA4_ELVAMBUENA.ipynb) and download.

### HISTORY
September 17, 2026 - Final touches made the final improvements and corrections to the code and README.

September 16, 2026 - README structure Created the overall structure and organization of the README.

September 16, 2026 - Initial commit Created the initial code and implemented the main functionality of the project.
