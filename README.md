# Project Title: Exploration of Employment in the United States #

## Group 8 (Ab Ibrahim, Al Wagner, Del Vinas, Jay Howarth, Crystal White) ##

## Submission Date: January 11, 2023 ##


### Section 1: How We Approached the Project ###

During our first class, we discussed the project requirements and various public data sources, ultimately deciding on the Bureau of Labor Statistics. We chose this data source because we thought it would be interesting and useful to understand how jobs within artificial intelligence field have changed, particularly over the past 2 years. We spent quite a bit of time in the first 2 classes combing through the BLS data, which, although it’s both broad and extensive, what it is not is architected in a way that any single human being could easily find and make use of that data. 
                
### Section 2: How We Approached the Data Sourcing, Manipulation, & Analysis ###

**Overview**

As a group, we split up various duties which included project requirement review, documentation, presentation creation, review of BLS data tables, code research, experimentation, and testing. We also met outside of class and explored various data sources and questions we could answer with the data. And, that’s when we hit our first snag.

Our initial research question was to define what is happening within the field of artificial intelligence in terms of employment, but we quickly learned that the BLS does not separate “artificial intelligence” as its own occupation subcategory. Instead, the BLS categorizes those employed in computer science fields as under one of a number of NAICS codes, primarily 1, 2, 3, 4, 5. From (source White House report), we learned that “artificial intelligence” has only shown up as a self-reported occupation since 2000, so it has not yet grown to such a degree that BLS categorizes it separately, but that may well change in the near future (more on this later). 

Since our original hypothesis could not be supported with the BLS data, we pivoted to view the “computer science” occupation designation which would include people working in artificial intelligence, machine learning, and data science. While further exploring that segment of data, we decided that rather than just reporting on job growth within computer science, what we wanted to demonstrate for our class members was which industries in the United States have the greatest number of real jobs, such that when our class mates begin building their resumes and portfolios, they can consider tailoring their application to the highest-growth industries. 

And, even though we had our plan for how to source and analyze the BLS data such that it met the project requirements, we still wondered if we could provide more granularity around the number of artificial intelligence jobs in the U.S., even as additional information to supplement the BLS data exploration. To support this supplementary request, we explored a new product, Kadoa, and scheduled time with a co-founder to discuss how to pull in jobs data from Indeed, LinkedIn, and potentially connecting their product to BLS data. We also pulled additional reports provided by the White House, government agencies, and credible news sources. 

To be efficient as a group, we pulled down the tables of data to review which industries employed the largest number of computer scientists. Those industries were: Government, Health and Education, Financial Services, Retail, Professional and Business Services, and Manufacturing industries. With our plan of industries to target, we were prepared to start pulling in the data for analysis. 

**Getting into the Code**

We began setting up our code by defining the API and keys needed to call in the BLS data. Now, at this point we ran into our 2nd challenge: Figuring out how to build the Series IDs needed to call the data we needed because the only instructions the BLS gives on how to use their Series IDs is to state, “A catalogue of Series IDs is not yet available.” So, the four of us dug around on the internet, queried ChatGPT, Bard, and even reached out to BLS statisticians on LinkedIn to try to figure out how to build the Series IDs. 

Fortunately, after 40 minutes and much frustration, Al figured out that the Series IDs are created by cobbling together multiple types of information as follows: Field Names, Prefix, Seasonal Adjustment Codes, Industry Codes, and Data Type Codes. Each of the fields must be input in a certain position to build the correct Series ID. So, finally having solved that piece of the puzzle (with no help from BLS documentation), we were ready to actually start coding.

We defined our time series as beginning in 2015 and ending in 2024. We wanted to illustrate the data leading up to present but also to predict what could be a change in employment across industries in a near future, preferring to stay closer to present to have a more accurate forecast. 

