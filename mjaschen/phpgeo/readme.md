# phpgeo - A Simple Geo Library for PHP

phpgeo provides abstractions to geographical coordinates (including support for different ellipsoids) and allows you to calculate geographical distances between coordinates with high precision.

[![License](https://poser.pugx.org/mjaschen/phpgeo/license)](//packagist.org/packages/mjaschen/phpgeo)

## License

Starting with version 2.0.0 phpgeo is licensed under the MIT license. Older versions were GPL-licensed.

## Examples/Usage

This list is incomplete, please visit the [documentation site](https://phpgeo.marcusjaschen.de/)
for the full monty of documentation and examples!

### Distance between two coordinates (Vincenty's Formula)

Use the calculator object directly:

```c#
var coordinate1 = new Coordinate(19.820664, -155.468066); // Mauna Kea Summit
var coordinate2 = new Coordinate(20.709722, -156.253333); // Haleakala Summit

var calculator = new Vincenty();

Console.WriteLine(calculator.getDistance(coordinate1, coordinate2)); // returns 128130.850 (meters; ≈128 kilometers)
```

or call the `getDistance()` method of a Coordinate object by injecting a calculator object:

```c#
var coordinate1 = new Coordinate(19.820664, -155.468066); // Mauna Kea Summit
var coordinate2 = new Coordinate(20.709722, -156.253333); // Haleakala Summit

Console.WriteLine(coordinate1.getDistance(coordinate2, new Vincenty()); // returns 128130.850 (meters; ≈128 kilometers)
```

### Simplifying a polyline

Polylines can be simplified to save storage space or bandwidth. Simplification is done with the [Ramer–Douglas–Peucker algorithm](https://en.wikipedia.org/wiki/Ramer–Douglas–Peucker_algorithm) (AKA Douglas-Peucker algorithm).

```c#
var polyline = new Polyline();
polyline.addPoint(new Coordinate(10.0, 10.0));
polyline.addPoint(new Coordinate(20.0, 20.0));
polyline.addPoint(new Coordinate(30.0, 10.0));

var processor = new SimplifyBearing(1500000);

// remove all points which perpendicular distance is less
// than 1500 km from the surrounding points.
var simplified = processor.simplify(polyline);

// simplified is the polyline without the second point (which
// perpendicular distance is ~1046 km and therefore below
// the simplification threshold)
```

### Polygon contains a point (e.g. "GPS geofence")

phpgeo has a polygon implementation which can be used to determinate if a point is contained in it or not.
A polygon consists of at least three points. Points are instances of the `Coordinate` class.

**Warning:** The calculation gives wrong results if the polygons has points on both sides of the 180/-180 degrees meridian.

```c#
var geofence = new Polygon();

geofence.addPoint(new Coordinate(-12.085870,-77.016261));
geofence.addPoint(new Coordinate(-12.086373,-77.033813));
geofence.addPoint(new Coordinate(-12.102823,-77.030938));
geofence.addPoint(new Coordinate(-12.098669,-77.006476));

var outsidePoint = new Coordinate(-12.075452, -76.985079);
var insidePoint = new Coordinate(-12.092542, -77.021540);

Console.WriteLine((bool)geofence.contains(outsidePoint)); // returns bool(false) the point is outside the polygon
Console.WriteLine((bool)geofence.contains(insidePoint)); // returns bool(true) the point is inside the polygon
```

### Formatted output of coordinates

You can format a coordinate in different styles.

#### Decimal Degrees

```c#
var coordinate = new Coordinate(19.820664, -155.468066); // Mauna Kea Summit

Console.WriteLine(coordinate.format(new DecimalDegrees()).ToString());
```

#### Degrees/Minutes/Seconds (DMS)

```c#
var coordinate = new Coordinate(18.911306, -155.678268); // South Point, HI, USA

var formatter = new DMS();

Console.WriteLine(coordinate.format(formatter).ToString()); // 18° 54′ 41″ -155° 40′ 42″

formatter
    .setSeparator(", ")
    .useCardinalLetters(true)
    .setUnits(DMS.UNITS_ASCII);

Console.WriteLine(coordinate.format(formatter).ToString()); // 18° 54' 41" N, 155° 40' 42" W
```

#### GeoJSON

```c#
var coordinate = new Coordinate(18.911306, -155.678268); // South Point, HI, USA

Console.WriteLine(coordinate.format(new GeoJSON()).ToString()); // { "type" : "point" , "coordinates" : [ -155.678268, 18.911306 ] }
```


## Features

**Info:** Please visit the **[documentation site](https://phpgeo.marcusjaschen.de/)** for complete and up-to-date documentation with many examples!

phpgeo provides the following features (follow the links for examples):

- abstractions of several geometry objects ([coordinate/point](https://phpgeo.marcusjaschen.de/Geometries/Coordinate.html),
  [line](https://phpgeo.marcusjaschen.de/Geometries/Line.html),
  [polyline/GPS track](https://phpgeo.marcusjaschen.de/Geometries/Polyline.html),
  [polygon](https://phpgeo.marcusjaschen.de/Geometries/Polygon.html)
- support for different [ellipsoids](https://phpgeo.marcusjaschen.de/Geometries/Ellipsoid.html), e.g. WGS-84
- [length/distance/perimeter calculations](https://phpgeo.marcusjaschen.de/Calculations/Distance_and_Length.html)
  with different implementations (Haversine, Vincenty)
- [Geofence](https://phpgeo.marcusjaschen.de/Calculations/Geofence.html) calculation,
  i. e. answering the question "Is this point contained in that area/polygon?"
- [formatting and output](https://phpgeo.marcusjaschen.de/Formatting_and_Output/index.html) of geometry objects
  (GeoJSON, nice strings, e. g. `18° 54′ 41″ -155° 40′ 42″`)
- calculation of [bearing angle between two points](https://phpgeo.marcusjaschen.de/Calculations/Bearing_and_Destination.html#page_Bearing-between-two-points)
  (spherical or with Vincenty's formula)
- calculation of a [destination point for a given starting point](https://phpgeo.marcusjaschen.de/Calculations/Bearing_and_Destination.html#page_Destination-point-for-given-bearing-and-distance),
  bearing angle, and distance (spherical or with Vincenty's formula)
- calculation of the [perpendicular distance between a point and a line](https://phpgeo.marcusjaschen.de/Calculations/Perpendicular_Distance.html)
- calculation of the [Cardinal Distances between two points](https://phpgeo.marcusjaschen.de/Calculations/Cardinal_Distance.html)
- getting segments of a [polyline](https://phpgeo.marcusjaschen.de/Geometries/Polyline.html#page_Segments)
  /[polygon](https://phpgeo.marcusjaschen.de/Geometries/Polygon.html#page_Segments),
- [reversing direction](https://phpgeo.marcusjaschen.de/Geometries/Polygon.html#page_Reverse-Direction)
  of polyline/polygon

## Miscellaneous

[@clemdesign](https://github.com/clemdesign) created a [TypeScript port](https://github.com/clemdesign/typescript-tsgeo) of phpgeo.

## Credits

* Marcus Jaschen <mail@marcusjaschen.de>
* [Chris Veness](http://www.movable-type.co.uk/scripts/latlong-vincenty.html) - JavaScript implementation of the [Vincenty formula](http://en.wikipedia.org/wiki/Vincenty%27s_formulae) for distance calculation
* Ersts,P.J., Horning, N., and M. Polin[Internet] Perpendicular Distance Calculator(version 1.2.2) [Documentation](http://biodiversityinformatics.amnh.org/open_source/pdc/documentation.php). American Museum of Natural History, Center for Biodiversity and Conservation. Available from http://biodiversityinformatics.amnh.org/open_source/pdc. Accessed on 2013-07-07.
* W. Randolph Franklin, PNPOLY - Point Inclusion in Polygon Test [Documentation](http://www.ecse.rpi.edu/Homepages/wrf/Research/Short_Notes/pnpoly.html)
* [Richard Barnes](https://github.com/r-barnes) Polyline GeoJSON Formatter
* [Paul Vidal](https://github.com/paulvl) Polygon Implementation

[Psalm]: https://github.com/vimeo/psalm