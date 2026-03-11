# Web Scraping Automation – eBay Tech Deals Data Pipeline

## Overview

This project implements an automated data pipeline that collects, processes, and analyzes technology deals from the eBay Global Tech Deals page.

The pipeline continuously gathers product data, stores it in a dataset, performs data cleaning, and conducts exploratory data analysis (EDA) to identify patterns in pricing, discounts, and shipping options.

---

## Methodology

### 1. Web Scraping

A Selenium-based scraper (`scraper.py`) was developed to extract product information from the eBay Global Tech Deals webpage.

The scraper collects the following attributes for each product:

* **timestamp** – date and time when the data was scraped
* **title** – product title
* **price** – current discounted price
* **original_price** – original listed price
* **shipping** – shipping information
* **item_url** – link to the product page

Since the webpage loads products dynamically, the scraper automatically scrolls through the page to trigger lazy loading and ensure all product listings are captured.

The collected data is appended to the dataset:

`ebay_tech_deals.csv`

---

### 2. Automation with GitHub Actions

The scraping process is automated using GitHub Actions.

The workflow runs every **3 hours** using the following cron schedule:

`0 */3 * * *`

Each execution of the workflow runs the scraper and appends new data to the dataset, allowing the repository to accumulate deal information over time.

---

### 3. Data Cleaning

The raw dataset is processed using the script `clean_data.py`.

The cleaning process includes:

* Removing the **"US $"** symbol and commas from price values
* Converting price fields into numeric format
* Handling missing **original_price** values by replacing them with the discounted price
* Standardizing missing shipping information
* Creating a new variable called **discount_percentage**

The cleaned dataset is saved as:

`cleaned_ebay_deals.csv`

---

### 4. Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed using the notebook:

`EDA.ipynb`

The analysis includes several visualizations and insights such as:

* Number of deals scraped per hour
* Distribution of product prices
* Comparison between original and discounted prices
* Distribution of discount percentages
* Frequency of different shipping options
* Keyword analysis in product titles
* Identification of the top 5 products with the highest discounts

The visualizations were created using **Matplotlib** and **Seaborn**.

---

## Key Findings

The exploratory analysis revealed several trends in the dataset:

* Most products fall within a specific price range, indicating a common pricing pattern for tech deals.
* Some products offer substantial discounts compared to their original prices.
* Popular brands such as **Apple** and **Samsung** frequently appear in the dataset.
* Free shipping is the most common shipping option for technology deals.

---

## Challenges Faced

Several challenges were encountered during the development of the pipeline:

* The webpage loads content dynamically, requiring automated scrolling to capture all product listings.
* Selenium occasionally loads pages differently than a regular browser session.
* Some product tiles were missing fields such as price or title, requiring additional error handling during scraping.

---

## Potential Improvements

Future improvements could include:

* Removing duplicate products collected across multiple scraping runs
* Extracting additional product attributes such as ratings or review counts
* Running the scraper for a longer period to analyze long-term pricing trends
* Using official APIs (if available) instead of web scraping for improved reliability

---

## Technologies Used

* Python
* Selenium
* Pandas
* Matplotlib
* Seaborn
* GitHub Actions