Now, with all that backstory provided, we’re ready to get into the code documentation. However, if you would like to skip endless pages of repetitive commentary on how we performed similar actions across the government, health and education, retail, professional and business services, and manufacturing industries, then feel free to skip to “Section 3. What We Learned.” If not, grab a coffee and a bottle of Tylenol, and let’s get to it. 

---

### Importing Libraries & Using BLS API ###

The provided Python code is meant to interact with the Bureau of Labor Statistics (BLS) public API to retrieve data for a specific time series related to employment. It imports necessary libraries, sets API parameters, sends a POST request to the BLS API, processes the response, and presents the data in a Pandas DataFrame.

**Code Walkthrough**

*Importing Libraries*

import requests
import json
import pandas as pd

The code begins by importing three essential libraries: requests, json, and pandas. These libraries are required for making HTTP requests, working with JSON data, and handling data in tabular form, respectively.

*Defining API Parameters*

api_url = “https://api.bls.gov/publicAPI/v2/timeseries/data/”
api_key = “Your API Key here”  # Replace with your API key
series_id = “CEU3000000001”
start_year = “2015”
end_year = “2024”

Here, we define various parameters needed for the BLS API request:

api_url: The API endpoint for BLS data retrieval.
Api_key: Your unique API key (You should replace “Your API Key here” with your actual API key).
Series_id: The unique identifier for the specific time series data (employment data in this case).
Start_year: The starting year for the data query.
End_year: The ending year for the data query.

*Formatting the Request Body*

data = json.dumps({
    "seriesid": [series_id],
    "startyear": start_year,
    "endyear": end_year,
    "registrationkey": api_key
})

In this section, the code creates a JSON-formatted request body. It includes the seriesid, startyear, endyear, and registration key as required by the BLS API. The values are taken from the previously defined variables.

*Sending the POST Request*

response = requests.post(api_url, data=data, headers={"Content-type": "application/json"})
response_data = response.json()

This code segment sends a POST request to the BLS API using the requests.post method. The request body (data) and headers are set accordingly. The API response is then converted from JSON format to a Python dictionary and stored in the response_data variable.

*Checking Request Status*

if response_data["status"] == "REQUEST_SUCCEEDED":
    print("Request succeeded")
else:
    print("Request failed")

Here, the code checks the status of the API request. If the request is successful (status is "REQUEST_SUCCEEDED"), it prints "Request succeeded." Otherwise, it prints "Request failed."

*Extracting and Formatting Data*

series_data = response_data["Results"]["series"][0]["data"]

df = pd.DataFrame(series_data)
df = df.rename(columns={"year": "Year", "period": "Month", "value": "Value", "footnotes": "Footnotes"})
df = df.reset_index(drop=True)

This section of the code extracts the actual data from the API response, which is nested within the JSON structure. It then converts the data into a Pandas DataFrame for easy manipulation. Column names are also renamed for clarity, and the index is reset.
    
*Importing the os Library*

import os

The code begins by importing the os library. This library is essential for interacting with the operating system, including functions related to file and directory operations.

*Printing the Current Working Directory*

print(os.getcwd())

This line of code utilizes the os.getcwd() function to retrieve and print the current working directory (CWD). The CWD is the directory in which the Python script is executed.

*Saving Data to a CSV File*

df.to_csv('data.csv', index=False)

In this section, the code uses the Pandas DataFrame df to save its contents to a CSV (Comma-Separated Values) file named "data.csv." The to_csv method is called on the DataFrame, and two parameters are specified:

'data.csv': The name of the CSV file where the data will be saved.
index=False: This parameter instructs Pandas not to include the index column in the CSV file.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method to display the first few rows of the DataFrame df. This is a convenient way to quickly inspect the data to ensure it has been loaded and processed correctly.

### Government Industry ###

*Reading an Excel File*

df = pd.read_excel('government.xlsx')

In this section, the code uses the pd.read_excel() function to read the contents of an Excel file named "government.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*

The Python code snippet below performs several tasks related to time series forecasting using the Prophet library:

