# Train with your own settings

You can train PandasAI to understand your data better and to improve its performance. Training is as easy as calling the `train` method on the `SmartDataframe`, `SmartDatalake` or `Agent`.

There are two kinds of training:

- instructions training
- q/a training

<iframe title='Train on PandasAI' style="width: 100%; max-width: 982px; min-height: 570px;" src="https://app.gemoo.com/embed/home?codeId=MlQ5yGpLeN59r"  frameborder="0" allowfullscreen loading="lazy"></iframe>
<br />

## Prerequisites

Before you start training PandasAI, you need to set your PandasAI API key. You can generate your API key by signing up at [https://pandabi.ai](https://pandabi.ai).

Then you can set your API key as an environment variable:

```python
import os

os.environ["PANDASAI_API_KEY"] = "YOUR_PANDASAIAPI_KEY"
```

## Instructions training

Instructions training is used to teach PandasAI how you expect it to respond to certain queries. You can provide generic instructions about how you expect the model to approach certain types of queries, and PandasAI will use these instructions to generate responses to similar queries.

For example, you might want the LLM to be aware that your company's fiscal year starts in April, or about specific ways you want to handle missing data. Or you might want to teach it about specific business rules or data analysis best practices that are specific to your organization.

To train PandasAI with instructions, you can use the `train` method on the `Agent`, `SmartDataframe` or `SmartDatalake`, as it follows:

```python
from pandasai import Agent

# Set your PandasAI API key (you can generate one signing up at https://pandabi.ai)
os.environ["PANDASAI_API_KEY"] = "YOUR_PANDASAI_API_KEY"

agent = Agent("data.csv")
agent.train(docs="The fiscal year starts in April")

response = agent.chat("What is the total sales for the fiscal year?")
print(response)
# The model will use the information provided in the training to generate a response
```

Your training data is persisted, so you only need to train the model once.

## Q/A training

Q/A training is used to teach PandasAI the desired process to answer specific questions, enhancing the model's performance and determinism. One of the biggest challenges with LLMs is that they are not deterministic, meaning that the same question can produce different answers at different times. Q/A training can help to mitigate this issue.

To train PandasAI with Q/A, you can use the `train` method on the `Agent`, `SmartDataframe` or `SmartDatalake`, as it follows:

```python
from pandasai import Agent

agent = Agent("data.csv")

# Train the model
query = "What is the total sales for the current fiscal year?"
response = """
import pandas as pd

df = dfs[0]

# Calculate the total sales for the current fiscal year
total_sales = df[df['date'] >= pd.to_datetime('today').replace(month=4, day=1)]['sales'].sum()
result = { "type": "number", "value": total_sales }
"""
agent.train(queries=[query], codes=[response])

response = agent.chat("What is the total sales for the last fiscal year?")
print(response)
# The model will use the information provided in the training to generate a response
```

Also in this case, your training data is persisted, so you only need to train the model once.
