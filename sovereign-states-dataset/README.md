## Sovereign States Dataset

This dataset provides a comprehensive list of sovereign states, along with their **common and formal names**, **membership within the UN system**, and details on **sovereignty disputes and recognition status**. The data was originally scraped from [Wikipedia's List of Sovereign States](https://en.wikipedia.org/wiki/List_of_sovereign_states) and processed for clarity and usability.

## Dataset Features

- **Common Name**: The commonly used name of the country or state.
- **Formal Name**: The official/formal name of the country or state.
- **Membership within the UN System**: Indicates whether the country is a UN member state or has observer status.
- **Sovereignty Dispute**: Any sovereignty or territorial disputes involving the state.
- **Further Information**: Additional details regarding the state’s recognition and status.

---

## Dataset Details

### Source
- **Website**: [Wikipedia - List of Sovereign States](https://en.wikipedia.org/wiki/List_of_sovereign_states)
- **Scraped On**: [12 January 2025]
- **Data Cleaning**: Non-ASCII characters, unnecessary symbols, and text within brackets were cleaned for clarity.

### Format
- **File Type**: CSV
- **Encoding**: UTF-8
- **Number of Rows**: [196]
- **Columns**:
  - `Common Name`
  - `Formal Name`
  - `Membership within the UN System`
  - `Sovereignty Dispute`
  - `Further Information`

---


## Citation
If you use this dataset in your research or project, please cite it as follows:

@misc{sovereign_states_dataset,
  - author = {Your Name or Team Name},
  - title = {Sovereign States Dataset},
  - year = {2025},
  - url = {https://huggingface.co/datasets/your-username/sovereign-states-dataset}
}

## Acknowledgments
Special thanks to the contributors of Wikipedia for maintaining and updating the List of Sovereign States. This dataset was scraped and processed using:

- Python
- Scrapy
- Pandas
- Regex for cleaning data

## Contributing
Contributions are welcome! If you spot an issue or have suggestions for improvement:

1. Fork the repository.
2. Make your changes.
3. Submit a pull request.

## Who are the source Data producers ?
The data is machine-generated (using web scraping) and subjected to human additional treatment.

below, I provide the script I created to scrape the data (as well as my additional treatment):

import scrapy


class StatesspiderSpider(scrapy.Spider):
    name = 'statesspider'
    start_urls = ['https://en.wikipedia.org/wiki/List_of_sovereign_states']

    def parse(self, response):
        rows = response.xpath('//table[contains(@class, "wikitable")][1]//tr')  # Locate the main table

        for row in rows[1:]:  # Skip the header row
            common_and_formal_names = row.xpath('td[1]//text()').getall()  # First column
            membership_within_un_system = row.xpath('td[2]//text()').getall()  # Second column
            sovereignty_dispute = row.xpath('td[3]//text()').getall()  # Third column
            further_information = row.xpath('td[4]//text()').getall()  # Fourth column

            # Clean up and join text lists
            common_and_formal_names = ' '.join(common_and_formal_names).strip()
            membership_within_un_system = ' '.join(membership_within_un_system).strip()
            sovereignty_dispute = ' '.join(sovereignty_dispute).strip()
            further_information = ' '.join(further_information).strip()

            yield {
                'Common and Formal Names': common_and_formal_names,
                'Membership within the UN System': membership_within_un_system,
                'Sovereignty Dispute': sovereignty_dispute,
                'Further Information': further_information,
            }

## Usage

### Loading the Dataset in Python
To use the dataset in Python, you can load it using pandas:

```python
import pandas as pd

# Load the dataset
url = "https://huggingface.co/datasets/your-username/sovereign-states-dataset/resolve/main/sovereign_states_cleaned_final.csv"
df = pd.read_csv(url)

# Preview the dataset
print(df.head())
