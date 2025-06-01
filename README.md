# FP-Growth in Python

Ever wonder what products customers buy together, or what trends hide in your sales data? This project offers a robust **Python implementation of the FP-Growth algorithm**, a powerful tool for **market basket analysis**. Beyond just finding frequent purchases, it digs deeper to uncover strong **association rules** and reveal the **correlation** between items using confidence and lift metrics.

---

## Table of Contents

* [Why FP-Growth?](#why-fp-growth)
* [Key Features](#key-features)
* [How It Works Under the Hood](#how-it-works-under-the-hood)
* [Getting Started](#getting-started)
    * [Prerequisites](#prerequisites)
    * [Installation](#installation)
    * [Running the Analysis](#running-the-analysis)
* [Configuration](#configuration)
* [Your Data: The Input Format](#your-data-the-input-format)
* [Interpreting the Results](#interpreting-the-results)
* [Our Development Team](#our-development-team)

---

## Why FP-Growth?

When dealing with massive transaction datasets, finding patterns can be a huge challenge. Traditional methods like Apriori can become computationally expensive, especially when generating countless candidate itemsets. That's where **FP-Growth shines**! It's an efficient, non-candidate-generation algorithm that compresses your data into an **FP-Tree**, making the mining process much faster and more scalable. This project leverages FP-Growth to not only identify frequently co-occurring items but also to define actionable rules and understand their real-world impact.

---

## Key Features

* **Fast FP-Tree Construction**: Quickly builds a compact FP-Tree from your transaction data.
* **Efficient Frequent Itemset Mining**: Discovers all itemsets without generating extra candidates.
* **Actionable Association Rule Generation**: Creates meaningful "if-then" rules from the frequent patterns.
* **Confidence Scoring**: Evaluates the reliability of each rule (how often the consequent appears when the antecedent is present).
* **Lift Correlation Analysis**: Quantifies the relationship between items in a rule – are they positively, negatively, or independently associated?
* **Direct Excel Input**: Conveniently loads transactional data from `.xlsx` files.
* **FP-Tree Visualization**: Generates a clear, visual representation of your FP-Tree using Graphviz.

---

## How It Works Under the Hood

This project orchestrates a series of steps to turn raw transaction data into valuable insights:

1.  **Load Your Data**: We start by reading your transaction data from an Excel file, specifically targeting the second column for your comma-separated items.
2.  **Smart Preprocessing**:
    * First, we count how often each individual item appears.
    * Then, we filter out any items that don't meet your specified **minimum support** threshold (they're too infrequent to be interesting).
    * Finally, we sort the items within each transaction based on their overall frequency – this is crucial for building an efficient FP-Tree.
3.  **Build the FP-Tree**: The preprocessed transactions are then used to construct the FP-Tree. This tree is a highly compressed representation of your dataset, allowing for rapid pattern discovery.
4.  **Mine for Frequent Itemsets**: We traverse the FP-Tree to identify all combinations of items that appear together frequently enough to meet your `min_support` criteria.
5.  **Derive Association Rules**: From these frequent itemsets, we generate all possible **association rules**. Think of them as "If a customer buys X, then they are likely to buy Y."
6.  **Evaluate Rule Strength (Confidence & Lift)**:
    * **Confidence**: For each rule (`A -> B`), we calculate its confidence: the probability of `B` being bought when `A` is already in the basket. We keep only rules that meet your `min_confidence` threshold.
    * **Lift**: This metric tells us the true relationship.
        * **Lift > 1**: Indicates a **positive correlation**; buying `A` *increases* the chances of buying `B`. (e.g., bread and butter)
        * **Lift < 1**: Indicates a **negative correlation**; buying `A` *decreases* the chances of buying `B`. (e.g., diet soda and regular soda)
        * **Lift = 1**: **No correlation**; `A` and `B` are independent.

---

## Getting Started

Ready to analyze your own data? Here's what you'll need and how to get going.

### Prerequisites

Make sure you have:

* **Python 3.x** installed.
* **pip**, Python's package installer.
* **Graphviz** installed on your system for the tree visualization. You can find installation instructions on the [Graphviz website](https://graphviz.org/download/).

### Installation

Clone this repository and install the necessary Python packages:

```bash
git clone [https://github.com/your-username/fp-growth-python.git](https://github.com/your-username/fp-growth-python.git)
cd fp-growth-python
pip install pandas anytree graphviz ipython
```

### Running the Analysis

1. **Prepare your data**: Place your transactional data in an Excel file named `Horizontal_Format.xlsx` in the project directory.
2. **Execute the script**:
    
    Bash
    
    ```
    python main.py
    ```
    

---

## Configuration

You can easily adjust the analysis parameters by modifying these variables at the top of `main.py`:

- `file_path`: Change this if your Excel file has a different name or path. (Default: `"/content/Horizontal_Format.xlsx"`)
- `min_support`: Set the minimum **count** an itemset must achieve to be considered "frequent." (Default: `3`)
- `min_confidence`: Define the minimum **confidence percentage** (as a decimal) for a rule to be considered "strong." (Default: `0.7` for 70%)

---

## Your Data: The Input Format

Your Excel file (`Horizontal_Format.xlsx`) should be structured as follows:

- **Column 1**: Can contain any transaction ID or identifier; this column is currently ignored by the script.
- **Column 2 (index 1)**: Must contain the **items** for each transaction, with items separated by **commas**.

**Example `Horizontal_Format.xlsx` snippet:**

|Transaction ID (ignored)|Items (comma-separated)|
|:--|:--|
|101|Apples,Milk,Bread|
|102|Milk,Sugar,Coffee|
|103|Apples,Milk|
|104|Bread,Sugar|
|105|Milk,Coffee|

Export to Sheets

---

## Interpreting the Results

The script will print various outputs to your console:

- **FP-Tree Structure**: A textual breakdown of how your data is condensed into the tree.
- **FP-Tree Visualization**: A visual graph will pop up (or be saved to a file, depending on your IPython/environment setup) showing the tree's structure and node counts.
- **Frequent Itemsets**: A list of all item combinations that meet your `min_support` threshold. These are the building blocks for your rules.
- **Strong Association Rules**: This is where the actionable insights lie! For each rule (`{Antecedent} -> {Consequent}`), you'll see:
    - **Confidence**: A percentage or decimal indicating the reliability of the rule. Higher confidence means it's more likely for the consequent to occur if the antecedent is present.
    - **Lift**: A crucial metric for understanding correlation.
        - **Lift > 1**: Indicates a **positive correlation**. The items in the antecedent and consequent are bought together _more often_ than expected by chance. This is what you're typically looking for!
        - **Lift < 1**: Indicates a **negative correlation**. The items are bought together _less often_ than expected.
        - **Lift = 1**: Indicates **no correlation**. The purchase of the antecedent has no impact on the purchase of the consequent.

---

## Our Development Team

| Name            | GitHub Profile                      |
| :-------------- | :---------------------------------- |
| [Member 1 Name] | [Link to Member 1's GitHub Profile] |
| [Member 2 Name] | [Link to Member 2's GitHub Profile] |
| [Member 3 Name] | [Link to Member 3's GitHub Profile] |
| [Member 4 Name] | [Link to Member 4's GitHub Profile] |
| [Member 5 Name] | [Link to Member 5's GitHub Profile] |
| [Member 6 Name] | [Link to Member 6's GitHub Profile] |