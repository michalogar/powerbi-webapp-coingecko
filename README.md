# End-to-End Web Application Development in Power BI Using CoinGecko API

## Project Overview
This project demonstrates the end-to-end process of building a web application in Power BI using data from the CoinGecko API. The goal is to provide a dynamic and interactive cryptocurrency dashboard that replicates some of the functionality seen on the CoinGecko website.

### Key Features:

- **Data Extraction & Transformation**: Connects to the free CoinGecko API to pull real cryptocurrency data, including price, market cap, volume, and other key metrics. Using Power Query in Power BI, we clean, transform, and structure the data for analysis. This project also deals with **looping through API calls using recursive functions** and **handling rate limits** imposed by the API provider to ensure reliable data extraction.
- **Visualizations**: The dashboard uses **only native Power BI visuals**, leveraging Power BI’s built-in capabilities to create intuitive, user-friendly charts and tables for real-time insights into cryptocurrency data.

This project serves as a practical example of how to build a data-driven web application entirely within Power BI, integrating real data while maintaining efficient data handling techniques.

## Setup and Installation
To get started with this project, you'll need to follow these simple steps to set up Power BI Desktop and connect to the CoinGecko API.

### Prerequisites:
1. **Power BI Desktop**: Make sure you have **Power BI Desktop** installed. You can download it for free from [here](https://www.microsoft.com/en-us/download/details.aspx?id=58494).
2. **CoinGecko API Access**: You will need to create a free account on CoinGecko and get an API key for accessing the data.
- Go to the [CoinGecko](https://www.coingecko.com/) and sign up.
- Go to [Developers Dashboard](https://www.coingecko.com/en/developers/dashboard) to generate API Key.
- Follow the instructions to generate your API key.
- You will use this key to authenticate your requests to the CoinGecko API.

## Steps to Set Up:
1. Clone the Repository or Download the .pbix File:
- You can either clone this repository to your local machine using the following command:
```git clone https://github.com/michalogar/powerbi-webapp-coingecko.git```
- Or you can directly download the `.pbix` file from the repository if you prefer.
