# Web Scraping and Pandas Project

# web_scraping_pandas_python_project

---

Python-based Web Scraping and Data Processing project implemented in a Jupyter Notebook to extract data from a Wikipedia page, process it into a Pandas DataFrame, and export it as a CSV file.

---

## Author

**Charles Pugh**

Google-certified Data Analyst

Email: [charlespughtech@gmail.com](mailto:charlespughtech@gmail.com)

LinkedIn: [https://www.linkedin.com/in/charlespughtech/](https://www.linkedin.com/in/charlespughtech/)

Date: June 01, 2025

---

## Table of Contents

- [Web Scraping and Pandas Project](#web-scraping-and-pandas-project)
- [web_scraping_pandas_python_project](#web_scraping_pandas_python_project)
  - [Author](#author)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
  - [Requirements](#requirements)
  - [Project Structure](#project-structure)
  - [Data Scraping](#data-scraping)
  - [Data Processing](#data-processing)
  - [Usage](#usage)
  - [Contact](#contact)

---

## Project Overview

This project scrapes data from a Wikipedia page listing the largest U.S. companies by revenue, extracts a table, processes it into a structured Pandas DataFrame, and saves the results as a CSV file. The project uses `requests` and `BeautifulSoup` for web scraping and `Pandas` for data manipulation. The dataset is sourced directly from the web, requiring no external files as input.

The scraped table includes the following columns:
- Rank
- Name
- Industry
- Revenue (USD millions)
- Revenue growth
- Employees
- Headquarters

---

## Requirements

- Python 3.12 or higher
- Jupyter Notebook (recommended via Anaconda or JupyterLab)
- Python libraries:
  - `requests` (for HTTP requests)
  - `beautifulsoup4` (for HTML parsing)
  - `pandas` (for data processing)

---

## Project Structure

```bash
web_scraping_pandas_python_project/
├── README.md                                   # Project overview and instructions
├── data_scraping_pandas_python_project.ipynb   # Jupyter Notebook with web scraping code
├── web_scraped_table.csv                      # Output CSV file (generated after running the notebook)
└── data_scraping_pandas_python_project.html    # HTML export of the Jupyter Notebook
```

---

## Data Scraping

The data scraping process retrieves a table from a Wikipedia page using `requests` and `BeautifulSoup`. Follow these steps to replicate:

- **Fetch and Parse Webpage**:
  - Use `requests.get()` to send an HTTP GET request to the URL: [https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue).
  - Parse the HTML content using `BeautifulSoup` with the `html.parser`.
- **Extract Table Data**:
  - Locate the target table using `BeautifulSoup`'s `find_all('table')`.
  - Extract table rows (`tr`) and cells (`td`) using `find_all()`.
  - Clean the extracted text by stripping whitespace with `.text.strip()`.
- **Full Implementation**:
  - The complete code for scraping the table is shown below (from the notebook):

```python
from bs4 import BeautifulSoup
import requests

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html.parser')

table = soup.find_all('table')[1]
table_rows = table.find_all('tr')

for row in table_rows[1:]:
    row_data = row.find_all('td')
    clean_table_rows = [data.text.strip() for data in row_data]
    print(clean_table_rows)
```

---

## Data Processing

The data processing step converts the scraped table into a Pandas DataFrame and exports it as a CSV file. Follow these steps to replicate:

- **Create Pandas DataFrame**:
  - Extract table headers using `find_all('th')` and clean them with `.text.strip()`.
  - Initialize a Pandas DataFrame with these headers.
  - Iterate through table rows, extract and clean cell data, and append each row to the DataFrame using `df.loc[]`.
- **Export to CSV**:
  - Save the DataFrame to a CSV file using `df.to_csv()`, excluding the index column with `index=False`.
- **Full Implementation**:
  - The complete code for processing and exporting the data is shown below (from the notebook):

```python
import pandas as pd
from bs4 import BeautifulSoup
import requests

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html.parser')

table = soup.find_all('table')[1]
world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]

df = pd.DataFrame(columns=world_table_titles)
table_rows = table.find_all('tr')

for row in table_rows[1:]:
    row_data = row.find_all('td')
    clean_table_rows = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = clean_table_rows

df.to_csv(r'web_scraped_table.csv', index=False)
```

- **Key Insights**:
  - The program automates the extraction of structured data from a webpage.
  - The resulting CSV file contains 100 rows (top 100 companies) with columns for rank, name, industry, revenue, revenue growth, employees, and headquarters.
  - The process can be adapted to scrape other tables by modifying the URL and table index.

---

## Usage

To explore or replicate the Web Scraping and Pandas Project, follow these steps:

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/charlespughtech/web_scraping_pandas_python_project.git
   cd web_scraping_pandas_python_project
   ```

2. **Install Dependencies**:

   ```bash
   pip install requests beautifulsoup4 pandas
   ```

3. **Explore the Project**:

   - Open `data_scraping_pandas_python_project.ipynb` in Jupyter Notebook or JupyterLab.
   - The notebook contains:
     - **Markdown Cells**: Explanations of the web scraping process, library imports, and data processing steps.
     - **Code Cells**: Webpage fetching, HTML parsing, table extraction, DataFrame creation, and CSV export.
   - Run the notebook cells sequentially to scrape the Wikipedia page, process the data, and generate `web_scraped_table.csv`.
   - Alternatively, view the static HTML export in `data_scraping_pandas_python_project.html` using a web browser to see the notebook content and sample outputs.

4. **Replicate the Project from Scratch** (Optional):

   - Create a new Jupyter Notebook named `data_scraping_pandas_python_project.ipynb`.
   - Add Markdown cells to document:
     - The purpose of the project (scraping and processing a table from Wikipedia).
     - The libraries used (`requests`, `BeautifulSoup`, `pandas`).
     - The steps for web scraping and data processing.
   - Add code cells to:
     - Import `requests`, `BeautifulSoup`, and `pandas`.
     - Fetch the Wikipedia page using `requests.get()`.
     - Parse the HTML with `BeautifulSoup`.
     - Extract the table headers and rows.
     - Create a Pandas DataFrame and populate it with the scraped data.
     - Export the DataFrame to `web_scraped_table.csv`.
   - Follow the steps in Data Scraping and Data Processing to implement the logic.
   - Test the notebook to verify the CSV file is generated with the correct data.
   - Export the notebook to HTML using Jupyter’s “File > Download as > HTML” to create `data_scraping_pandas_python_project.html`.

Results are available in `data_scraping_pandas_python_project.ipynb` (interactive) and `data_scraping_pandas_python_project.html` (static). Check the code cells for the implementation and Markdown cells for documentation.

---

## Contact

For inquiries or data analytics services, please contact:

**Charles Pugh**

Google-certified Data Analyst

Email: [charlespughtech@gmail.com](mailto:charlespughtech@gmail.com)

LinkedIn: [https://www.linkedin.com/in/charlespughtech/](https://www.linkedin.com/in/charlespughtech/)
