What's the Weather Like?

## Background

Whether financial, political, or social -- data's true power lies in its ability to answer questions definitively. So let's take what you've learned about Python requests, APIs, and JSON traversals to answer a fundamental question: "What's the weather like as we approach the equator?"

Now, we know what you may be thinking: _"Duh. It gets hotter..."_

But, if pressed, how would you **prove** it?

![Equator](Images/equatorsign.png)

## WeatherPy  http://localhost:8888/notebooks/2/Activities/05-Ins_OpenWeatherDataFrame/Solved/Ins_OpenWeatherDataFrame.ipynb 

In this example, you'll be creating a Python script to visualize the weather of 500+ cities across the world of varying distance from the equator. To accomplish this, you'll be utilizing a [simple Python library](https://pypi.python.org/pypi/citipy), the [OpenWeatherMap API](https://openweathermap.org/api), and a little common sense to create a representative model of weather across world cities.

Your objective is to build a series of scatter plots to showcase the following relationships:

* Temperature (F) vs. Latitude
* Humidity (%) vs. Latitude
* Cloudiness (%) vs. Latitude
* Wind Speed (mph) vs. Latitude

Your final notebook must:

* Randomly select **at least** 500 unique (non-repeat) cities based on latitude and longitude.
* Perform a weather check on each of the cities using a series of successive API calls.
* Include a print log of each city as it's being processed with the city number and city name.
* Save both a CSV of all data retrieved and png images for each scatter plot.

As final considerations:

* You must complete your analysis using a Jupyter notebook.
* You must use the Matplotlib or Pandas plotting libraries.
* You must include a written description of three observable trends based on the data.
* You must use proper labeling of your plots, including aspects like: Plot Titles (with date of analysis) and Axes Labels.
* See [Example Solution](WeatherPy_Example.pdf) for a reference on expected format.

## Hints and Considerations

* The city data is generated based on random coordinates; as such, your outputs will not be an exact match to the provided starter notebook.

* You may want to start this assignment by refreshing yourself on the [geographic coordinate system](http://desktop.arcgis.com/en/arcmap/10.3/guide-books/map-projections/about-geographic-coordinate-systems.htm).

* Next, spend the requisite time necessary to study the OpenWeatherMap API. Based on your initial study, you should be able to answer  basic questions about the API: Where do you request the API key? Which Weather API in particular will you need? What URL endpoints does it expect? What JSON structure does it respond with? Before you write a line of code, you should be aiming to have a crystal clear understanding of your intended outcome.

* A starter code for Citipy has been provided. However, if you're craving an extra challenge, push yourself to learn how it works: [citipy Python library](https://pypi.python.org/pypi/citipy). Before you try to incorporate the library into your analysis, start by creating simple test cases outside your main script to confirm that you are using it correctly. Too often, when introduced to a new library, students get bogged down by the most minor of errors -- spending hours investigating their entire code -- when, in fact, a simple and focused test would have shown their basic utilization of the library was wrong from the start. Don't let this be you!

* Part of our expectation in this challenge is that you will use critical thinking skills to understand how and why we're recommending the tools we are. What is Citipy for? Why would you use it in conjunction with the OpenWeatherMap API? How would you do so?

* In building your script, pay attention to the cities you are using in your query pool. Are you getting coverage of the full gamut of latitudes and longitudes? Or are you simply choosing 500 cities concentrated in one region of the world? Even if you were a geographic genius, simply rattling 500 cities based on your human selection would create a biased dataset. Be thinking of how you should counter this. (Hint: Consider the full range of latitudes).

* Lastly, remember -- this is a challenging activity. Push yourself! If you complete this task, then you can safely say that you've gained a strong mastery of the core foundations of data analytics and it will only go better from here. Good luck!

## Copyright

Data Boot Camp © 2018. All Rights Reserved.


#Cloudiness Plot plt.scatter(cities_remove["Latitude"],cities_remove["Cloudliness"],edgecolors="black",linewidths=1.5,marker="o") 
#Plot labels plt.title("Cloudiness (%) vs. Latitude (12/03/2017)") 
plt.ylabel("Cloudiness (%)") 
plt.xlabel("Latitude") 
plt.grid=True 
plt.xlim([-95,95]) 
plt.ylim([-5,105]) #Save Plot 
plt.savefig("Cloudiness (%) vs. Latitude.png") 
plt.show()

Findings
• Latitude seems to have the most impact on Temperature
• Latitude seems to have little impact on Cloudliness and Wind Speed
• Latitude seems to have a minor effect on Humidity

# Save config information
url = "http://api.openweathermap.org/data/2.5/weather?"
city = "London"

# Build query URL
query_url = url + "appid=" + api_key + "&q=" + city
query_url

# Get weather data
weather_response = requests.get(query_url)
weather_json = weather_response.json()

# Get the temperature from the response
print(f"The weather API responded with: {weather_json}.")
weather = json.dumps(weather_json, indent=2, sort_keys=True)
print(weather)

The weather API responded with: {'coord': {'lon': -0.13, 'lat': 51.51}, 'weather': [{'id': 800, 'main': 'Clear', 'description': 'clear sky', 'icon': '01n'}], 'base': 'stations', 'main': {'temp': 282.35, 'pressure': 1023, 'humidity': 76, 'temp_min': 279.15, 'temp_max': 284.82}, 'visibility': 10000, 'wind': {'speed': 1, 'deg': 240}, 'clouds': {'all': 0}, 'dt': 1567385409, 'sys': {'type': 1, 'id': 1502, 'message': 0.0088, 'country': 'GB', 'sunrise': 1567401255, 'sunset': 1567450013}, 'timezone': 3600, 'id': 2643743, 'name': 'London', 'cod': 200}.
{
  "base": "stations",
  "clouds": {
    "all": 0
  },
  "cod": 200,
  "coord": {
    "lat": 51.51,
    "lon": -0.13
  },
  "dt": 1567385409,
  "id": 2643743,
  "main": {
    "humidity": 76,
    "pressure": 1023,
    "temp": 282.35,
    "temp_max": 284.82,
    "temp_min": 279.15
  },
  "name": "London",
  "sys": {
    "country": "GB",
    "id": 1502,
    "message": 0.0088,
    "sunrise": 1567401255,
    "sunset": 1567450013,
    "type": 1
  },
  "timezone": 3600,
  "visibility": 10000,
  "weather": [
    {
      "description": "clear sky",
      "icon": "01n",
      "id": 800,
      "main": "Clear"
    }
  ],
  "wind": {
    "deg": 240,
    "speed": 1
  }
}

# Dependencies
import csv
import matplotlib.pyplot as plt
import requests
import pandas as pd
from config import api_key

# Save config information.
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "metric"

# Build partial query URL
query_url = f"{url}appid={api_key}&units={units}&q="

cities = ["Paris", "London", "Oslo", "Beijing"]

# set up lists to hold reponse info
lat = []
temp = []

# Loop through the list of cities and perform a request for data on each
for city in cities:
    response = requests.get(query_url + city).json()
    lat.append(response['coord']['lat'])
    temp.append(response['main']['temp'])

print(f"The latitude information received is: {lat}")
print(f"The temperature information received is: {temp}")


The latitude information received is: [48.86, 51.51, 59.91, 39.91]
The temperature information received is: [11.31, 9.02, 9.03, 26.72]
# create a data frame from cities, lat, and temp
weather_dict = {
    "city": cities,
    "lat": lat,
    "temp": temp
}
weather_data = pd.DataFrame(weather_dict)
weather_data.head()

citylattemp0Paris48.8611.311London51.519.022Oslo59.919.033Beijing39.9126.72# Build a scatter plot for each data type
plt.scatter(weather_data["lat"], weather_data["temp"], marker="o")

# Incorporate the other graph properties
plt.title("Temperature in World Cities")
plt.ylabel("Temperature (Celsius)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("TemperatureInWorldCities.png")

# Show plot
plt.show()

# Dependencies
import requests
from config import api_key

# Save config information.
url = "http://api.openweathermap.org/data/2.5/weather?"
city = "Bujumbura"
units = "metric"
# Build query URL and request your results in Celsius
query_url = f"{url}appid={api_key}&q={city}&units={units}"

# Get weather data
weather_response = requests.get(query_url)
weather_json = weather_response.json()

# Get temperature from JSON response
temperature = weather_json["main"]["temp"]
# Report temperature
print(f"The temperature in Bujumbura is {temperature} C.")
# BONUS

# use list of units
units = ["metric", "imperial"]

# set up list to hold two different temperatures
temperatures = []

# loop throught the list of units and append them to temperatures list
for unit in units:
    # Build query URL based on current element in units
    query_url = url + "appid=" + api_key + "&q=" + city + "&units=" + unit

    # Get weather data
    weather_response = requests.get(query_url)
    weather_json = weather_response.json()

    # Get temperature from JSON response
    temperature = weather_json["main"]["temp"]

    temperatures.append(temperature)

# Report temperatures by accessing each element in the list
print(
    f"The temperature in Bujumbura is {temperatures[0]}C or {temperatures[1]}F.")
The temperature in Bujumbura is 16.81C or 62.27F.


