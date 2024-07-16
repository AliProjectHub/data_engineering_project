# Weather Data Pipeline using Apache Airflow

## Overview

This project sets up an Apache Airflow DAG to extract weather data from an API, transform the data, and load it into an AWS S3 bucket. The weather data is for the city of Portland and includes various metrics such as temperature, humidity, wind speed, and more.

## Features

- **HTTP Sensor**: Checks if the weather API is ready.
- **Data Extraction**: Extracts weather data using an HTTP GET request.
- **Data Transformation**: Transforms the extracted data into a structured format.
- **Data Loading**: Loads the transformed data into an AWS S3 bucket.

## Installation

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/your-repo/weather-data-pipeline.git
    cd weather-data-pipeline
    ```

2. **Install Dependencies**:
    Ensure you have Apache Airflow and other necessary dependencies installed. You can use the following command to install Airflow:
    ```bash
    pip install apache-airflow
    ```

3. **Set Up AWS Credentials**:
    Replace the placeholder values for AWS credentials in the `transform_load_data` function with your actual AWS access key, secret key, and session token.

## Configuration

1. **Airflow Connections**:
    - Set up an Airflow HTTP connection named `weathermap_api` with the base URL of the weather API.
    - Add your API key to the endpoint in the DAG script.

2. **DAG Configuration**:
    - Modify the `default_args` dictionary as needed, particularly the email configuration.
    - Set the `start_date` to your desired start date.
    - Adjust the `schedule_interval` to control how frequently the DAG runs.

## Code Explanation

### Imports

- **Airflow**: For creating and managing the DAG.
- **Datetime and Timedelta**: For managing date and time operations.
- **HTTP Sensor and Operator**: For making HTTP requests and handling responses.
- **Pandas**: For data manipulation and transformation.

### Functions

- **kelvin_to_fahrenheit**: Converts temperature from Kelvin to Fahrenheit.
- **transform_load_data**: Transforms the extracted weather data and loads it into an AWS S3 bucket.

### Default Arguments

Defines default arguments for the DAG, including the owner, start date, retry configuration, and email settings.

### DAG Definition

- **is_weather_api_ready**: Checks if the weather API is ready to provide data.
- **extract_weather_data**: Extracts weather data from the API.
- **transform_load_weather_data**: Transforms and loads the weather data into an S3 bucket.

### DAG Workflow

Defines the task dependencies to ensure the tasks run in the correct order:
```plaintext
is_weather_api_ready >> extract_weather_data >> transform_load_weather_data
