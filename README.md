<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive College Navigation</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
    <style>
        #map { height: 80vh; width: 100%; }
        #controls { margin: 10px; text-align: center; }
    </style>
</head>
<body>
    <h2>College Campus Navigation</h2>
    <div id="controls">
        <label for="landmark">Select Landmark:</label>
        <select id="landmark">
            <option value="">--Choose a location--</option>
            <option value="KC">KC Ground</option>
            <option value="AB1">AB1</option>
            <option value="AB2">AB2</option>
            <option value="AB3">AB3</option>
            <option value="AB4">AB4</option>
            <option value="AB5">AB5</option>
            <option value="AB6">AB6</option>
            <option value="AB7">AB7</option>
            <option value="AB8">AB8</option>
            <option value="AB9">AB9</option>
            <option value="AB10">AB10</option>
            <option value="AB11">AB11</option>
            <option value="Mess">I&J Mess</option>
            <option value="Hostel">Girls Hostel</option>
            <option value="Dispensary">Dispensary</option>
            <option value="GD Subway">GD Subway</option>
            <option value="Home">Home</option>
        </select>
        <button onclick="locateLandmark()">Find</button>
    </div>
    <div id="map"></div>
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
    <script>
        var map = L.map('map').setView([27.495, 77.678], 17); // Adjust coordinates as needed
        
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; OpenStreetMap contributors'
        }).addTo(map);
        
        var landmarks = {
            "KC": [27.497, 77.675],
            "AB1": [27.496, 77.676],
            "AB2": [27.495, 77.677],
            "AB3": [27.494, 77.678],
            "AB4": [27.493, 77.679],
            "AB5": [27.492, 77.680],
            "AB6": [27.491, 77.681],
            "AB7": [27.490, 77.682],
            "AB8": [27.489, 77.683],
            "AB9": [27.488, 77.684],
            "AB10": [27.487, 77.685],
            "AB11": [27.486, 77.686],
            "Mess": [27.495, 77.674],
            "Hostel": [27.494, 77.673],
            "Dispensary": [27.493, 77.672],
            "GD Subway": [27.492, 77.671],
            "Home": [27.779142, 77.440445]
        };
        
        for (var key in landmarks) {
            L.marker(landmarks[key]).addTo(map).bindPopup(key);
        }
        
        function locateLandmark() {
            var selectedLandmark = document.getElementById("landmark").value;
            if (selectedLandmark && landmarks[selectedLandmark]) {
                map.setView(landmarks[selectedLandmark], 18);
            }
        }
        
        // Get User Location
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(function (position) {
                var userLocation = [position.coords.latitude, position.coords.longitude];
                L.marker(userLocation).addTo(map).bindPopup("You are here").openPopup();
                map.setView(userLocation, 17);
            });
        }
    </script>
</body>
</html>
