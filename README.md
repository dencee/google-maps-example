# maps

## Introduction
This is a VUE application that consumes the Google Maps API. It allows the user to drop markers across a map in either one of three ways: 

* By right clicking on the map and providing a description for the marker.
* By having an array pre-populated from an external API.
* By entering a latitude and longitude into the form.


## Project setup

Obtain a Google Maps API key from google and substitute it into the script tag within public/index.html:

```
 <script src='https://maps.googleapis.com/maps/api/js?key=GET-YOUR-OWN-KEY'></script>
 ```


From within the project:
```
npm install
npm run serve
```

## Visuals

![screenshot](https://github.com/achongsBiz/readme-files/blob/master/gmap-demo/gmap1.png)
