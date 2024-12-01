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

## API Rate Limiting & Recursive Functions in Power Query
One of the core aspects of this project is fetching cryptocurrency data from the CoinGecko API while adhering to its rate limits and handling large datasets. Below is an explanation of how these challenges were addressed using Power Query.
1. Understanding the API Rate Limits
   - The CoinGecko API enforces a rate limit, restricting the number of requests you can make within a specified time (e.g., 30 requests per minute).
   - Exceeding these limits results in failed requests and errors, which can disrupt data loading in Power BI.
2. Recursive Functions for API Pagination
   - CoinGecko’s API returns data in pages, with each page containing a limited number of records (or just for one coin). To fetch data for more coins, it is necessary to make multiple API calls.
   - In Power Query, I implemented recursive functions to loop through pages of API results, combining them into a single dataset.
   - Here’s how the recursive logic works:
     1. Start by fetching the first page of results from the endpoint:
        `https://api.coingecko.com/api/v3/coins/markets`
        This endpoint returns, by default, a list of 100 coins with their IDs and some market data.
     2. Extend the request to fetch up to 250 coins per page, optimizing data retrieval (1 page = 1 request).
     3. Dynamically determine the number of pages to request:
        - The number of pages is calculated based on the `No of Coins` parameter set by the user.
      4. Use a recursive function to loop through the pages:
         - The function makes repeated API calls for each page until all requested coins are fetched.
      5. Extract all coin IDs from the retrieved data:
         - These IDs are essential for fetching additional details, such as historical market data.
      6. Create custom functions for specific endpoints:
         - For example, to fetch historical market data, a function is created for the endpoint:
           `https://api.coingecko.com/api/v3/coins/{coin_id}/market_chart`
         - This function loops through all retrieved `coin_id`s to fetch detailed data for each coin.
      7. Example M Code for Recursive Function:
         ```
         let
    // Function to retrieve paginated data from the API
    getData = (offset as number) =>
    let
        // Define the API URL with dynamic page offset
        url = "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&per_page=250&sparkline=true&page=" & Number.ToText(offset),
        
        // Define headers, including API key for authorization
        headers = [
            Accept = "application/json",
            #"x-cg-demo-api-key" = #"api-key"
        ],
        
        // Make the API request with the defined headers
        response = Web.Contents(url, [Headers=headers]),
        
        // Convert the binary response to text format
        responseText = Text.FromBinary(response),
        
        // Parse the JSON response into a Power Query structure (table or record)
        result = Json.Document(responseText)
    in
        result,

    // Calculate the number of pages needed by dividing the total number of coins by 250 (items per page) and rounding up
    pageNo = Number.RoundUp(#"No of Coins"/250, 0),

    // Set the number of coins to filter
    toFilter = #"No of Coins",

    // Generate a list of offsets for pagination; adjust the second argument as needed for more pages
    offsetRange = List.Numbers(1, pageNo),
    
    // Transform each offset into a separate API call, creating a list of results
    Source = List.Transform(offsetRange, each getData(_)),

    // Convert the list of lists into a single table
    convertToTable = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    
    // Expand the data from each page into individual rows in the table
    #"Expanded Column1" = Table.ExpandListColumn(convertToTable, "Column1"),
    #"Kept First Rows" = Table.FirstN(#"Expanded Column1",toFilter)
in
    #"Kept First Rows"
         ```







  
