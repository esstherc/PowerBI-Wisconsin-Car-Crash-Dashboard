# Wisconsin-Car-Crash-Dashboard
![alt text](images/Dashboard-1.jpg)
## Demo 
- [Video](https://www.youtube.com/watch?v=MDELlRKnYrM&ab_channel=YanbingChen)
- [PowerBI Dashboard - online version](https://app.powerbi.com/view?r=eyJrIjoiZjJiZTBiZjYtZmM1MC00YzQyLWE5YTctN2FjZWVmOGZhM2M3IiwidCI6IjZmMGJiNzJmLTUzNzctNGRkZi05MzZhLWI2YzcyYmYyMWFlMiIsImMiOjF9&pageName=ReportSection122b823e02231482f562)
- The map displayed in the PowerBI Dashboard contains over 30,000 dots, exceeding the limit for publishing reports, which is fewer than 30,000 dots. As a result, the map feature may not be visible in the published version of the report. However, all other features of the dashboard are functioning properly and are available for use.

## Introduction
- This project is aimed at developing a Power BI Dashboard for generating insights about car crash accident data in Wisconsin, US.

## Dataset
#### Original dataset
- [Countrywide traffic accident dataset](https://arxiv.org/pdf/1906.05409.pdf
) (February 2016 to March 2023)
- Approximately 7.7 million records of traffic accidents

#### Data Preprocessing 
- Python(filtering and create new categorical columns)
- Power BI (Calculating new data fields)
- Dataset: 34688 WI Records out of 7.7 million data

## Target Audience
- Government entities and policymakers (Local and state transportation departments,emergency services......)
- Wisconsin residents

## Potential Research Questions
1. What is the spatial pattern of traffic accidents in Wisconsin?  
2. Are there specific times of day or month when traffic accidents are more likely to occur, and what is their impact on traffic patterns?  
3. How do traffic signs and signals, road infrastructure, and traffic calming measures influence the frequency and severity of traffic accidents in Wisconsin?  
4. How do weather conditions or other environmental stimuli affect the occurrence of traffic accidents?  

## Installation / Usage
- Install Power BI Desktop from [Official Power BI Download Site](https://powerbi.microsoft.com/en-us/downloads/) in Windows laptop
- Download data files from link given in Introduction
- Clone/download this repository to your local machine
- Open Dashboard report file (Wisconsin Car Crash Dashboard.pbix) in Power BI Desktop

## DAX Formulas Used in Measures
```
Time Classification = 
    VAR CurrentHour= 'Traffic Accidents in Wisconsin'[Hour]
RETURN
    SWITCH(
        TRUE(),
        CurrentHour >= 6 && CurrentHour < 10, "Morning Commute",
        CurrentHour >= 10 && CurrentHour < 16, "Daytime",
        CurrentHour >= 16 && CurrentHour < 19, "Evening Commute",
        CurrentHour >= 19 && CurrentHour < 23, "Evening",
        "Late Night to Early Morning"
    )
```
```
Weather Category = SWITCH(
    TRUE(),
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"Overcast", "Scattered Clouds", "Mostly Cloudy", "Partly Cloudy", "Fair", "Clear", "Mostly Cloudy / Windy", "Partly Cloudy / Windy", "Fair / Windy"}, "Clear or Partly Cloudy",
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"Cloudy", "Cloudy / Windy", "Haze", "Mist", "Haze / Windy"}, "Cloudy",
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"Light Rain", "Heavy Rain", "Rain", "Light Rain with Thunder", "Showers in the Vicinity", "Drizzle", "Light Drizzle", "Heavy Drizzle", "Rain / Windy", "Drizzle and Fog", "Drizzle / Windy", "Heavy Rain / Windy", "Light Rain / Windy", "Light Drizzle / Windy", "Light Rain Showers", "Light Rain Shower", "Thunder in the Vicinity"}, "Rain",
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"Light Snow", "Snow", "Wintry Mix", "Heavy Snow", "Snow and Sleet", "Light Snow / Windy", "Snow / Windy", "Heavy Snow / Windy", "Light Snow with Thunder", "Blowing Snow", "Wintry Mix / Windy", "Blowing Snow / Windy", "Light Snow Shower", "Light Snow and Sleet", "Heavy Snow with Thunder"}, "Snow or Wintry Conditions",
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"T-Storm", "Thunder", "Heavy T-Storm", "T-Storm / Windy", "Thunderstorm", "Heavy T-Storm / Windy", "Light Thunderstorms and Rain", "Heavy Thunderstorms and Rain", "Thunderstorms and Rain"}, "Thunderstorms",
    'Traffic Accident in Wisconsin'[Weather_Condition] IN {"Light Freezing Rain", "Light Sleet", "Light Freezing Drizzle", "Light Ice Pellets", "Light Snow Grains", "Freezing Rain", "Light Freezing Rain / Windy", "Sleet / Windy", "Heavy Sleet / Windy", "Freezing Rain / Windy", "Heavy Sleet", "Light Freezing Fog"}, "Icy or Freezing Conditions",
    'Traffic Accident in Wisconsin'[Weather_Condition] = "N/A Precipitation", "No Precipitation or Data Unavailable",
    "Unknown" // Default case if none of the above conditions are met
)
```

If you'd like to request a new function, feel free to open an new issue. Please include sample queries and their corresponding results.

## Authors
[Yanbing Chen](https://github.com/esstherc/)  
[Qianheng Zhang](https://github.com/QianhengZhang)  
April,2024