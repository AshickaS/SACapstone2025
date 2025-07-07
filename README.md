# Real-time Dynamic Parking Price Modeling with Pathway

## Project Overview

This project demonstrates a real-time data streaming pipeline using **Pathway** to implement a dynamic pricing model for parking spaces. It processes simulated real-time data from a historical dataset, performs on-the-fly feature engineering, calculates dynamic prices within tumbling windows, and visualizes the results using **Bokeh**.

The current implementation focuses on demonstrating a baseline dynamic pricing model.

## Key Features

* **Real-time Data Ingestion:** Simulates live data streams by replaying a historical parking dataset from a Google Sheet CSV.
* **On-the-Fly Feature Engineering:** Extracts time components, converts categorical traffic conditions and vehicle types into numerical features, and calculates occupancy rates dynamically.
* **Windowed Aggregations:** Processes data within daily tumbling windows to aggregate key metrics (maximum/minimum occupancy, capacity) per parking space.
* **Dynamic Price Calculation:** Implements a baseline pricing model where price is adjusted based on the aggregated occupancy behavior within each daily window.
* **Real-time Visualization:** Utilizes Bokeh to display the calculated dynamic price changes over time, updating as new data flows through the pipeline.

## Pricing Model Implemented (Current)

The dynamic pricing logic currently implemented is derived from a sample notebook, calculating price as:

$Price = 10 + \\frac{(Max\\_Occupancy - Min\\_Occupancy)}{Capacity}$

This model provides a basic dynamic adjustment based on the range of occupancy observed within a daily window relative to the parking space's capacity.

*(Note: Future iterations or extensions, as per project requirements, might include a Demand-Based Price Function (Model 2) incorporating Queue Length, Traffic, Special Day status, and Vehicle Type Weight, and a Proximity-Based Price Function (Model 3) using geospatial data.)*

## Data Source

The project uses historical parking data accessed directly from a Google Sheet via a public URL. This data is preprocessed using Pandas and then saved to a local CSV file (`parking_stream_full.csv`), which Pathway then replays to simulate a real-time stream.

## How to Run

1.  **Environment Setup:**
    * Open the provided Python notebook (e.g., in Google Colab).
    * The notebook includes `!pip install pathway bokeh --quiet` to install necessary libraries.

2.  **Data Preparation:**
    * The notebook directly reads the parking data from a Google Sheet URL.
    * It then preprocesses this data using Pandas and saves it as `parking_stream_full.csv` in the local environment.

3.  **Execute the Notebook:**
    * **Ensure `parking_stream_full.csv` is generated and accessible.**
   
    * Run all cells in the notebook sequentially.

4.  **Observe Outputs:**
    * A Bokeh plot will appear, dynamically updating as Pathway processes the simulated real-time data, showing the calculated dynamic price over time.

## Dependencies

* `pathway`
* `bokeh`
* `pandas`
* `datetime`
* `panel`

## Files

* `dynamic_parking_pricing_notebook.ipynb`: The main notebook file containing all the code
* `parking_stream_full.csv`: A temporary CSV file generated during runtime from the Google Sheet data, used by Pathway for stream replay.
