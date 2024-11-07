# Fetching the Census Data Using the Census API
This is a Python script that fetches Census data for the United States from the American Community Survey (ACS) for multiple years and states. The data is fetched using the Census API and saved in a CSV file for futher analysis.

## Features
- **Fetch Data for Multiple Years and States**: Specify a range of years  (e.g: 2010-2020) and a state using its FIPS code to retrieve Census data for that location. The default state is Texas (FIPS code 48).
- **Customizable Variables**: Define the specific Census variables to retrieve by updating the 'variable' list in the script. This allows extraction of various demographic, economic, and housing data points.

## Getting Started

### Prerequisites
- Python 3.x
- Required libraries:
  - [Requests library](https://pypi.org/project/requests/) for making API calls
  - [Pandas](https://pypi.org/project/pandas/) for data handling
  - [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) for parsing HTML
  - [Census](https://pypi.org/project/census/) for interfacing with the Census API
  - [python-dotenv](https://pypi.org/project/python-dotenv/) for managing environment variables
- A Census API key (sign up [here](https://api.census.gov/data/key_signup.html) if you don't already have one)

### Installation
1. Clone this repository or download the ```state_year.ipynb```:
   ```bash
    git clone https://github.com/jibekgupta/census.git
    cd census
    ```
2. Install the required packages:
   ```bash
   pip install requests pandas beautifulsoup4 census python-dotenv
   ```
3. Create a ```.env``` file in the same directory as the ```state_year.ipynb``` file and add your Census API key:
   ```bash
   API_KEY = 'your_api_key_here'
   ```
### Usage
1. Open the ```state_year.ipynb``` Jupyter notebook or any Python environment.

2. Update the **variable list** with the desired variables in the cell with ```race_variables```. For example:
   ```python
   race_variable = ["B01001_001E",
              "B19013_001E",
               # Add more variables as needed
   ]
   ```
   
3. Update the **State FIPS code**
   ```python
   def fetch_census_data(year, variable_label_mapping, state=48)
   # Change the state = FIPS code for your required state
   ```

4. Set the **Year Range** for data collection:
   ```python
   def collect_all_years_data(start_year=1926, end_year=2026):
   # Modify start_year and end_year according to your needs
   ```

5. Specify the **ACS survey type (```acs1``` or ```acs5```)**:
   ```python
   variables_url = f'https://api.census.gov/data/{year}/acs/acs1/variables.html'

   url = f'https://api.census.gov/data/{year}/acs/acs1?get=NAME,{",".join(race_variable)}&for=state:{state}&key={api_key}
   # Change 'acs1' to 'acs5' if required
   ```

6. Update the **Output File Name** if needed:
   ```python
   output_files = "TX_census_data_with_labels_acs5.csv"
   # Rename the file as needed
   ```
7. Run the notebook to start data coleection


## Code Explanation
- **Loading Libraries and API Key**:
  ```python
  %load_ext autotime
  import pandas as pd
  import requests
  from bs4 import BeautifulSoup
  from census import Census
  import os
  from dotenv import load_dotenv
  load_dotenv(dotenv_path='key.env')
  api_key=os.getenv('API_KEY')
  ```
  
- **Fetch Variable Labels**: Fetches the labels for specified Census variables for each year.
  ```python
  def fetch_variable_labels(year):
      # Define amd request variables page, then parse to ectract labels
  ```

- **Fetch Census Data**: Retrieves Census data for the given year and state.
  ```python
  def fetch_census_data(year, variable_label_mapping, state=48):
      # Requests data from teh Census API and structures it in a dictionary
  ```
- **Collect Data Across Years**: Loops over the specified years to collect and store data.
  ```python
  def collect_all_years_data(start_year=1926, end_year=2026):
      # Collects data over the year range and compiles it into a DataFrame
  ```

## Example
For example, to fetch ACS data for Texas (FIPS code 48) from 2010 to 2020, with specific variables in race demographics, set ```state=48```, ```start_year=2010```, and ```end_year=2020```, then run the ```collect_all_years_data``` function notebook.

## Output 
The collectd data will be saved to a CSV file(e.g. ```TX_census_data_with_labels_acs5.csv```), ready for futher analysis.

