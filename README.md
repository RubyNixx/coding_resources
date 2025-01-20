# Table of contents
1. [Introduction](#introduction)
2. [Pyspark](#pyspark)
   1. [Basic PySpark operations](#pyspark1)
3. [python](#python)
4. [SQL](#sql)
5. [Markdown](#markdown)
   1. [Basic Formatting](#markdownsub1)
   2. [Creating Diagrams](#markdownsub2)
   3. [Highlighting Syntax](#markdownsub3)
   4. [Creating Sections](#markdownsub4)
   5. [Emojis](#markdownsub5)
   6. [Checklists](#markdownsub6)
   7. [Collapsed Sections](#markdownsub7)

## Coding Resources sorted by coding language <a name="introduction"></a>

Range of cheat sheets, coding resources, videos, etc that I want to keep track of &amp; others may find helpful.

## Pyspark <a name="pyspark"></a> :snake:

### Basic PySpark Operations <a name="pyspark1"></a>
[PySpark_RDD_Cheat_Sheet.pdf](https://github.com/user-attachments/files/18294448/PySpark_RDD_Cheat_Sheet.pdf)
Source: https://www.datacamp.com/cheat-sheet/pyspark-cheat-sheet-spark-in-python

Source: https://aeshantechhub.co.uk/databricks-dbutils-cheat-sheet-and-pyspark-amp-sql-best-practice-cheat-sheet/
```python
    # Create a DataFrame from a CSV file:
    df = spark.read.csv("/mnt/datasets/sample.csv", header=True, inferSchema=True)
    
    # Display the first few rows of the DataFrame:
    df.show(5)

    # Select columns from a DataFrame:
    df.select("column1", "column2").show()
```
<b>Best Practice: Avoid using collect()</b>

Avoid using collect() as it brings all data to the driver node, which can cause memory issues.
```python
    # Bad practice - using collect() to bring all data to driver:
    data = df.collect()

    # Better practice - use show() or take() instead:
    df.show(5)
```

<b>Repartitioning DataFrames:</b>

Repartition your DataFrames to optimize performance when dealing with large datasets.
```python
    # Repartition the DataFrame based on a column:
    df = df.repartition("column_name")
```

<b>Check if your df is pandas or pyspark</b>

```python
print(type(example_df))

```

<b>Convert pandas to pyspark df</b>

```python
from pyspark.sql import SparkSession

# Initialize Spark session if not already done
spark = SparkSession.builder.getOrCreate()

# Convert Pandas DataFrames to PySpark
example_df = spark.createDataFrame(example_df)
```

<b>Joins</b>

```python
.join(df1, fn.col("Code") == fn.col("Der_Code"), how="left")
```

<b>See the df in different ways</b>

```python
# Prints the columns & types
df.printSchema()

# Prints list of columns in a paragraph format
print(df.columns)

#Prints disinct values in a given column


```

<b>Drop columns</b>

```python
df = df.drop("column1", "column2")
```


***

## Python <a name="python"></a> :snake:

<b>Cheat Sheets</b>

[python-cheat-sheet.pdf](https://github.com/user-attachments/files/18294457/python-cheat-sheet.pdf)

Source: https://www.datacamp.com/cheat-sheet/python-for-data-science-a-cheat-sheet-for-beginners

[Numpy_Cheat_Sheet.pdf](https://github.com/user-attachments/files/18294463/Numpy_Cheat_Sheet.pdf)

Source: https://www.datacamp.com/cheat-sheet/numpy-cheat-sheet-data-analysis-in-python

[Pandas_Cheat_Sheet.pdf](https://github.com/user-attachments/files/18294466/Pandas_Cheat_Sheet.pdf)

Source: https://www.datacamp.com/cheat-sheet/pandas-cheat-sheet-for-data-science-in-python

[Data_Wrangling_Cheat_Sheet.pdf](https://github.com/user-attachments/files/18294469/Data_Wrangling_Cheat_Sheet.pdf)

Source: https://www.datacamp.com/cheat-sheet/pandas-cheat-sheet-data-wrangling-in-python

[Cheat-Importing Data.pdf](https://github.com/user-attachments/files/18294477/Cheat-Importing.Data.pdf)

[Cheat-Jupyiter Notebooks.pdf](https://github.com/user-attachments/files/18294478/Cheat-Jupyiter.Notebooks.pdf)

[Cheat-Pandas Basics.pdf](https://github.com/user-attachments/files/18294481/Cheat-Pandas.Basics.pdf)

[Python-Cheat-Sheet-for-Scikit-learn-Edureka.pdf](https://github.com/user-attachments/files/18294497/Python-Cheat-Sheet-for-Scikit-learn-Edureka.pdf)

[scikit_learn_cheat.pdf](https://github.com/user-attachments/files/18294504/scikit_learn_cheat.pdf)

[Sklearn-cheat-sheet.pdf](https://github.com/user-attachments/files/18294508/Sklearn-cheat-sheet.pdf)

***

## SQL <a name="sql"></a> :scroll:

SQL Best Practices Cheat Sheet
Source: https://aeshantechhub.co.uk/databricks-dbutils-cheat-sheet-and-pyspark-amp-sql-best-practice-cheat-sheet/

SQL is widely used in Databricks for data querying and transformation. Below are some best practices to keep your queries optimized.

<b>Common SQL Operations:</b>

```sql
    # Creating a table from a DataFrame:
    df.createOrReplaceTempView("temp_table")
    
    # Running a SQL query on the DataFrame:
    spark.sql("SELECT * FROM temp_table").show()
```

<b>Best Practice: Use LIMIT when previewing data</b>

```sql
Avoid fetching large datasets during development. Use LIMIT to preview data instead.

    # Use LIMIT to preview data in SQL:
    spark.sql("SELECT * FROM temp_table LIMIT 10").show()
```

<b>Best Practice: Leverage Caching</b>

```sql
Cache intermediate results in memory to optimise performance for iterative queries.

    # Cache a DataFrame for future use:
    df.cache()
```

<b>Avoid using SELECT * in production</b>

```sql
Using SELECT * can lead to unnecessary data transfer and slow performance, especially with large datasets.

    # Bad practice - using SELECT *:
    spark.sql("SELECT * FROM temp_table")

    # Better practice - select only needed columns:
    
				
```


***

## Markdown <a name="markdown"></a> :blue_book:

<b>Complete formatting cheat sheet:</b>
[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

Some bits from the above I used alot:

### General Formatting <a name="markdownsub1"></a>

Style	Syntax	Keyboard shortcut	Example	Output
```markdown
Bold	** ** or __ __	
Example: **This is bold text**

Italic	* * or _ _
Example: _This text is italicized_

Strikethrough	~~ ~~
Example: ~~This was mistaken text~~

Bold and nested italic	** ** and _ _
Example: **This text is _extremely_ important**

All bold and italic	*** ***
Example: ***All this text is important***

Subscript	<sub> </sub>
Example: This is a <sub>subscript</sub> text

Superscript	<sup> </sup>
Example:This is a <sup>superscript</sup> text	This is a superscript text

Underline	<ins> </ins>
Example:This is an <ins>underlined</ins> text	This is an underlined text
```

<b>Horizontal rules</b>
```markdown
Three or more...

---

Hyphens

***

Asterisks

___

Underscores
```

<b>Insert a hyperlink</b>
```markdown
[Insert your text here](https://www.google.com)
```

### Creating Diagrams <a name="markdownsub2"></a>

You can also use code blocks to create diagrams in Markdown. GitHub supports Mermaid, GeoJSON, TopoJSON, and ASCII STL syntax. For more information, see [Creating diagrams](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams).

### Syntax Highlighting <a name="markdownsub3"></a>
Source: https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks
You can add an optional language identifier to enable syntax highlighting in your fenced code block.

Syntax highlighting changes the color and style of source code to make it easier to read.

For example, to syntax highlight Markdown code:

````
```markdown
hello this is my markdown

You can put code in this block & it will show in a grey box. Change your language as required. More info can be found below on supported languages.
```
````

This will display the code block. If using python, the code block will be formatted with colours.

When you create a fenced code block that you also want to have syntax highlighting on a GitHub Pages site, use lower-case language identifiers. For more information, see [About GitHub Pages and Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#syntax-highlighting).

We use [Linguist](https://github.com/github-linguist/linguist) to perform language detection and to select [third-party grammars](https://github.com/github-linguist/linguist/blob/main/vendor/README.md) for syntax highlighting. You can find out which keywords are valid in the languages [YAML](https://github.com/github-linguist/linguist/blob/main/lib/linguist/languages.yml) file.

### Creating sections <a name="markdownsub4"></a>

To create a contents and sections in your markdown file, you can use the below code.
Source: https://stackoverflow.com/questions/11948245/markdown-to-create-pages-and-table-of-contents

```markdown
# Table of contents
1. [Introduction](#introduction)
2. [Some paragraph](#paragraph1)
    1. [Sub paragraph](#subparagraph1)
3. [Another paragraph](#paragraph2)

## This is the introduction <a name="introduction"></a>
Some introduction text, formatted in heading 2 style

## Some paragraph <a name="paragraph1"></a>
The first paragraph text

### Sub paragraph <a name="subparagraph1"></a>
This is a sub paragraph, formatted in heading 3 style

## Another paragraph <a name="paragraph2"></a>
The second paragraph text
```

### Emojis <a name="markdownsub5"></a>

See full list here :smile::

https://gist.github.com/rxaviers/7360908

### Create a checklist <a name="markdownsub6"></a>

To create a task list, preface list items with a hyphen and space followed by [ ]. To mark a task as complete, use [x].

Source: https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-task-lists#creating-task-lists

```markdown
- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:
```

### Create a collapsed section <a name="markdownsub7"></a>

Markdown code:
````markdown
<details>

<summary>This is a collapsed section</summary>

### You can add a header

You can add text within a collapsed section. 

You can add an image or a code block, too.

```python
   print("Hello World")
```

</details>
````

Preview how it looks:

<details>

<summary>This is a collapsed section</summary>

### You can add a header

You can add text within a collapsed section. 

You can add an image or a code block, too.

```python
   print("Hello World")
```

</details>

