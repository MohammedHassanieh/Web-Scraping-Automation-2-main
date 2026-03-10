# Web-Scraping-Automation-2

## eBay Tech Deals Data Pipeline

## Overview

This project implements a complete data pipeline that scrapes, processes, and analyzes technology deals from the eBay Global Tech Deals page.

The pipeline automatically collects product data over time, cleans the dataset, and performs exploratory data analysis (EDA) to identify trends in pricing, discounts, and shipping options.

## Methodology

### 1. Web Scraping

A Selenium-based scraper (`scraper.py`) was developed to collect product information from the eBay Global Tech Deals page.

The scraper extracts the following fields:

- timestamp
- title
- price
- original_price
- shipping
- item_url

The scraper scrolls through the page to trigger lazy loading and ensures all product tiles are captured.

The collected data is appended to: [ebay_tech_deals.csv](./ebay_tech_deals.csv)

### 2. Automation with GitHub Actions

The scraper is automated using GitHub Actions to run every **3 hours**.

Cron schedule used: 0 \* 3 \* \* \*

Each run collects new deal data and appends it to the dataset, allowing the repository to build a time-based dataset over approximately two days.

### 3. Data Cleaning

The script `clean_data.py` processes the raw scraped data by:

- Removing `US $` and commas from price fields
- Converting price values to numeric format
- Handling missing `original_price` values
- Cleaning missing shipping information
- Creating a new feature: discount_percentage

The cleaned dataset is saved as: [cleaned_ebay_deals.csv](./cleaned_ebay_deals.csv)

### 4. Exploratory Data Analysis

EDA was performed in the notebook: [EDA.ipynb](./EDA.ipynb)

The analysis includes:

- Time series analysis of deals scraped per hour
- Distribution of product prices
- Comparison of original vs discounted prices
- Discount percentage distribution
- Shipping option frequency
- Keyword analysis in product titles
- Price difference analysis
- Identification of the top 5 highest discounts

Visualizations were created using **Matplotlib and Seaborn**.

## Key Findings

Some common observations include:

- Most deals cluster within a specific price range.
- Several products show significant discounts compared to their original prices.
- Certain brands and keywords (such as Apple and Samsung) appear frequently in the dataset.
- Free shipping is the most common shipping option among deals.

## Challenges Faced

Several technical challenges were encountered:

- Dynamic page loading required scrolling to load all product listings.
- Selenium occasionally loaded a different page structure compared to a normal browser session.
- Some product tiles did not initially contain all fields (title or price), requiring additional validation logic.

## Potential Improvements

Future improvements could include:

- Deduplicating products across scraping runs
- Collecting additional product attributes such as ratings or number of reviews
- Running the scraper for a longer time period to analyze price trends
- Using API-based scraping if available to increase reliability

## Technologies Used

- Python
- Selenium
- Pandas
- Matplotlib
- Seaborn
- GitHub Actions