-	Imports the required libraries, including Prophet, and matplotlib for plotting.
-	Renames columns in the DataFrame to match Prophet's expected format.
-	Prepares the data for modeling.
-	Creates a Prophet model and adds seasonality.
-	Fits the model to the data.
-	Generates a future dataframe for forecasting.
-	Makes a forecast using the trained model.
-	Visualizes the forecast and its components using matplotlib.

*Importing Libraries*

import prophet
from prophet.plot import plot_components
import matplotlib.pyplot as plt

The code starts by importing the necessary libraries, including Prophet for time series forecasting, and matplotlib for visualization.

*Renaming Columns*

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section renames the columns in the Pandas DataFrame df to match the expected input format of Prophet. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values.

*Creating a Prophet Model*

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. We chose 0.9 because we were more comfortable with that level of certain (as opposed to a higher value). Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This captures monthly seasonality in the data.

*Fitting the Model*

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data.

*Generating a Future Dataframe*

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data.

*Making a Forecast*

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

fig1 = m.plot(forecast)
plt.show()

fig2 = plot_components(m, forecast)
plt.show()

Two plots are generated to visualize the forecast and its components. fig1 displays the overall forecast, including the observed data, predicted values, and uncertainty intervals. fig2 shows the individual components of the forecast, such as trend and seasonality. Both plots are displayed using matplotlib's plt.show() function.

### Health and Education Industries ###

*Reading Data from Excel*

