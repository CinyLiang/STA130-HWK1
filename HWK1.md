---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.2
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# STA130 01 Homework

+++

## "Prelecture" HW [*completion prior to next LEC is suggested but not mandatory*]

#### 1. Pick one of the datasets from the ChatBot session(s) of the **TUT demo** (or from your own ChatBot session if you wish) and use the code produced through the ChatBot interactions to import the data and confirm that the dataset has missing values<br>

```{code-cell} ipython3
#import data:

import pandas as pd
data = 'https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-05-05/villagers.csv'
df = pd.read_csv(data)

#missing value confirmation:

missing_values = df.isnull().sum()
print(missing_values)
```

With the code above, the data has been imported and the existance of missing values has been confirmed.

+++

#### 2. Start a new ChatBot session with an initial prompt introducing the dataset you're using and request help to determine how many columns and rows of data a `pandas` DataFrame has, and then

1. use code provided in your ChatBot session to print out the number of rows and columns of the dataset; and,  
2. write your own general definitions of the meaning of "observations" and "variables" based on asking the ChatBot to explain these terms in the context of your dataset

```{code-cell} ipython3
# Get the shape of the DataFrame
rows, columns = df.shape

# Print the number of rows and columns
print(f"Number of rows: {rows}")
print(f"Number of columns: {columns}")
```

An observation refers to one individual data point in a data set, which, in a DataFrame, is represented by one row of data. (For instance, in a DataFrame that records the height and weight of students in a Statistics class, one observation refers to the data point containing one student and his or her corresponding height and weight.)

A variable of a data set refers to a feature included in the data set. (For instance, in the same example of the DataFrame that records the height and weight of students, height and weight are both variables.)

+++

#### 3. Ask the ChatBot how you can provide simple summaries of the columns in the dataset and use the suggested code to provide these summaries for your dataset

```{code-cell} ipython3
print(df.describe())
print(df.describe(include='all'))
print(df.info())
print(df['gender'].value_counts())
print(df['species'].value_counts())
print(df['birthday'].value_counts())
print(df['personality'].value_counts())
print(df['song'].value_counts())
df['phrase'].value_counts()
```

#### 4. If the dataset you're using has (a) non-numeric variables and (b) missing values in numeric variables, explain (perhaps using help from a ChatBot if needed) the discrepancies between size of the dataset given by `df.shape` and what is reported by `df.describe()` with respect to (a) the number of columns it analyzes and (b) the values it reports in the "count" column

```{code-cell} ipython3
new_data = 'https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv'
df2 = pd.read_csv(new_data)

missing_values2 = df2.isnull().sum()
print(missing_values2)

rows2, columns2 = df2.shape
print(f"Number of rows: {rows2}")
print(f"Number of columns: {columns2}")

numeric_summary = df2.describe()
print("\nSummary of numeric columns:")
print(numeric_summary)
```

(a) The first difference between the two commands "df.shape" and "df.describe()" is that the former accounts for all the rows and columns in the DataFrame, whereas the latter only accounts for the numeric columns. 

(b) The second discrepency is that when there are missing numeric values, the "df.describe()" command excludes the missing value when evaluating the "count" section, while "df.shape" reports the exact number of rows regardless of missing values. 

The example data set above is a clear demonstration of the two discrepencies: the "df2.shape" command reports the exact 891 rows and 15 columns, while the "df.describe" command only includes the 6 numeric columns, and its count for the "age" column excludes the 177 missing values, resulting in a count of 714 instead of 891.

+++

#### 5. Use your ChatBot session to help understand the difference between the following and then provide your own paraphrasing summarization of that difference

- an "attribute", such as `df.shape` which does not end with `()`
- and a "method", such as `df.describe()` which does end with `()`

+++

An "attribute" is a variable that belongs to and stores states or characteristics of an object, whereas a "method" is a function that defines an operation or action of the object. In practice, an attribute is accessed like a regular variable and reports features of the object it belongs to, and a method is accessed like a function call and allows operations to be conducted to the object. An addition difference between the two terms is that an attribute can be directly modified, whereas no direct modification can be conducted to methods.

+++

#### ChatGPT Link:
https://chatgpt.com/share/0f6c9293-367a-4e29-8ef4-f2ef7a600a1b

