# Martinez-Rueda polygon clipping algorithm [![npm version](https://badge.fury.io/js/martinez-polygon-clipping.svg)](https://badge.fury.io/js/martinez-polygon-clipping) [![CircleCI](https://circleci.com/gh/w8r/martinez.svg?style=svg)](https://circleci.com/gh/w8r/martinez)

![screenshot 2016-07-26 10 54 01](https://cloud.githubusercontent.com/assets/26884/17131796/611b3b20-531f-11e6-941c-b0f8fd385016.png)
![screenshot 2016-07-25 18 53 44](https://cloud.githubusercontent.com/assets/26884/17131805/64b74134-531f-11e6-913b-81c0cbd1a618.png)

## Details

The algorithm is specifically *fast* and *capable* of working with polygons of all types: multipolygons (without cascading),
polygons with holes, self-intersecting polygons and degenerate polygons with overlapping edges.

### Example

Play with it by [forking this Codepen](http://codepen.io/w8r/pen/rrBkER)

```js
var martinez = require('martinez-polygon-clipping');
var gj1 = { "type": "Feature", ..., "geometry": { "type": "Polygon", "coordinates": [ [ [x, y], ... ] ]};
var gj2 = { "type": "Feature", ..., "geometry": { "type": "MultiPolygon", "coordinates": [ [ [ [x, y], ...] ] ]};

var intersection = {
  "type": "Feature",
  "properties": { ... },
  "geometry": {
    "type": "Polygon",
    "coordinates": martinez.intersection(gj1.geometry.coordinates, gj2.geometry.coordinates)
  }
};
```

### API

* **`.intersection(<Geometry>, <Geometry>) => <Geometry>`**
* **`.union(<Geometry>, <Geometry>)        => <Geometry>`**
* **`.diff(<Geometry>, <Geometry>)         => <Geometry>`**
* **`.xor(<Geometry>, <Geometry>)          => <Geometry>`**

`<Geometry>` is [GeoJSON](http://geojson.org/geojson-spec.html) [`'Polygon'`](http://geojson.org/geojson-spec.html#id4) or [`'MultiPolygon'`](http://geojson.org/geojson-spec.html#id7) <u>**coordinates**</u> structure.
`<Operation>` is an enum of `{ INTERSECTION: 0, UNION: 1, DIFFERENCE: 2, XOR: 3 }` in case you have to decide programmatically
which operation do you need

### Features

The algorithm of Matrinez et al. was extended to work with multipolygons without cascading.

### Authors

* [Alexander Milevski](https://github.com/w8r/)
* [Vladimir Ovsyannikov](https://github.com/sh1ng/)

### Based on

* [A new algorithm for computing Boolean operations on polygons](http://www.sciencedirect.com/science/article/pii/S0965997813000379) (2008, 2013) by Francisco Martinez, Antonio Jesus Rueda, Francisco Ramon Feito (and its C++ code)
