# Task-1
API integration and Data visualization
import requests
import matplotlib.pyplot as plt
import pandas as pd

# Replace with your OpenWeatherMap API key
API_KEY = 'YOUR_API_KEY'
CITY = 'London' # Example city
UNITS = 'metric' # or 'imperial'

def fetch_weather_data(city, api_key, units):
    """Fetches current weather data for a given city."""
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
    complete_url = f"{base_url}q={city}&appid={api_key}&units={units}"
    response = requests.get(complete_url)
    data = response.json()
    return data

def create_visualization(weather_data):
    """Creates a simple visualization of temperature."""
    if weather_data and weather_data.get('main'):
        temp = weather_data['main']['temp']
        feels_like = weather_data['main']['feels_like']
        humidity = weather_data['main']['humidity']

        data = {'Metric': ['Temperature (°C)', 'Feels Like (°C)', 'Humidity (%)'],
                'Value': [temp, feels_like, humidity]}
        df = pd.DataFrame(data)

        fig, ax = plt.subplots(figsize=(8, 6))
        ax.bar(df['Metric'], df['Value'], color=['skyblue', 'lightcoral', 'lightgreen'])
        ax.set_ylabel('Value')
        ax.set_title(f'Current Weather in {CITY}')
        plt.grid(axis='y', linestyle='--')
        plt.show()
    else:
        print("Could not retrieve weather data or invalid data format.")

if _name_ == "_main_":
    weather_data = fetch_weather_data(CITY, API_KEY, UNITS)
    if weather_data:
        print(f"Fetched weather data for {CITY}: {weather_data}")
        create_visualization(weather_data)
    else:
        print("Failed to fetch weather data.")
