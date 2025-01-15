## Greenhouse Gas Emissions Dataset

This dataset contains information about greenhouse gas (GHG) emissions (ktCO2/year) for various countries, territories, regions, and groups, scraped from Wikipedia. It provides detailed data about emissions over time and includes per capita emissions, percentage of global total, and the change in emissions since 1990.

---

## Dataset Summary

This dataset is a valuable resource for analyzing greenhouse gas emissions across countries, regions, and the world. It provides a comprehensive time series of emissions data along with additional insights such as:
- Percentage of global total emissions.
- Changes in emissions since 1990 (baseline year).
- Per capita emissions.

## Dataset Features:
- **Country/Territory/Region/Group**: Name of the country, region, or group.
- **GHG Emissions (ktCO2/year)**: Total greenhouse gas emissions for each year (1970, 1990, 2000, 2010, 2020, 2021, 2022, and 2023).
- **% of Global Total**: The percentage of total global emissions contributed by the country or region.
- **Change (1990=100%)**: The change in emissions since 1990, expressed as a percentage.
- **GHG Emissions Per Capita**: Emissions per person for the country or region.

---

## Source

The dataset was scraped from the Wikipedia page: [List of countries by greenhouse gas emissions](https://en.wikipedia.org/wiki/List_of_countries_by_greenhouse_gas_emissions).

### Licensing
The data is available under the [Creative Commons Attribution-ShareAlike License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License).

---

## Splits

The dataset contains one split:
- **train**: Includes all rows and columns from the table (approximately 200 entries).

---

## Examples

Here's a sample record from the dataset:

| Country/Territory/Region/Group | 2023 GHG Emissions (ktCO2) | % of Global Total | Change (1990=100%) | 2023 Per Capita Emissions (tCO2) |
|--------------------------------|----------------------------|--------------------|--------------------|-----------------------------------|
| China                          | 11,474,238                | 30.69%            | 270%              | 8.1                               |
| United States                  | 5,106,856                 | 13.64%            | 93%               | 15.3                              |
| Tuvalu                         | 12                        | 0.00003%          | 110%              | 1.0                               |

---

## Usage

You can load this dataset using the Hugging Face `datasets` library:

```python
from datasets import load_dataset

dataset = load_dataset("username/ghg_emissions")
```
