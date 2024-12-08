<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Driver Traffic Monitoring</title>
  <style>
    body, html {
      margin: 0;
      padding: 0;
      height: 100%;
      font-family: Arial, sans-serif;
    }

    #map {
      height: 75%;
      width: 100%;
    }

    #dashboard {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 25%;
      background: #212121;
      color: white;
      display: flex;
      justify-content: space-around;
      align-items: center;
      padding: 10px;
    }

    .dashboard-item {
      flex: 1;
      text-align: center;
    }

    .dashboard-item h3 {
      margin: 0 0 10px 0;
      color: #f0ad4e;
    }

    .dashboard-item p {
      margin: 0;
      font-size: 16px;
    }

    button {
      padding: 10px 15px;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 3px;
      cursor: pointer;
    }

    button:hover {
      background-color: #218838;
    }
  </style>
  <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places"></script>
</head>
<body>
  <div id="map"></div>
  <div id="dashboard">
    <div class="dashboard-item">
      <h3>Fine</h3>
      <p id="fine">No fines applied</p>
    </div>
    <div class="dashboard-item">
      <h3>Weather</h3>
      <p id="weather">Loading...</p>
    </div>
    <div class="dashboard-item">
      <h3>Time</h3>
      <p id="clock">Loading...</p>
    </div>
  </div>

  <script>
    let map;
    let trafficLayer;
    let stationaryTimer;
    let stationaryTime = 0;
    let lastPosition = null;
    let isTrafficJam = false; // Simulated value for demo purposes
    const fineRate = 50; // Fine rate per minute of being stationary
    let fine = 0;

    // Initialize the map
    function initMap() {
      const initialLocation = { lat: 23.8103, lng: 90.4125 }; // Example: Dhaka

      map = new google.maps.Map(document.getElementById("map"), {
        center: initialLocation,
        zoom: 14,
      });

      trafficLayer = new google.maps.TrafficLayer();
      trafficLayer.setMap(map);

      // Start location tracking
      startLocationTracking();

      // Start the clock
      startClock();

      // Fetch weather information
      fetchWeather();
    }

    // Start tracking the user's location
    function startLocationTracking() {
      if (navigator.geolocation) {
        navigator.geolocation.watchPosition(
          (position) => {
            const currentLocation = {
              lat: position.coords.latitude,
              lng: position.coords.longitude,
            };

            // Check if the car is stationary
            checkStationary(currentLocation);

            // Update map center
            map.setCenter(currentLocation);
          },
          (error) => {
            console.error("Error getting location:", error);
          },
          {
            enableHighAccuracy: true,
            maximumAge: 0,
          }
        );
      } else {
        alert("Geolocation is not supported by your browser.");
      }
    }

    // Check if the car is stationary
    function checkStationary(currentLocation) {
      if (lastPosition) {
        const distance = getDistance(lastPosition, currentLocation);

        if (distance < 10 && !isTrafficJam) {
          // If stationary without traffic jam, start the timer
          if (!stationaryTimer) {
            startTimer();
          }
        } else {
          // If moved or traffic jam detected, reset the timer
          resetTimer();
        }
      }

      lastPosition = currentLocation;
    }

    // Calculate distance between two points (Haversine formula)
    function getDistance(loc1, loc2) {
      const R = 6371e3; // Earth's radius in meters
      const lat1 = (loc1.lat * Math.PI) / 180;
      const lat2 = (loc2.lat * Math.PI) / 180;
      const deltaLat = ((loc2.lat - loc1.lat) * Math.PI) / 180;
      const deltaLng = ((loc2.lng - loc1.lng) * Math.PI) / 180;

      const a =
        Math.sin(deltaLat / 2) * Math.sin(deltaLat / 2) +
        Math.cos(lat1) *
          Math.cos(lat2) *
          Math.sin(deltaLng / 2) *
          Math.sin(deltaLng / 2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));

      return R * c; // Distance in meters
    }

    // Start the stationary timer
    function startTimer() {
      stationaryTimer = setInterval(() => {
        stationaryTime += 1;

        // Apply fine every minute
        if (stationaryTime % 60 === 0) {
          fine += fineRate;
          document.getElementById("fine").innerText = `Fine: $${fine}`;
        }

        // Show warning after 30 seconds
        if (stationaryTime === 30) {
          alert("The car has been stationary for too long without traffic. Please move!");
        }
      }, 1000);
    }

    // Reset the stationary timer
    function resetTimer() {
      clearInterval(stationaryTimer);
      stationaryTimer = null;
      stationaryTime = 0;
    }

    // Start the clock
    function startClock() {
      setInterval(() => {
        const now = new Date();
        document.getElementById("clock").innerText = now.toLocaleTimeString();
      }, 1000);
    }

    // Fetch weather information (mock data for demo purposes)
    function fetchWeather() {
      // Replace this with a real weather API call if needed
      setTimeout(() => {
        document.getElementById("weather").innerText = "Sunny, 30°C";
      }, 2000);
    }

    // Load the map
    window.onload = initMap;
  </script>
</body>
</html>