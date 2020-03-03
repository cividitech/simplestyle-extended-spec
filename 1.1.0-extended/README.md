# simplestyle-extended-spec

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in
this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## 1. Purpose

This is an extension of the simplestyle-spec to include additional geometry not
covered by the simplespec. Additionally this supports circles around a Point.

## 2. File format

`simplestyle` and hence `simplestyle-extended` is a set of agreed-upon 'special values' in
the pre-existing [GeoJSON](http://geojson.org/) data standard that
define styles. As such, files implementing `simplestyle` are by
definition valid GeoJSON files and valid [JSON](http://json.org/) files.

## 3. Client Behavior

The entirety of the spec is optional, so any combination of
specified properties are valid. When properties are not given, the defaults
below are assumed by implementations.

Multi features are assumed to have the same styling rules as single features---
MultiPoints are styled as Points, MultiPolygons as Polygons, and MultiLineStrings
as LineStrings. `marker` styles do not affect `stroke` and `fill` rules and vice versa.
The behavior of `fill` rules on LineStrings is undefined, but implementations
are encouraged to set `fill` to 0 by default in that case.

For features with a circle-radius, implementations may use the colors defined in
fill and stroke properties to style the resulting circle.

```javascript
// COLOR RULES
// Colors can be in short form:
//   "#ace"
// or long form
//   "#aaccee"
// with or without the # prefix.
// Colors are interpreted the same as in CSS,
// in #RRGGBB and #RGB order.
// But other color formats or named colors
// are not supported
{
    "type": "FeatureCollection",
    "features": [{ "type": "Feature",
        "geometry": {
            "type": "Point",
            "coordinates": [0, 0]
        },
        "properties": {
            // OPTIONAL: default ""
            // A title to show when this item is clicked or
            // hovered over
            "title": "A title",

            // OPTIONAL: default ""
            // A description to show when this item is clicked or
            // hovered over
            "description": "A description",

            // OPTIONAL: default "555555"
            // the color of a line as part of a polygon, polyline, or
            // multigeometry
            //
            // value must follow COLOR RULES
            "stroke": "#555555",

            // OPTIONAL: default 1.0
            // the opacity of the line component of a polygon, polyline, or
            // multigeometry
            //
            // value must be a floating point number greater than or equal to
            // zero and less or equal to than one
            "stroke-opacity": 1.0,

            // OPTIONAL: default 2
            // the width of the line component of a polygon, polyline, or
            // multigeometry
            //
            // value must be a floating point number greater than or equal to 0
            "stroke-width": 2,

            // OPTIONAL: default "555555"
            // the color of the interior of a polygon
            //
            // value must follow COLOR RULES
            "fill": "#555555",

            // OPTIONAL: default 0.5
            // the opacity of the interior of a polygon. Implementations
            // may choose to set this to 0 for line features.
            //
            // value must be a floating point number greater than or equal to
            // zero and less or equal to than one
            "fill-opacity": 0.5,

            // OPTIONAL
            // a radius for a circle around the coordinate of a point feature
            // Implementations may choose to use fill and stroke properties
            // to style the resulting circle object
            //
            // value must be a floating point number greater than or equal to
            // zero
            "radius": 1
        }
    }]
}
```
