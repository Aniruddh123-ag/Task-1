# Task-1
API integration and Data visualization
<br>

import requests
<br>
import matplotlib.pyplot as plt
<br>
import pandas as pd
<br>

# Replace with your OpenWeatherMap API key
API_KEY = 'YOUR_API_KEY'
<br>
CITY = 'London' # Example city
<br>
UNITS = 'metric' # or 'imperial'
<br>

def fetch_weather_data(city, api_key, units):
<br>
    """Fetches current weather data for a given city."""
    <br>
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
    <br>
    complete_url = f"{base_url}q={city}&appid={api_key}&units={units}"
    <br>
    response = requests.get(complete_url)
    <br>
    data = response.json()
    <br>
    return data
    <br>

def create_visualization(weather_data):
    """Creates a simple visualization of temperature."""
    <br>
    if weather_data and weather_data.get('main'):
    <br>
        temp = weather_data['main']['temp']
        <br>
        feels_like = weather_data['main']['feels_like']
        <br>
        humidity = weather_data['main']['humidity']
        <br>

        data = {'Metric': ['Temperature (°C)', 'Feels Like (°C)', 'Humidity (%)'],
                'Value': [temp, feels_like, humidity]}
        df = pd.DataFrame(data)
        <br>

        fig, ax = plt.subplots(figsize=(8, 6))
        ax.bar(df['Metric'], df['Value'], color=['skyblue', 'lightcoral', 'lightgreen'])
        ax.set_ylabel('Value')
        ax.set_title(f'Current Weather in {CITY}')
        plt.grid(axis='y', linestyle='--')
        plt.show()
    else:
        print("Could not retrieve weather data or invalid data format.")

if _name_ == "_main_":
<br>
    weather_data = fetch_weather_data(CITY, API_KEY, UNITS)
    <br>
    if weather_data:
    <br>
        print(f"Fetched weather data for {CITY}: {weather_data}")
        <br>
        create_visualization(weather_data)
        <br>
    else:
    <br>
        print("Failed to fetch weather data.")
