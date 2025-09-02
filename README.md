<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Simple Weather App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 40px;
    }
    input {
      padding: 10px;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-left: 10px;
    }
    #weather {
      margin-top: 30px;
      font-size: 20px;
    }
  </style>
</head>
<body>
  <h1>Weather App</h1>
  <input type="text" id="cityInput" placeholder="Enter city (e.g., London)" />
  <button onclick="getWeather()">Get Weather</button>
  <div id="weather"></div>

  <script>
    async function getWeather() {
      const city = document.getElementById('cityInput').value.trim();
      if (!city) {
        alert("Please enter a city name.");
        return;
      }
  
      const apiKey = "9776ef9eab0a4df8be6123710250209";
      const url = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city}&aqi=yes`;
  
      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error("Network response was not ok.");
        const data = await response.json();
  
        // Accessing correct fields based on WeatherAPI response
        const temperature = data.current.temp_c;
        const condition = data.current.condition.text;
        const location = data.location.name;
  
        document.getElementById('weather').innerHTML = `
          <p><strong>City:</strong> ${location}</p>
          <p><strong>Temperature:</strong> ${temperature}°C</p>
          <p><strong>Condition:</strong> ${condition}</p>
        `;
      } catch (error) {
        console.error("Error fetching weather data:", error);
        document.getElementById('weather').textContent = "Failed to retrieve weather data.";
      }
    }
  </script>
  
</body>
</html>
