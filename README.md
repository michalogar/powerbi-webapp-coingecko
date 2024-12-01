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
  ```
  git clone https://github.com/michalogar/powerbi-webapp-coingecko.git
  ```
  - Or you can directly download the `.pbix` file from the repository if you prefer.
2. Open the Power BI Project:
  - Open Power BI Desktop.
  - From the main screen, go to **File** > **Open** and select the `.pbix` file from the cloned repository or downloaded folder.
3. Configure API Key:
  - In the Power BI file, open **Power Query** by clicking on **Transform Data**.
  - In the Power Query Editor, you will find a parameter named `api-key`. Replace the placeholder text with your API key to authenticate your requests to the CoinGecko API.
4. Set the Number of Coins to Fetch:
  - In the Power Query Editor, you'll also find a parameter to specify the **number of coins** you'd like to fetch. Adjust this value based on how many cryptocurrencies you want the dashboard to display.
5. Refresh the Data:
  - After configuring the parameters, go back to the main Power BI Desktop interface.
  - Click on **Refresh** to pull the latest cryptocurrency data from the CoinGecko API.
6. Start Using the Dashboard:
  - Once the data is refreshed, you can start exploring the interactive cryptocurrency dashboard.

## Usage Instructions
The Power BI report mimics the main CoinGecko website, providing a user-friendly interface to explore cryptocurrency data. Below are the key instructions on how to navigate and interact with the report.

### 1. Main Dashboard Overview
- The main page of the report provides a comprehensive view of the cryptocurrency market:
  - **Global Market Overview**: At the top of the page, you'll find a summary of the global cryptocurrency market, including metrics like total market capitalization, 24-hour trading volume, and the number of active coins.
  - **Cryptocurrency Table**: Below the global overview, a detailed table lists cryptocurrencies along with their:
    - Logo, name, and symbol
    - Current price
    - Percentage changes (e.g., 24-hour, 7-day)
    - Other key metrics like market cap and trading volume
  - **Customise Button**:
    - Adjust the visibility of specific columns.
    - Adjust the visibility of specific columns.
![image](https://github.com/user-attachments/assets/6f2b483f-d292-4643-81db-20dcbec50bbf)

## 2. Drill-Through to Coin Details
- You can right-click on a cryptocurrency in the main table and use the **Drill-Through** feature to access a detailed report for that coin.
- The detailed page includes:
  - **Historical Chart**: Visualizes the selected coin’s price, market cap, and volume over time (free API provide 1 year of historical price data).
  - Additional insights and metrics specific to the selected cryptocurrency.
 ![image](https://github.com/user-attachments/assets/e521dfa5-ccab-4fa4-96a1-cee112d5b2a7)

  
