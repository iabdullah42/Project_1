#This is the start of the README#

##Just documenting for now##

###Note### Add in list of files included in Folder and descriptions of each


README - Code Documentation
This README document provides a step-by-step explanation of the code provided. It is intended for business analysts and developers to understand and discuss the code functionality.

Code Overview
The provided Python code is meant to interact with the Bureau of Labor Statistics (BLS) public API to retrieve data for a specific time series related to employment. It imports necessary libraries, sets API parameters, sends a POST request to the BLS API, processes the response, and presents the data in a Pandas DataFrame.

Code Walkthrough
Importing Libraries

import requests
import json
import pandas as pd

The code begins by importing three essential libraries: requests, json, and pandas. These libraries are required for making HTTP requests, working with JSON data, and handling data in tabular form, respectively.

Defining API Parameters
api_url = "https://api.bls.gov/publicAPI/v2/timeseries/data/"
api_key = "Your API Key here"  # Replace with your API key
series_id = "CEU3000000001"
start_year = "2015"
end_year = "2024"

Here, we define various parameters needed for the BLS API request:

api_url: The API endpoint for BLS data retrieval.
api_key: Your unique API key (You should replace "Your API Key here" with your actual API key).
series_id: The unique identifier for the specific time series data (employment data in this case).
start_year: The starting year for the data query.
end_year: The ending year for the data query.

Formatting the Request Body

data = json.dumps({
    "seriesid": [series_id],
    "startyear": start_year,
    "endyear": end_year,
    "registrationkey": api_key
})

In this section, the code creates a JSON-formatted request body. It includes the seriesid, startyear, endyear, and registration key as required by the BLS API. The values are taken from the previously defined variables.

Sending the POST Request

response = requests.post(api_url, data=data, headers={"Content-type": "application/json"})
response_data = response.json()

This code segment sends a POST request to the BLS API using the requests.post method. The request body (data) and headers are set accordingly. The API response is then converted from JSON format to a Python dictionary and stored in the response_data variable.

Checking Request Status

if response_data["status"] == "REQUEST_SUCCEEDED":
    print("Request succeeded")
else:
    print("Request failed")

Here, the code checks the status of the API request. If the request is successful (status is "REQUEST_SUCCEEDED"), it prints "Request succeeded." Otherwise, it prints "Request failed."

Extracting and Formatting Data

series_data = response_data["Results"]["series"][0]["data"]
df = pd.DataFrame(series_data)
df = df.rename(columns={"year": "Year", "period": "Month", "value": "Value", "footnotes": "Footnotes"})
df = df.reset_index(drop=True)

This section of the code extracts the actual data from the API response, which is nested within the JSON structure. It then converts the data into a Pandas DataFrame for easy manipulation. Column names are also renamed for clarity, and the index is reset.

Printing the Data Frame

print(df)

Finally, the code prints the resulting Pandas DataFrame, displaying the employment data in a tabular format.

Code Walkthrough
Importing the os Library

import os

The code begins by importing the os library. This library is essential for interacting with the operating system, including functions related to file and directory operations.

Printing the Current Working Directory

print(os.getcwd())

This line of code utilizes the os.getcwd() function to retrieve and print the current working directory (CWD). The CWD is the directory in which the Python script is executed.

Saving Data to a CSV File

df.to_csv('data.csv', index=False)

In this section, the code uses the Pandas DataFrame df to save its contents to a CSV (Comma-Separated Values) file named "data.csv." The to_csv method is called on the DataFrame, and two parameters are specified:

'data.csv': The name of the CSV file where the data will be saved.
index=False: This parameter instructs Pandas not to include the index column in the CSV file.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method to display the first few rows of the DataFrame df. This is a convenient way to quickly inspect the data to ensure it has been loaded and processed correctly.

Reading an Excel File

df = pd.read_excel('government.xlsx')

In this section, the code uses the pd.read_excel() function to read the contents of an Excel file named "government.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

Code Overview

The Python code snippet below performs several tasks related to time series forecasting using the Prophet library:

Imports the required libraries, including Prophet, and matplotlib for plotting.
Renames columns in the DataFrame to match Prophet's expected format.
Prepares the data for modeling.
Creates a Prophet model and adds seasonality.
Fits the model to the data.
Generates a future dataframe for forecasting.
Makes a forecast using the trained model.
Visualizes the forecast and its components using matplotlib.

Code Walkthrough
Importing Libraries

import prophet
from prophet.plot import plot_components
import matplotlib.pyplot as plt

The code starts by importing the necessary libraries, including Prophet for time series forecasting, and matplotlib for visualization.

Renaming Columns

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section renames the columns in the Pandas DataFrame df to match the expected input format of Prophet. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values.

Creating a Prophet Model

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This captures monthly seasonality in the data.

Fitting the Model

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data.

Generating a Future Dataframe

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data.

Making a Forecast

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

Visualizing the Forecast

fig1 = m.plot(forecast)
plt.show()

fig2 = plot_components(m, forecast)
plt.show()

Two plots are generated to visualize the forecast and its components. fig1 displays the overall forecast, including the observed data, predicted values, and uncertainty intervals. fig2 shows the individual components of the forecast, such as trend and seasonality. Both plots are displayed using matplotlib's plt.show() function.

Code Walkthrough
Reading Data from Excel

df = pd.read_excel('health_education.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "health_education.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

Code Walkthrough
Renaming Columns

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']


This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

Creating a Prophet Model

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

Fitting the Model

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

Generating a Future Dataframe

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

Making a Forecast

forecast = m.predict(future)
The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

Visualizing the Forecast

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

Visualizing the Components of the Forecast

fig2 = plot_components(m, forecast)
plt.show()


Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

Code Overview
The Python code provided below continues the process of reading data from an Excel file named "financial_activities.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet follows a similar structure to the previous sections, focusing on data loading and initial inspection.

Code Walkthrough
Reading Data from Excel

df = pd.read_excel('financial_activities.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "financial_activities.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

Code Overview
The Python code provided below follows a similar structure to the previous sections. It focuses on creating a time series forecast using the Prophet library. Specifically, it reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components.

Code Walkthrough
Renaming Columns

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

Creating a Prophet Model

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

Fitting the Model

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

Generating a Future Dataframe

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

Making a Forecast

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

Visualizing the Forecast

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

Visualizing the Components of the Forecast

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

Code Overview
The Python code provided below continues the process of reading data from an Excel file named "professional_business_services.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet follows a similar structure to the previous sections, focusing on data loading and initial inspection.

Code Walkthrough
Reading Data from Excel

df = pd.read_excel('professional_business_services.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "professional_business_services.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

Code Overview
The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

Code Walkthrough
Renaming Columns

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

Creating a Prophet Model

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

Fitting the Model

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

Generating a Future Dataframe

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

Making a Forecast

forecast = m.predict(future)
The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

Visualizing the Forecast

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

Visualizing the Components of the Forecast

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.


Code Overview
The provided Python code continues the process of reading data from an Excel file named "manufacturing.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet is consistent with the previous sections, focusing on data loading and initial inspection.

Code Walkthrough
Reading Data from Excel
df = pd.read_excel('manufacturing.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "manufacturing.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

Displaying the First Rows of the DataFrame

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

Code Overview
The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

Code Walkthrough
Renaming Columns

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

Creating a Prophet Model

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

Fitting the Model

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

Generating a Future Dataframe

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

Making a Forecast

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

Visualizing the Forecast

fig1 = m.plot(forecast)
plt.show()


In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

Visualizing the Components of the Forecast

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.





