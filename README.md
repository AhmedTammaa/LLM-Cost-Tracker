# LLM and Embedding Cost Tracker

## Overview

Welcome to the **LLM and Embedding Cost Tracker**! This Python library provides wrapper classes to track and accumulate cost and token usage data for multiple Large Language Model (LLM) calls and embedding operations. If you're tired of rewriting cost-tracking code for different projects, this tool is here to simplify your workflow.

**Note:** This repository is in its early stages, and more features are coming soon. Stay tuned!

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [LLMCostTracker](#llmcosttracker)
  - [EmbeddingCostCalculator](#embeddingcostcalculator)
- [Supported Models](#supported-models)
- [Contributing](#contributing)
- [License](#license)
- [Future Plans](#future-plans)

## Features

- **LLMCostTracker**: Easily track total cost, input tokens, and output tokens for multiple LLM calls.
- **EmbeddingCostCalculator**: Calculate and track embedding costs for various models.
- **Extensible**: Designed to support additional models and features in future updates.
- **Easy Integration**: Seamlessly integrate with your existing LLM projects.

## Installation

Clone the repository and install the required packages:

```bash
git clone https://github.com/yourusername/llm-cost-tracker.git
cd llm-cost-tracker
pip install -r requirements.txt
```

*Replace `yourusername` with your actual GitHub username.*

## Usage

### LLMCostTracker

The `LLMCostTracker` class helps you track and accumulate the cost and token usage of your LLM calls.

#### Example

```python
from llm_cost_tracker import LLMCostTracker

# Initialize the tracker
tracker = LLMCostTracker()

# Simulate an LLM call with a callback object 'cb'
class Callback:
    def __init__(self, total_cost, prompt_tokens, completion_tokens):
        self.total_cost = total_cost
        self.prompt_tokens = prompt_tokens
        self.completion_tokens = completion_tokens

# Example callback data
cb = Callback(total_cost=0.01, prompt_tokens=100, completion_tokens=200)

# Add the call data to the tracker
tracker.add_call(cb)

# Get total costs and tokens
totals = tracker.get_totals()
print(totals)
```

**Output:**

```
{'total_cost': 0.01, 'input_tokens': 100, 'output_tokens': 200}
```

#### Methods

- `add_call(cb)`: Adds a single LLM call's cost and token data to the tracker.
- `get_totals()`: Returns accumulated total cost, input tokens, and output tokens.
- `add_two_llm_call_data(data1, data2)`: Adds two `LLMCallData` instances together.
- `add_list_llm_call_data(data_list)`: Accumulates a list of `LLMCallData` instances into a single total.

### EmbeddingCostCalculator

The `EmbeddingCostCalculator` class calculates and tracks the cost of embedding operations based on the provided model.

#### Example

```python
from llm_cost_tracker import EmbeddingCostCalculator

# Initialize the calculator with a specific model
with EmbeddingCostCalculator(model_name="text-embedding-3-large") as calculator:
    # Your list of document chunks
    paragraphs = [
        {'page_content': 'This is the first paragraph.'},
        {'page_content': 'This is the second paragraph.'},
        # Add more paragraphs as needed
    ]
    # Calculate the embedding cost
    calculator(paragraphs)
    print(calculator.embedding_cost_summary)
```

**Output:**

```
{
    'model_name': 'text-embedding-3-large',
    'total_tokens': 14,
    'total_cost': 0.0
}
```

#### Methods

- `__call__(paragraphs)`: Calculates the cost based on the provided paragraphs.
- `add_documents_with_cost(index, documents)`: Calculates cost and adds documents to the index.

## Supported Models

### Embedding Models

- **text-embedding-3-small**
- **text-embedding-3-large**
- **ada-v2**

*Note: More models will be supported in future updates.*

## Contributing

Contributions are welcome! If you'd like to help improve this project, please:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request for review.

For major changes, please open an issue first to discuss what you'd like to change.

## Future Plans

- **Additional Models**: Support for more LLM and embedding models.
- **Enhanced Features**: Improved cost estimation algorithms and integration capabilities.
- **Comprehensive Documentation**: Detailed guides and more usage examples.
- **Community Engagement**: Foster a community around the project for shared learning and collaboration.

---

*By using the LLM and Embedding Cost Tracker, you can efficiently monitor and manage the costs associated with your LLM and embedding operations, making your development process smoother and more cost-effective.*
