# SmartDataframe

## Installation

The `SmartDataframe` is one of the key components of `pandasai`.

It is a class that extends the `pandas` or `polars` dataframe with the ability to chat with the user.

You can use the `SmartDataframe` as follows:

```python
from pandasai import SmartDataframe
import pandas as pd

# Sample DataFrame
df = pd.DataFrame({
    "country": ["United States", "United Kingdom", "France", "Germany", "Italy", "Spain", "Canada", "Australia", "Japan", "China"],
    "gdp": [19294482071552, 2891615567872, 2411255037952, 3435817336832, 1745433788416, 1181205135360, 1607402389504, 1490967855104, 4380756541440, 14631844184064],
    "happiness_index": [6.94, 7.16, 6.66, 7.07, 6.38, 6.4, 7.23, 7.22, 5.87, 5.12]
})

# Instantiate a LLM
from pandasai.llm import OpenAI

llm = OpenAI(api_token="YOUR_API_TOKEN")

df = SmartDataframe(df, config={"llm": llm})
df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

## Import from csv

You can also import a `SmartDataframe` from a csv file as follows:

```python
from pandasai import SmartDataframe

df = SmartDataframe("data/Loan payments data.csv")
df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

## Import from excel

You can also import a `SmartDataframe` from an excel file as follows:

```python
from pandasai import SmartDataframe

df = SmartDataframe("data/Loan payments data.xlsx")
df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

## Import from google sheets

You can also import a `SmartDataframe` from a google sheet as follows:

```python
from pandasai import SmartDataframe

df = SmartDataframe("https://docs.google.com/spreadsheets/d/fake/edit#gid=0")
df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

## Import from polars

You can also import a `SmartDataframe` from a polars dataframe as follows:

```python
from pandasai import SmartDataframe
import polars as pl

df = SmartDataframe(pl.DataFrame({
    "country": ["United States", "United Kingdom", "France", "Germany", "Italy", "Spain", "Canada", "Australia", "Japan", "China"],
    "gdp": [19294482071552, 2891615567872, 2411255037952, 3435817336832, 1745433788416, 1181205135360, 1607402389504, 1490967855104, 4380756541440, 14631844184064],
    "happiness_index": [6.94, 7.16, 6.66, 7.07, 6.38, 6.4, 7.23, 7.22, 5.87, 5.12]
}))

df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

## Name and description

Sometimes, providing more information about the dataframe can help the AI to better understand the context of the query. You can provide a name and a description to the `SmartDataframe` as follows:

```python
from pandasai import SmartDataframe

df = SmartDataframe("data/Loan payments data.csv", name="Loan payments data", description="This dataset contains information about loans.")
df.chat('Which are the 5 happiest countries?')
# Output: United Kingdom, Canada, Australia, United States, Germany
```

Most of the times, a name is more than enough. The description is useful when the name is not descriptive enough or when you want to provide more information about the dataframe, the links to other dataframes, or about some specific columns of the dataframe that might be poorly named.

If you want to get to know more about the `SmartDataframe` class, check out this video:

[![Intro to SmartDataframe](https://cdn.loom.com/sessions/thumbnails/1ec1b8fbaa0e4ae0ab99b728b8b05fdb-00001.jpg)](https://www.loom.com/embed/1ec1b8fbaa0e4ae0ab99b728b8b05fdb?sid=7370854b-57c3-4f00-801b-69811a98d970 "Intro to SmartDataframe")

## Sample data

PandasAI automatically generates sample data shuffling the rows of the dataframe and anonymizing the values of the columns that are sensitive. This is useful to protect the privacy of the users and to avoid leaking sensitive information.
However, sometimes you might want to pass custom data to the LLM. You can do so by passing a `sample_head` argument to the `SmartDataframe` as follows:

```python
from pandasai import SmartDataframe
import pandas as pd

# Sample DataFrame
sample_df = pd.DataFrame({
    "country": ["United States", "United Kingdom", "France", "Germany", "Italy", "Spain", "Canada", "Australia", "Japan", "China"],
    "gdp": [19294482071552, 2891615567872, 2411255037952, 3435817336832, 1745433788416, 1181205135360, 1607402389504, 1490967855104, 4380756541440, 14631844184064],
    "happiness_index": [6.94, 7.16, 6.66, 7.07, 6.38, 6.4, 7.23, 7.22, 5.87, 5.12]
})

# Instantiate a LLM
from pandasai.llm import OpenAI

df = SmartDataframe("data/Loan payments data.csv", sample_head=sample_df)
```