Chat Summary:
1. Importing Libraries and Data: I learned how to import libraries like pandas and load data from a URL into a DataFrame.
2. Attributes and Methods:
Attributes are variables associated with an object, holding its state or data.
Methods are functions within a class that define behaviors or actions an object can perform.
We discussed how to modify both attributes and methods in an object.
3. Exploring a DataFrame:
I learned how to check for missing values, display the first n rows, and access specific columns in a DataFrame.
We also covered how to analyze discrepancies between df.shape and df.describe(), especially with non-numeric columns and missing values.
4. Methods to Summarize Data:
We discussed the use of .describe() for summarizing columns and how it behaves differently with numeric vs. non-numeric columns.
The count in df.describe() reflects the number of non-missing values, which can differ from the total number of rows shown by df.shape.

+++

## "Postlecture" HW [*submission along with "Prelecture" HW is due prior to next TUT*]

#### 6. The `df.describe()` method provides the 'count', 'mean', 'std', 'min', '25%', '50%', '75%', and 'max' summary statistics for each variable it analyzes. Give the definitions (perhaps using help from the ChatBot if needed) of each of these summary statistics

+++

'Count' refers to the number of non-missing entries in a numeric column; 

'Mean' refers to the arithmetic average of the values of non-missing entries in a numeric column; 

'Std' refers to the standard deviation of values of non-missing entries in a numeric column; 

'min' refers to the minimum value among all entries in a numeric column; 

'25%' refers to the 25th percentile (the value that has 25% of other entry values smaller than it and 75% greater than it) of the data in a numeric column;

'50%' refers to the 50th percentile, also known as the median, (the value that has half of other entry values smaller than it and half greater than it) of the data in a numeric column;

'75%' refers to the 75th percentile (the value that has 75% of other entry values smaller than it and 25% greater than it) of the data in a numeric column;

'Max' refers to the maximum value among all entries in a numeric column.

+++

#### 7. Missing data can be considered "across rows" or "down columns".  Consider how `df.dropna()` or `del df['col']` should be applied to most efficiently use the available non-missing data in your dataset and briefly answer the following questions in your own words

1. Provide an example of a "use case" in which using `df.dropna()` might be peferred over using `del df['col']`<br><br>
    
2. Provide an example of "the opposite use case" in which using `del df['col']` might be preferred over using `df.dropna()` <br><br>
    
3. Discuss why applying `del df['col']` before `df.dropna()` when both are used together could be important<br><br>
    
4. Remove all missing data from one of the datasets you're considering using some combination of `del df['col']` and/or `df.dropna()` and give a justification for your approach, including a "before and after" report of the results of your approach for your dataset.

+++

The 'df.dropna()' is a method that removes rows (or columns if the parameter 'axis' is set to 1) with missing values from the DataFrame by providing a new DataFrame by default. In contrast, the 'del df['col']'is a command that removes a specific column regardless of the existance of missing values by directly deleting the specified column from the original DataFrame. In light of the differences:

1. In cases when there are only a few missing values for a large data set (for instance, a data set involving the height, weight, and age of ten thousand highschool students in Toronto that has missing values for only a few observations) and the researchers wants to preserve as many variables included in the DataFrame as possible, the 'df.dropna()' method should be used, which will only remove observations with missing values. In this case, if 'del df['col']' were to be used, several variables might be removed, leaving the researchers with highly insufficient information about the students. Additionally, the 'df.dropna()' method might be preferred to 'del df['col']' when the researchers do not want any changes to be made to the original dataset and only want to preview how the dataset appears without missing values given that 'df.dropna()' creates a new DataFrame.