df = pd.read_excel('health_education.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "health_education.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Renaming Columns*

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

forecast = m.predict(future)
The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

fig2 = plot_components(m, forecast)
plt.show()


Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Financial Activities Industry ###
*Reading Data from Excel*

df = pd.read_excel('financial_activities.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "financial_activities.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*
The Python code provided below follows a similar structure to the previous sections. It focuses on creating a time series forecast using the Prophet library. Specifically, it reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components.

*Code Walkthrough*

*Renaming Columns*

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Professional and Business Services Industries ###

*Code Overview*
The Python code provided below continues the process of reading data from an Excel file named "professional_business_services.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet follows a similar structure to the previous sections, focusing on data loading and initial inspection.

*Code Walkthrough*

*Reading Data from Excel*

df = pd.read_excel('professional_business_services.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "professional_business_services.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*
The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

*Code Walkthrough*

*Renaming Columns*

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

forecast = m.predict(future)
The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

fig1 = m.plot(forecast)
plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Manufacturing ###

*Code Overview*

The provided Python code continues the process of reading data from an Excel file named "manufacturing.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet is consistent with the previous sections, focusing on data loading and initial inspection.

*Code Walkthrough*

*Reading Data from Excel*

df = pd.read_excel('manufacturing.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "manufacturing.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

*Code Walkthrough*

*Renaming Columns*

df = df.rename(columns={'Date': 'ds'})
df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

m = prophet.Prophet(interval_width=0.9)
m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

fig1 = m.plot(forecast)
plt.show()


In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

fig2 = plot_components(m, forecast)
plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

---

### Section 3: What We Learned ###

**Key Learnings from the Data**

-	**Government** Full-time employment in the government industry was trending slightly upwards until 2020 when COVID hit, dropping to its lowest number of full-time employees since before 2015, and has not yet returned to pre-COVID levels.


-	**Health and Education** Similar to the government, overall employment was trending upwards until 2020; however, job loss was not as significant as it was in the government industry, and it recovered much faster, reaching pre-pandemic levels by early 2023.


-	**Financial Activities** Within the industry of finance, we see significantly fewer jobs overall than in Government and Health and Education sectors; however, the employment trends are similar to these other industries in that employment was trending upwards, dipped in 2020 (with a loss of less than 500 – in tens of thousands) jobs, before reaching and exceeding pre-pandemic levels in 2021.

-	**Retail Trade** Overall, the retail industry employs fewer full-time workers than either the Government or Healthcare and Education industries but more than are employed within the Financial industry. Unlike the previously discussed industries, Retail employment was declining previous to 2020 and may not yet reach 2019 employment levels until this year.

-	**Professional and Business Services** With Professional and Business Services, we see similar overall employment numbers to Government and Health and Education, but we also see a similar swift post-pandemic recovery period similar to the Financial industry, reaching pre-pandemic employment levels mid-2021.

-	**Manufacturing** At a peak of 13,000 (in tens of thousands) full-time employees in 2019, manufacturing employs the 2nd lowest number of FTEs from the industries we’ve reviewed, but unlike Financial Services, Manufacturing didn’t reach pre-pandemic employment levels until 2023 and is expected to increase by less than 1,000 (in tens of thousands) jobs by 2027. 

*Government Key Learning*

Full-time employment in the government industry was trending slightly upwards until 2020 when COVID hit, dropping to its lowest number of full-time employees since before 2015, and has not yet returned to pre-COVID levels. Looking more closely at the data, we can see a trend in the government industry where there is a seasonal dip every year mid-way through the calendar year. A second, lesser dip can be observed occurring at the beginning of every calendar year. This makes sense when considering that federal and state governments operate on an annual budget which typically begins in July of each year, is re-evaluated at the mid-point at each fiscal year, then wraps up at the end of each June. Specifically, we observe that starting in July, there is an acceleration of hiring of computer science professionals which drops off slightly at the end of the calendar year before picking back up in the months of February to April before taking a dip in May then a steeper decline every June. 

Using Prophet, we forecast full-time employment within the government throughout the 2026 calendar year. What we see from the data is that there is an expected steady increase in employment, year over year, adding more than 1,000 (in tens of thousands) of full-time employees by the end of 2026.

When we looked at the values on an annual basis, using Prophet, we noticed that there was a steep decline at the end of February which caused us to look more closely at the raw data. What we learned were the trends previously mentioned, *but* what Prophet was reflecting in the visualization was the significance of COVID as an outlier. It was such a strong decline that Prophet was representing it as a seasonal factor when it is not. 

*Health and Education Key Learning*

Similar to the government, employment was trending upwards until 2020; however, job loss was not as significant as it was in the government industry, and it recovered much faster, reaching pre-pandemic levels by early 2023. Pre-pandemic, overall employment within the Health and Education industries was higher than that of the government industry (by almost 2,000 more jobs – in tens of thousands). 

Using Prophet to forecast job growth within the health and education industries, what we see is that almost 4,000 more jobs jobs ( in tens of thousands) will be created within these industries for the time period from 2024-2027. This trend is further reflected by a table provided by the BLS (Source citation). What is worthy of note from the BLS data provided in (SOURCE NAME) is that only “Health Care Services” is expected to have the same high percentage of growth in jobs as “Computer Science and Mathematics” at roughly 15% annual growth, but “Computer Science and Mathematics” jobs have an annual median income of $100k whereas “Health Care Services” has an annual median income of $33k. But, let’s get back to the Prophet data visualizations.

Similar to the Government industry visualizations, when we look at Health and Education on an annual basis, we see the steep decline just before March which we attribute to COVID’s affect on the statistical model.


*Financial Activities Key Learning*

Within the industry of finance, we see significantly fewer jobs overall than in Government and Health and Education sectors; however, the employment trends are similar to these other industries in that employment was trending upwards, dipped in 2020 (with a loss of less than 500 – in tens of thousands) jobs, before reaching and exceeding pre-pandemic levels in 2021.

Although employing far fewer full-time employees than either Healthcare and Education or Government industries, the financial services industry recovered more quickly and has been growing at a steady rate since its recovery in 2021. Projecting from 2024 to 2027, our model shows that employment in the Financial Services industry is expected to increase by 500 (tens of thousands) jobs, as a conservative estimate. 

Similar to the previous 2 industries, the affect of COVID on Prophet’s statistical model can also be observed within the financial services industry data. 

*Retail Trade Key Learning*

Overall, the retail industry employs fewer full-time workers than either the Government or Healthcare and Education industries but more than are employed within the Financial industry. Unlike the previously discussed industries, Retail employment was declining previous to 2020 and may not yet reach 2019 employment levels until this year.

The volatility of the Retail industry can be observed through our visualizations with seasonal heights being reached at the end of each year (which is expected due to holiday shopping); however, when the data is viewed outside of the end-of-year trends, employment within the retail industry seems to be largely flat since 2015 with little gains to be expected even with projections up until 2027. 

From our review of industries employing the greatest number of computer scientists, we know that Retail was one of largest employers, but what we can see from the data is that Retail is a seasonal and volatile industry which may not provide job stability even for computer scientists. 

Similar to the other industries, the significant dip observed just before March occurs within the Retail visualization when viewing the model on a yearly basis. 

*Professional and Business Services Key Learning*

With Professional and Business Services, we see similar overall employment numbers to Government and Health and Education, but we also see a similar swift post-pandemic recovery period similar to the Financial industry, reaching pre-pandemic employment levels mid-2021. Previous to 2020, we saw employment within the Professional and Business Services industry at almost 22,000 (in tens of thousands) employed. By 2022, those levels were exceeded and are projected to reach almost 23,000 (in tens of thousands)  by 2024. 

In terms of seasonality, what we see is a dip in employment at the end of each calendar year which makes sense considering this industry is comprised of a lot of B2B consultants where engagements may conclude at the end of their clients’ fiscal years. However, employment has steadily increased since 2021 and is expected to continue well into 2027. 


*Manufacturing Key Learning*

At a peak of 13,000 (in tens of thousands) full-time employees in 2019, manufacturing employs the 2nd lowest number of FTEs from the industries we’ve reviewed, but unlike Financial Services, Manufacturing didn’t reach pre-pandemic employment levels until 2023 and is expected to increase by less than 1,000 (in tens of thousands) jobs by 2027.

Unlike the other industries, there doesn’t seem to be any specific seasonality we can point to in terms of employment. What we can observe from the visualizations is that employment has largely been flat since 2015, experiencing neither significant highs or lows, until the pandemic which took employment to the lowest levels of the period examined (2015-2027). Considering the safety requirements, new regulations, and extended time period before manufacturing employees could reliably return to work, this is to be expected. 

*Conclusion*

Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

Transition statement

**Key Learnings about Working with BLS Data**

-	Accessing government data
-	Using government data
-	Understanding government data
-	Getting help working with government data
-	Limitations of government data
-	Sourcing information to supplement government data

* Accessing, using and understanding government data*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum


*Getting help working with government data*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum


*Sourcing information to supplement government data*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

Transition statement

**Key Learnings about Working as a Project Team**

-	Establishing areas of ability & setting ourselves up for success
-	Pivoting and rethinking assumptions
-	Getting outside help
-	Comparison to real-world scenarios
-	Using project to set ourselves and one another up for career success
                

*Establishing areas of ability & setting ourselves up for success*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

*Pivoting and rethinking assumptions*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

*Getting outside help*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

*Using project to set ourselves and one another up for career success*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

Transition statement

---
  
### Section 4: Results & Conclusions ###

**Recap & Conclusion**
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus

*Recap*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

*Conclusion*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum

---
                
### Section 5: Remaining Questions for Future Exploration ###

**Research areas for future exploration**
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

*Time-series seasonality*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

*Extracting COVID-related data from time-series*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

*Jobs by geography*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

*Prophet team discussion*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

*Kadoa data scraping exploration*
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. 

---
### Section 6: Appendix & Citations ###

Sources: (Note: APA Style – refer back to assignment 1)

White House report
National Security Council
CNBC
LinkedIn
Indeed
BLS table citation
BLS reports
McKinsey reports
Other



 
![image](https://github.com/iabdullah42/Project_1/assets/148771204/e18ed13e-6419-4aa9-a618-52c399302dec)
