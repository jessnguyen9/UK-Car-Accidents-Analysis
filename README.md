# Accident Data Analysis and Visualization

## Overview
This project analyzes and visualizes accident data from Calderdale, UK, using JavaScript, Python (Flask), and SQL. The goal is to provide an interactive dashboard and a dynamic map to explore accident trends over multiple years, helping users understand factors such as weather, lighting, and road conditions that contribute to accidents.
This code was designed to read in GEOJSON accident data sourced from the Calderdale district of West Minster, UK.

## Technologies Used
- **JavaScript** (D3.js, Leaflet.js, Plotly.js) for data visualization
- **Python** (Flask) for backend API and data retrieval
- **SQLite** for database storage
- **HTML & CSS** for frontend interface

## Features
- **Interactive Leaflet Map:** Displays accident locations with color-coded markers based on the year.
- **Dashboard with Bar and Pie Charts:** Allows users to filter accident data by year and analyze trends in accident severity, weather conditions, lighting, and road surfaces.
- **Flask API:** Serves accident data from an SQLite database and provides access to static GeoJSON files.
It contains:
    - JavaScript code that renders a leaflet map
    - Javascript code that renders an interactive user dashboard
     - HTML and CSS files
     - Flask application for retrieving accident data by the year from a SQLite database.
   
    Before using this code:
        - Check that the geojson files and png files for the markers are stored in their correct folders.
        - Install required dependencies d3.js and plotly libraries.
        - Include correct <script> tags in your HTML and CSS files to load these libraries. 

## Javascript: Leaflet Map

    This javascript code is designed to create a leaflet map with different colored icons for each year of accident data.

Step by Step explanation:
    
- Creates colored marker icons that will later be used for each year of data.

- Function to create map :
    Creates a map object centered on Calderdale with layers to hold accident data by year. 

- Function to create markers:
    Creates a marker for each point where an accident has happened. Assigns data to it's layer group based on year.

- Promise All:
    Pulls the data from each individual the geojson file and creates a layer group. 
    
    It then selects the correct icon for the year and then calls the createMarkers function to create markers for the layer group.  

    The layer groups are stored in an array to be called by the changeYear function to allow the user to toggle each year of data on or off.

## Javascript: User Interactive Dashboard

    This javascript code is designed to create interactive bar and pie charts where the user can select the year of data they wish to look at and different circumstances under which accidents took place. 

Step by Step explination:

- Data Retreieval:
    The data retrieval is done through D3.js using d3.json(url) function. 
    
    The URL is constructed based on the selected sample year to access the corresponding GeoJSON data.
    
- Creating filters on data for visuals & chart creation:
    - Filtering the data; preparing it for visuals;
            lines 42-510 
    - Bar Charts: lines 513-613 
        The code creates bar charts for various attributes such as "Weather Conditions," "Lighting Conditions," "Road Surface Conditions," and "Number of Vehicles." 
        
        Each bar chart represents the number of accidents for each category of the attribute.

    - Pie Charts: lines 614-658 
        The code generates pie charts to show the proportion of accident severity (Fatal, Serious, Slight) and the number of vehicles involved in accidents during different severity levels.

Creating the drop down menu: lines 660-688
    - Creates interactive toggle where user can change the year and specified chart data while hiding the others.

Initialize the function with init():

Sets up the initial state of the dashboard by:

    - Selecting the Dataset: It initializes a dropdown selector (#selDataset) that allows the user to choose the dataset they want to visualize

    - Toggle Selected Bar and Pie Charts: It calls the functions toggleSelectedBar() and toggleSelectedPie() with the parameter first=true

    - Fetching and Displaying Data: It calls the visuals(2017) function to fetch and display the accident data for the year 2017. This function retrieves the GeoJSON data for the year, processes it, and creates various visualizations using Plotly based on the retrieved data.

## Flask API 

    Before using this app:
        - Install required dependencies by running pip install Flask SQLAlchemy in python environment. 
        - Have Accidents.sqlite database in the Data folder and it contains the followign tables: 
            Accident_2017
            Accident_2018
            Accident_2019
            Accident_2020
        - Store static goejson files in the geojson directory within the project. 

Step by Step Explination:

- Run Flask application by entering the following into gibash:
    python app.py

- GET /api/v1.0/accidents/<int:year>
    This endpoint retrieves accident data for a specific year. 
    
    The available years are 2017, 2018, 2019, and 2020.
    
    If a valid year is provided, the endpoint returns a JSON response containing accident details for that year. 

- GET /geojson/<string:filename>
    This endpoint serves static GeoJSON files stored in the geojson directory. 
    
    It allows clients to access and download GeoJSON files for visualizing accident data on maps or other applications.