2. In cases when one or more columns of the data set feature a large number of missing values and the information of these columns are not necessary for the purpose of the study (for instance, a data set used in a study about the mental health condition of highschool students in Toronto that has most entries missing in the column that records  students' favorite songs), the 'del df['col']' command should be used, which will remove this unnecessary column withought reducing too many observations. In this case, if 'df.dropna()' were to be used, most rows will be removed, leaving the researchers with insufficient observations. Additionally, 'del df['col']' might be preferred to 'df.dropna()' when the researchers want to remove missing values directly from the original dataset given that 'del df['col']' directly deletes specified columns from the original DataFrame.

3. In some cases, some columns in a DataFrame might have large numbers of missing values, and using del df['col'] to remove those columns from the data set before applying df.dropna() will effectively preserve observations in the DataFrame. Otherwise, the 'df.dropna()' method will remove all rows with missing values, including observations that researchers might have not intended to remove.

4. The example below removes missing value of the DataFrame from the url 'https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv.' The operation in question 4 illustrates that there are 177 missing values in the column 'age,' 688 in the column 'deck,' and 2 in the column 'embark_down.' In light of this summary, my approach involves firstly, removing the two columns 'age' and 'deck using 'del df['col']',' which both have more than 175 missing values, and secondly, removing the two other remaining missing values by applying 'df.dropna().' This approach is dedicated to preserve as many observations as possible. In fact, the DataFrame before the operation has 891 rows and 15 columns, and the new DataFrame has 889 rows and 13 columns, with only 1 row and 2 columns removed.

```{code-cell} ipython3
# Remove the columns with large numbers of missing values
del df2['age']
del df2['deck']

# Remove the rows with the remaining missing values
df2 = df2.dropna()

# Check for the shape of the DataFrame
rows2, columns2 = df2.shape
print(f"Number of rows: {rows2}")
print(f"Number of columns: {columns2}")

# Check for missing values
df2.isna().sum()
```

#### 8. Give brief explanations in your own words for any requested answers to the questions below

> This problem will guide you through exploring how to use a ChatBot to troubleshoot code using the "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv" data set 
> 
> To initialially constrain the scope of the reponses from your ChatBot, start a new ChatBot session with the following slight variation on the initial prompting approach from "2" above
> - "I am going to do some initial simple summary analyses on the titanic data set I've downloaded (https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv) which has some missing values, and I'd like to get your help understanding the code I'm using and the analysis it's performing"
        
1. Use your ChatBot session to understand what `df.groupby("col1")["col2"].describe()` does and then demonstrate and explain this using a different example from the "titanic" data set other than what the ChatBot automatically provide for you

+++

This command 'df.groupby("col1")["col2"].describe()' groups the DataFrame by each unique value in column1 and asks for the summaries of the entries in column2 in each of the newly created groups. 

The example below uses the same command to group the data from the 'titanic' data set according to each observation's value in the 'sex' column. Specifically, it divides data into the 'male' group and the 'female' group. Then, it asks for the summary of entries in the 'age' column in each group, specifically, the count, mean, standard deviation, minimum value, maximum value, 25th percentile, 50th percentile, and the 75th percentile of age information in the two groups.

```{code-cell} ipython3
new_data = 'https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv'
df2 = pd.read_csv(new_data)

df2.groupby('sex')['age'].describe()
```

2. Assuming you've not yet removed missing values in the manner of question "7" above, `df.describe()` would have different values in the `count` value for different data columns depending on the missingness present in the original data.  Why do these capture something fundamentally different from the values in the `count` that result from doing something like `df.groupby("col1")["col2"].describe()`?

+++

Although 'count' in both commands are influenced by the missingness present in the original data, the 'count' in 'df.describe()' counts all non-missing entries in each column in the DataFrame, whereas the 'df.groupby("col1")["col2"]' command records the counts of entries with non-missing values in each group (grouped by each unique value in column1) in column2. Thus, in essence, the counts generated by the 'df.groupby("col1")["col2"]' command reflects the number of observations in different groups that have valid values in the specified column instead of the total non-missing entries for different data columns.

+++

3. Intentionally introduce the following errors into your code and report your opinion as to whether it's easier to (a) work in a ChatBot session to fix the errors, or (b) use google to search for and fix errors: first share the errors you get in the ChatBot session and see if you can work with ChatBot to troubleshoot and fix the coding errors, and then see if you think a google search for the error provides the necessary toubleshooting help more quickly than ChatGPT<br><br>
    
    1. Forget to include `import pandas as pd` in your code 
       <br> 
       Use Kernel->Restart from the notebook menu to restart the jupyter notebook session unload imported libraries and start over so you can create this error
       <br><br>
       When python has an error, it sometimes provides a lot of "stack trace" output, but that's not usually very important for troubleshooting. For this problem for example, all you need to share with ChatGPT or search on google is `"NameError: name 'pd' is not defined"`<br><br>

```{code-cell} ipython3
data = 'https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-05-05/villagers.csv'
df = pd.read_csv(data)
```

    2. Mistype "titanic.csv" as "titanics.csv"
       <br> 
       If ChatBot troubleshooting is based on downloading the file, just replace the whole url with "titanics.csv" and try to troubleshoot the subsequent `FileNotFoundError: [Errno 2] No such file or directory: 'titanics.csv'` (assuming the file is indeed not present)
       <br><br>
       Explore introducing typos into a couple other parts of the url and note the slightly different errors this produces<br><br>

```{code-cell} ipython3
import pandas as pd
new_data = 'https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanics.csv'
df2 = pd.read_csv(new_data)
```

    3. Try to use a dataframe before it's been assigned into the variable
       <br> 
       You can simulate this by just misnaming the variable. For example, if you should write `df.groupby("col1")["col2"].describe()` based on how you loaded the data, then instead write `DF.groupby("col1")["col2"].describe()`
       <br><br>
       Make sure you've fixed your file name so that's not the error any more<br><br>

```{code-cell} ipython3
df3.describe()
```

    4. Forget one of the parentheses somewhere the code
       <br>
       For example, if the code should be `pd.read_csv(url)` the change it to `pd.read_csv(url`<br><br>

```{code-cell} ipython3
df2.describe(
```

    5. Mistype one of the names of the chained functions with the code 
       <br>
       For example, try something like `df.group_by("col1")["col2"].describe()` and `df.groupby("col1")["col2"].describle()`<br><br>

```{code-cell} ipython3
df2.descrive()
```

    6. Use a column name that's not in your data for the `groupby` and column selection 
       <br>
       For example, try capitalizing the columns for example replacing "sex" with "Sex" in `titanic_df.groupby("sex")["age"].describe()`, and then instead introducing the same error of "age"<br><br>

```{code-cell} ipython3
df2.groupby('sex')['Age'].describe()
```

    7. Forget to put the column name as a string in quotes for the `groupby` and column selection, and see if the ChatBot and google are still as helpful as they were for the previous question
       <br>
       For example, something like `titanic_df.groupby(sex)["age"].describe()`, and then `titanic_df.groupby("sex")[age].describe()`

```{code-cell} ipython3
df2.groupby('sex')[age].describe()
```

In my opinion, fixing errors with Chatbot is certainly easier than doing so with Google. Since the interaction with Chatbot is conducted in form of chatting, I am able to provide detailed descriptions of the error information I encountered when running my code, whereas Google only allows me to type a few kew words and phrases when browsing for error fixation. This results in Chatbot giving me a more accurate fixation to my code. Also, since I can provide Chatbot with my original code, Chatbot can directly detect the problems in my code instead of only giving me some general interpretations based on the error information. Additionally, for some error informations (such as the one I got in the fourth situation, "SyntaxError: incomplete input"), Google cannot give a general interpretation immediately. I had to look through 5 results that were highly unrelated to my code errors before finding one result that suggests the missing of a bracket. Hence, using Chatbot for troubleshooting is more straightforward, efficient, and effective for me despite some other benefits Googling might have (for instance, since Google provides answers from a variaty of sources, its reliability might be better).

+++

#### 9. Have you reviewed the course [wiki-textbook](https://github.com/pointOfive/stat130chat130/wiki) and interacted with a ChatBot (or, if that wasn't sufficient, real people in the course piazza discussion board or TA office hours) to help you understand all the material in the tutorial and lecture that you didn't quite follow when you first saw it?

+++

Yes.

+++

#### ChatGPT Link:
https://chatgpt.com/share/d588d5fb-1d94-4fb0-a047-c8d97f08fa9d


Chat Summary:


Pandas Commands:


We discussed the differences between df.dropna() (which removes rows/columns with missing values) and del df['col'] (which deletes a specific column).

The command df.groupby("col1")["col2"].describe() was explained, showing how it provides descriptive statistics of "col2" for each group in "col1".

We clarified how missing values affect the count in df.groupby("col1")["col2"].describe(), and compared the count from df.describe() (overall) versus the groupby version (per group).


Code Errors and Fixes:


We addressed several errors in my code:
NameError: name 'pd' is not defined was fixed by adding the necessary pandas import statement (import pandas as pd).

FileNotFoundError was explained as resulting from an incorrect file path or a missing file.

NameError: name 'df3' is not defined happened because df3 was not initialized before being used.

SyntaxError: incomplete input in my code "df2.describe(" was due to missing closing parentheses, which we corrected.

AttributeError: 'DataFrame' object has no attribute 'descrive' was a typo issue; it should be describe().

KeyError: 'Column not found: Age' and NameError: name 'age' is not defined occurred because either the column did not exist or was being referenced incorrectly. Quotes around column names ('age') resolved this.
