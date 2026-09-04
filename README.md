# Weather Dashboard

A Power BI dashboard analyzing weather data, built with Power BI Desktop.

## Objective

To build a single-page, at-a-glance weather dashboard for selected cities (Paris, Antalya, Brussels, Berlin, London) that combines current conditions, a 7-day forecast, air quality, and sunrise/sunset and rainfall-chance data in one view — useful for quickly checking today's conditions and the outlook for the week ahead.

## Methodology

**Data source(s):**
- [WeatherAPI.com](https://www.weatherapi.com/) — pulled via its REST API, which returns current conditions, forecast, and air quality data in a single JSON response
- Fields used include `current.air_quality.*` (CO, O3, SO2, NO2, PM10, PM2.5), current conditions (temp, humidity, wind, UV, visibility, pressure, precipitation), `forecast.forecastday[].day` (daily forecast highs), and `forecast.forecastday[].astro` (sunrise/sunset)
- Time period covered: rolling — current day plus a 7-day forecast window
- Update frequency: manual refresh on file open (or scheduled refresh if published to the Power BI service with an API-key-based data source)

**Data preparation:**
- Flattened the nested JSON response (current conditions, forecast days, and air quality are separate nested objects in the API response) into flat tables suitable for visuals
- Converted forecast day labels into short weekday names (Fri, Sat, Sun...) for the forecast strip and line chart

**Modeling approach:**
- Separate tables for current conditions, daily forecast, and air quality, linked by city and date
- City selector (Paris / Antalya / Brussels / Berlin / London) drives the current-conditions panel
- Air quality shown both as a composite CO-based gauge and as individual pollutant readings (O3, SO2, NO2, PM10, PM2.5)

## Conclusion

The dashboard successfully consolidates current conditions, a 7-day outlook, and air quality into one view, making it easy to compare cities and anticipate the week ahead at a glance. Since it depends on a live API, its main limitation is that insights are only as current as the last refresh — for production use, scheduling automatic refreshes (e.g. via Power BI service with a stored API key) would keep it up to date without manual intervention.


## Project structure

weather-dashboard/
├── weather_dashboard.pbix          # Original Power BI file
├── weather_dashboard.pbip          # Power BI Project pointer file
├── weather_dashboard.Report/       # Report visuals/layout (text-based)
├── weather_dashboard.SemanticModel/ # Data model, measures, relationships (text-based)
├── .gitignore
└── README.md

## How to open

1. Clone this repo.
2. Open `weather_dashboard.pbip` in Power BI Desktop (requires the "Power BI Project (.pbip) save option" preview feature enabled).
   - Alternatively, open `weather_dashboard.pbix` directly for the standard file.
3. If the report uses an external data source, you may need to update credentials or connection settings under **Transform data > Data source settings**.

## Requirements

- Power BI Desktop (version [X], [month/year])
- [Any data source credentials or API keys needed — do not commit these]
