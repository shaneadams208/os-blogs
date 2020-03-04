# A Web Developer's Guide to Working With Spatial Data

_Crash course for web devs on how to work with maps and mapping data._

## Intro 

What is a map? Representing reality on an abstracted image. 

What is spatial data?
- "data that describes anything with spatial extent (i.e. size, shape or position)" [w3c/](https://www.w3.org/TR/sdw-bp/)
- "AKA location information"

Coordinates - xyz, plus time. Extra dimensions (attributes).

Viewing the map in a browser. Center or bounding box, zoom, pitch, bearing. Visible layers. etc.

_Spheres and planes_: why is spatial special? 
- The importance of where - illustrate with sorted table vs map of countries
- "As location is often the common factor across multiple datasets, spatial data is an especially useful addition to the Web of data." [w3c](https://www.w3.org/TR/sdw-bp/)
- Spatial relationships

_Servers and clients_: why is web special?
- Mobile browsers deliver the web to users wherever they go

Focus: get you up and running. I will approach this using a specific set of technologies - each step has many ways to solve the same problem. I'll indicate those where possible. (Which technologies should I use?)

⚠️ = snags and pitfalls
👍 = rule of thumb

## Key concepts

Terms defined

Coordinates
- coordinate formats: decimal degrees, deg min sec, radians, etc.
- Locating points on the surface of a sphere.
- Is this getting too in depth? Could be its own post. Don't want to lose people here.

Coordinate Reference Systems
- Geographic Reference Systems
- What it is and why it matters
- CRSs vs Projections
- 👍 - use Web Mercator. Or BNG? (I'd like this to be applicable to a global audience).
- Read more: [OS blog](https://www.ordnancesurvey.co.uk/blog/2016/09/ostn15-new-geoid-britain/), [more technical](https://www.ordnancesurvey.co.uk/documents/resources/guide-coordinate-systems-great-britain.pdf).
- ⚠️: [lon, lat] vs [lat, lon].  

![image](./assets/image-of-coordinate-system.png). <- Do we have OS graphics we want to use? 

Raster
- Tiles
- Formats: tif, png, jpg
- Placing tiles
- Fetching tiles as we zoom
- ZXY ("Zoom X Y"!), WMTS 
- Popular tile servers - Ordnance Survey, OSM, Bing, Mapbox, Stamen
- Advantages and disadvantages  (inspiration [here](https://en.wikipedia.org/wiki/GIS_file_formats#Advantages_and_disadvantages))
- Digital elevation model and hillshade
- Satellite
- Rendered vector maps
- Heatmaps and other raster maps
- Opacity

SVG, canvas, divs.

Vector
- Points, Lines, Polygons
    - Define Feature.
    - Representing geometries: arrays of coordinate pairs.
    - Talk about Multi* / FeatureCollections (image) (types)
    - Complex polygons
- "Layer": collection of similar features  (?? multi-type layers?)
- Formats: geojson, shp, kml, gml, geopackage, vector tiles (code examples - at least of geojson)
    - An aside: topojson.
- Labels.
- geometries and attributes
- Features vs Vector Tiles
- SVG
- Pop-ups
- Advantages and disadvantages (inspiration [here](https://en.wikipedia.org/wiki/GIS_file_formats#Advantages_and_disadvantages))

Data sources
- Tile server
- PostGIS
- Geoserver
- CartoDB
- ArcGIS MapServer
- ??

Styling
- 

Mapping terms
- Map state: refers to the state of hte map visualization including zoom level, center or bounding box, pitch, bearing 
- Zoom to or fly to
- Pop-up
- Geocoding
- Gazetteer
- Temporal or spatiotemporal

Common tools / libraries
- Mapboxgl.js
- Leaflet.js
- Openlayers.js
- D3.js
- Turf.js

## How a typical web map works

1. Include div where map will be placed in HTML document
2. Initialize basemap. Create instance of map class - examples from Leaflet, Mapbox, etc. (Explain this uses raster tiles. <- does it also use vector tiles?). Include intial view parameters including where, zoom level etc. (Behind the scenes.)
3. Fetch and add custom layers.
4. Attach event listeners and do custom styling. 

⚠️ Asset management. Like any webpage, managing data fetched asynchronously can be tricky - especially true as map data can often be quite large. Using async await or promises helps this massively. 

## A basic web map

Code example loading raster basemap, placing vector features on top. 