## World Heavyweight Boxing Champions Dataset

This dataset contains information about world heavyweight boxing champions extracted from the [Wikipedia page](https://en.wikipedia.org/wiki/List_of_world_heavyweight_boxing_champions). It includes details such as champion names, reign periods, and title defenses.

## Dataset Structure

### Columns
| Column Name           | Description                                           |
|-----------------------|-------------------------------------------------------|
| `No`                 | The ordinal number of the champion.                   |
| `Champion`           | Name of the heavyweight boxing champion.              |
| `Recognition`        | The organization or title under which the reign was recognized. |
| `Begin_reign`        | The date the reign began (YYYY-MM-DD format).          |
| `End_reign`          | The date the reign ended (YYYY-MM-DD format).          |
| `Days`               | The total number of days in the reign.                |
| `Title_defenses`     | The number of title defenses during the reign.         |
| `Additional_recognition` | Other notable details about the champion or reign. |

### Who are the source Data producers ?
The data is machine-generated (using web scraping) and subjected to human additional treatment.

below, I provide the script I created to scrape the data (as well as my additional treatment):
```
import scrapy
import re

class ChampionsSpider(scrapy.Spider):
    name = "champions"
    start_urls = [
        "https://en.wikipedia.org/wiki/List_of_world_heavyweight_boxing_champions"
    ]

    def parse(self, response):
        # Locate the second table on the page
        table = response.xpath('(//table[contains(@class, "wikitable")])[2]')
        rows = table.xpath('.//tr')

        def clean_text(text):
            """Remove special characters, extra whitespace, and newlines."""
            if text:
                text = re.sub(r'\s+', ' ', text)  # Replace multiple spaces/newlines with a single space
                text = text.strip()  # Remove leading and trailing spaces
                return text
            return None

        for row in rows[1:]:  # Skip the header row
            yield {
                "No": clean_text(row.xpath('.//td[1]//text()').get()),
                "Champion": clean_text(row.xpath('.//td[2]//text()').get()),
                "Recognition": clean_text(row.xpath('.//td[3]//text()').get()),
                "Begin_reign": clean_text(row.xpath('.//td[4]//text()').get()),
                "End_reign": clean_text(row.xpath('.//td[5]//text()').get()),
                "Days": clean_text(row.xpath('.//td[6]//text()').get()),
                "Title_defenses": clean_text(row.xpath('.//td[7]//text()').get()),
                "Additional_recognition": clean_text(row.xpath('.//td[8]//text()').get()),
            }
```
### Dataset Creation
- Source: Data was scraped from the Wikipedia page using a Python Scrapy script.
- Cleaning: Special characters and extra whitespace were removed to ensure a clean dataset.

### Usage
This dataset can be used for:

- Sports Analysis: Analyze trends in boxing history.
- Historical Research: Study the evolution of world heavyweight boxing champions.
- Data Analysis: Perform statistical analysis on reign durations and title defenses.

### License
The dataset is derived from content licensed under the Creative Commons Attribution-ShareAlike 3.0 Unported License (CC BY-SA 3.0).

### Limitations
The dataset is limited to the information available on Wikipedia as of the scraping date.
Some rows might contain incomplete or approximate data due to the source material.

### Acknowledgments
Special thanks to Wikipedia contributors for compiling the original data.     

### Example Row
```json
{
  "No": "1",
  "Champion": "Bob Fitzsimmons",
  "Recognition": "World",
  "Begin_reign": "1897-03-17",
  "End_reign": "1899-06-09",
  "Days": "815",
  "Title_defenses": "2",
  "Additional_recognition": "First three-division champion"
}
```
