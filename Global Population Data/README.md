## List of Countries and Dependencies by Population

This dataset contains population-related information for countries and dependencies, scraped from Wikipedia. The dataset includes the following columns:

1. **Location**: The country or dependency name.
2. **Population**: Total population count.
3. **% of World**: The percentage of the world's population this country or dependency represents.
4. **Date**: The date of the population estimate.
5. **Source**: Whether the source is official or derived from the United Nations.

---

## Dataset Summary

This dataset provides a comprehensive overview of population statistics by country and dependency. It is ideal for researchers, data scientists, and analysts who need accurate and up-to-date population data.

## Dataset Features:
- **Location**: Textual description of the country or territory.
- **Population**: Integer value representing the population size.
- **% of World**: Float representing the percentage of the world's total population.
- **Date**: The date on which the population estimate was recorded.
- **Source**: A textual description of the data source (e.g., United Nations or official national statistics).

---

## Source

The dataset was scraped from the Wikipedia page: [List of countries and dependencies by population](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population).

## Licensing
This dataset is based on data available under the [Creative Commons Attribution-ShareAlike License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License).

---

## Splits

The dataset has one split:
- `train`: Contains all records from the table (approximately 200 entries).

---

## Examples

Here's a sample record from the dataset:

| Location        | Population  | % of World | Date       | Source                   |
|-----------------|-------------|------------|------------|--------------------------|
| China           | 1,411,778,724 | 17.82%     | 2023-01-01 | Official national data   |
| India           | 1,393,409,038 | 17.59%     | 2023-01-01 | United Nations estimate  |
| Tuvalu          | 11,931       | 0.00015%   | 2023-01-01 | United Nations estimate  |

---

## Usage

You can load this dataset using the Hugging Face `datasets` library:

```python
from datasets import load_dataset

dataset = load_dataset("username/dataset_name")
```
