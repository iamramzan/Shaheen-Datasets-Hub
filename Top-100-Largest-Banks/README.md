## Dataset Summary
This dataset contains information about the largest banks globally, including their rank, name, and total assets (in US$ billion as of 2023). The data was scraped from [Wikipedia's List of Largest Banks](https://en.wikipedia.org/wiki/List_of_largest_banks). It can be used for financial analysis, market research, and educational purposes.

## Dataset Structure
### Columns
- **Rank**: The rank of the bank based on total assets.
- **Bank Name**: The name of the bank.
- **Total Assets (2023, US$ billion)**: The total assets of the bank in billions of US dollars as of 2023.

### Example
| Rank | Bank Name          | Total Assets (2023, US$ billion) |
|------|--------------------|-----------------------------------|
| 1    | Industrial & Commercial Bank of China (ICBC) | 5,000 |
| 2    | China Construction Bank  | 4,500 |

## Source
The data was scraped from [Wikipedia's List of Largest Banks](https://en.wikipedia.org/wiki/List_of_largest_banks) using Python and Scrapy.

## Usage
This dataset can be used for:
- Financial market research.
- Trend analysis in global banking.
- Educational purposes and data visualization.

## Licensing
The data is publicly available under [Wikipedia's Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use).

## Limitations
- The data may not reflect real-time changes as it was scraped from a static page.
- Possible inaccuracies due to updates or inconsistencies on the source page.

## Acknowledgements
Thanks to Wikipedia and the contributors of the "List of Largest Banks" page.

## Citation
If you use this dataset, please cite it as:
```
@misc{largestbanks2023,
  author = {Your Name or Organization},
  title = {Largest Banks Dataset},
  year = {2023},
  publisher = {Hugging Face},
  url = {https://huggingface.co/datasets/your-dataset-name}
}
```
## Who are the source Data producers ?
The data is machine-generated (using web scraping) and subjected to human additional treatment.

below, I provide the script I created to scrape the data (as well as my additional treatment):

import scrapy

class LargestBanksSpider(scrapy.Spider):
    name = "largest_banks"
    start_urls = ["https://en.wikipedia.org/wiki/List_of_largest_banks"]

    def parse(self, response):
        # Locate the table containing the data
        table = response.xpath("//table[contains(@class, 'wikitable')]")

        # Extract rows from the table
        rows = table.xpath(".//tr")

        for row in rows[1:]:  # Skip the header row
            rank = row.xpath(".//td[1]//text()").get()
            bank_name = row.xpath(".//td[2]//a/text() | .//td[2]//text()")
            total_assets = row.xpath(".//td[3]//text()").get()

            # Extract all text nodes for bank name and join them
            bank_name = ''.join(bank_name.getall()).strip() if bank_name else None

            if rank and bank_name and total_assets:
                yield {
                    "Rank": rank.strip(),
                    "Bank Name": bank_name,
                    "Total Assets (2023, US$ billion)": total_assets.strip()
                }
