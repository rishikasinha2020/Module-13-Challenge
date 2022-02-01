1. ***Deliverable 1***: Add Tectonic Plate Data
2. ***Deliverable 2***: Add Major Earthquake Data
3. ***Deliverable 3***: Add an Additional Map
4. ***Deliverable 4***: A written report on the Mapping Earthquakes analysis

## Resources and Before Start Notes:

* Data Source: `tectonic_plate_starter_logic.js`, `tectonic_plate_starter_logic.js`, `tectonic_plate_starter_logic.js` and `index.html`
* Data Tools: JavaScript, JSON, GeoJSON and IO (Web Server)
* Software: ES6+, ECMAScript and Visual Studio Code 1.50.0

For more information, visit [`The Mapbox API`](https://www.mapbox.com/pricing/?utm_medium=blog&utm_source=mapbox-blog&utm_campaign=blog%7Cmapbox-blog%7Cpricing%7Cnew-pricing-46b7c26166e7-19-05&utm_term=pricing&utm_content=new-pricing-46b7c26166e7/). 

Overview of Project
Basil and Sadhana like how you created your earthquake map with two different maps and the earthquake overlay. Now, Basil and Sadhana would like to see the earthquake data in relation to the tectonic plates’ location on the earth, and they would like to see all the earthquakes with a magnitude greater than 4.5 on the map, and they would like to see the data on a third map.
1.	Deliverable 1: Add Tectonic Plate Data
2.	Deliverable 2: Add Major Earthquake Data
3.	Deliverable 3: Add an Additional Map
4.	Deliverable 4: A written report on the Mapping Earthquakes analysis README.md.
Resources and Before Start Notes:
•	Data Source: tectonic_plate_starter_logic.js, tectonic_plate_starter_logic.js, tectonic_plate_starter_logic.js and index.html
•	Data Tools: JavaScript, JSON, GeoJSON and IO (Web Server)
•	Software: ES6+, ECMAScript and Visual Studio Code 1.50.0
For more information, visit The Mapbox API.

Technical Overview:
In this module, you will use the Leaflet.js Application Programming Interface (API) to populate a geographical map with GeoJSON earthquake data from a URL. Each earthquake will be visually represented by a circle and color, where a higher magnitude will have a larger diameter and will be darker in color. In addition, each earthquake will have a popup marker that, when clicked, will show the magnitude of the earthquake and the location of the earthquake.
Basic Project Plan
Purpose The purpose of this project is to visually show the differences between the magnitudes of earthquakes all over the world for the last seven days.
Tasks To complete this project, use a URL for GeoJSON earthquake data from the USGS website and retrieve geographical coordinates and the magnitudes of earthquakes for the last seven days. Then add the data to a map.
Approach Your approach will be to use the JavaScript and the D3.js library to retrieve the coordinates and magnitudes of the earthquakes from the GeoJSON data. You'll use the Leaflet library to plot the data on a Mapbox map through an API request and create interactivity for the earthquake data.
Now that you have an overview of the project plan, let's set up a Mapbox account and get the API token you'll need to create geographical maps.

Deliverable Requirements:
Using your knowledge of JavaScript, Leaflet.js, and geoJSON data, you’ll add tectonic plate data using d3.json(), add the data using the geoJSON() layer, set the tectonic plate LineString data to stand out on the map, and add the tectonic plate data to the overlay object with the earthquake data.
Final map looks similar to the following image:
Module-13 Revised\Mapping_Earthquakes\Resources\Image13.1.png(Refer to the image in this path)

Deliverable 1: Add Tectonic Plate Data
// DELIVERABLE 1 and 2
// Module 13
//Filename: js/challenge_logic.js
// 1. Add a 2nd layer group for the tectonic plate data.
    let allEarthquakes = new L.LayerGroup();
    let tectonicPlates = new L.LayerGroup();
    let majorEarthquakes = new L.LayerGroup();


Deliverable 2: Add Major Earthquake Data
// 2. Add a reference to the tectonic plates group to the overlays object.
//Filename: js/challenge_logic.js
    let overlays = {
        "Earthquakes": allEarthquakes,
        "Tectonic Plates": tectonicPlates,
        "Major Earthquakes": majorEarthquakes
};

// DELIVERABLE 2
// Module 13

d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson").then(function(data) {

  // This function returns the style data for each of the earthquakes we plot on
  // the map. We pass the magnitude of the earthquake into two separate functions
  // to calculate the color and radius.
  function styleInfo(feature) {
    return {
      opacity: 1,
      fillOpacity: 1,
      fillColor: getColor(feature.properties.mag),
      color: "#000000",
      radius: getRadius(feature.properties.mag),
      stroke: true,
      weight: 0.5
    };
  }

  // This function determines the color of the marker based on the magnitude of the earthquake.
  function getColor(magnitude) {
    if (magnitude > 5) {
      return "#ea2c2c";
    }
    if (magnitude > 4) {
      return "#ea822c";
    }
    if (magnitude > 3) {
      return "#ee9c00";
    }
    if (magnitude > 2) {
      return "#eecc00";
    }
    if (magnitude > 1) {
      return "#d4ee00";
    }
    return "#98ee00";
  }
  
// DELIVERABLE 1 and 2
// Module 13
// Here we create a legend control object.
let legend = L.control({
  position: "bottomright"
});

// Then add all the details for the legend
legend.onAdd = function() {
  let div = L.DomUtil.create("div", "info legend");

  const magnitudes = [0, 1, 2, 3, 4, 5];
  const colors = [
    "#98ee00",
    "#d4ee00",
    "#eecc00",
    "#ee9c00",
    "#ea822c",
    "#ea2c2c"
  ];

// Looping through our intervals to generate a label with a colored square for each interval.
  for (var i = 0; i < magnitudes.length; i++) {
    console.log(colors[i]);
    div.innerHTML +=
      "<i style='background: " + colors[i] + "'></i> " +
      magnitudes[i] + (magnitudes[i + 1] ? "&ndash;" + magnitudes[i + 1] + "<br>" : "+");
    }
    return div;
  };

  // Finally, we our legend to the map.
  legend.addTo(map);


  // 3. Use d3.json to make a call to get our Tectonic Plate geoJSON data.
  d3.json("https://raw.githubusercontent.com/fraxen/tectonicplates/master/GeoJSON/PB2002_boundaries.json").then(function(plateData) {
      // Adding our geoJSON data, along with style information, to the tectonicplates
      // layer.
      L.geoJson(plateData, {
        color: "#ff6500",
        weight: 2
      })
      .addTo(tectonicPlates);

      // Then add the tectonicplates layer to the map.
      tectonicPlates.addTo(map);
    
  });
});
4.	The earthquake data and tectonic plate data displayed on the map when the page loads.
      // Module 13
      // Then add the tectonicplates layer to the map.
      tectonicPlates.addTo(map);

Deliverable 3: Add an Additional Map:
1.	A third map tile layer is created.
2.	The third map is added to the overlay object.
3.	All the earthquake data and tectonic plate data are displayed on the all maps of the webpage.
Results with detail analysis:
1.	A third map tile layer is created.

// DELIVERABLE 3
// Module 13
Your final map should look similar to the following image:
Module-13 Revised\Mapping_Earthquakes\Resources\Image13.2.png(Refer to the image in this path)

// Create a base layer that holds all three maps.
let baseMaps = {
  "Streets": streets,
  "Satellite": satelliteStreets,
  "Dark": dark
};

// We create a third tile layer that will be the background of our map.
let dark = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/dark-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', {
	attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
	maxZoom: 18,
	accessToken: API_KEY
});


Deliverable 4:
A written report on the Mapping Earthquakes analysis README.md.
1.	A README.md that describes the purpose of the repository. Although there is no graded written analysis for this challenge, it is encouraged and good practice to add a brief description of your project.
