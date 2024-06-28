# myradar-web-sdk
MyRadar is pleased to provide an SDK and tools for adding weather data to your web projects.  Currently, this SDK provides the ability to display and animate weather layers over a google maps object.

To get started, add the MyRadar SDK to your project

```bash

npm install @myradar/layers --save

```

```typescript

import layers from '@myradar/layers'

```

After the Google Maps object is initialized, create an ```ImageOverlay``` type and load a layer

```typescript

const overlay = new layers.ImageOverlay(
    host, 
    (validTimeString) => {}, //image changed callback (optional)
    (index, validTimeString, img) => {}, //image loaded callback (optional)
    () => {} //map view changed callback (optional)
  );

```

Once an overlay is created and the map is initialized, add the overlay to the map and load one or more layers on the overlay.  In this case, 

```typescript

const layers = ["15minMRMSPrecipRate", "15minHRRRPrecipRate"];
const now = new Date().getTime()/1000; //current time in seconds
const numImages = 12;

overlay.setMap(map);
overlay.loadLayers(layers, currentTime, numImages, (validTimeStrs, layerValidTimes, layerInfos) => {});

```

A complete example:

```typescript

const overlay = new layers.ImageOverlay(
    host, 
    (validTimeString) => {}, //image changed callback (optional)
    (index, validTimeString, img) => {}, //image loaded callback (optional)
    () => {} //map view changed callback (optional)
  );

const map = new google.maps.Map(mapDiv, {
    center: {39.6, -96.1},
    zoom: 5
  });

google.maps.event.addListenerOnce(map, 'tilesloaded', () => {
  const layers = ["15minMRMSPrecipRate", "15minHRRRPrecipRate"];
  const now = new Date().getTime()/1000; //current time in seconds
  const numImages = 12;

  overlay.setMap(map);
  overlay.loadLayers(layers, currentTime, numImages, (validTimeStrs, layerValidTimes, layerInfos) => {});

  });

```
