# GeoJSON



### 형식



```
{ "type": "Linestring", "coordinates": [[10.0, 11.2],
[10.5, 11.9]] }
```



```
{ "type": "Feature", "geometry": { "type": "Point",
"coordinates": [10.0, 20.0] }, "properties": {
"signpost": "5", "last_check": "20200701" }
```



```
"Feature", "geometry": { "type": "Point",
"coordinates": [10.0, 5.0] }, }, { "type": "Feature",
"geometry": { "type": "LineString", "coordinates":
[[10.2, 1.0], [10.3, 2.0], [10.4, 2.5]] },
"properties": { "route": "341A7", "class": "local" } }
] }
```



1. Point
    [ ST_Point 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4133.html), [ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)

   ``` { "type": "point", "coordinates": [ 10.0, 11.2 ] }
   { "type": "point",
   "coordinates": [ 10.0,
   11.2 ] }

2. LineString
   [ ST_LineString 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4091.html), [ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)
   ` { "type": "Linestring", "coordinates": [[10.0, 11.2], [10.5, 11.9]] }`

3. Polygon
   [ ST_Polygon 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4140.html), [ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)
   ` { "type": "Polygon", "coordinates": [[[10.0, 11.2], [10.5, 11.9], [10.8, 12.0], [10.0, 11.2]]] }`

4. MultiPoint
   [ ST_MultiPoint](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4096.html) [함수, ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)
   ` { "type": "MultiPoint", "coordinates": [[10.0, 11.2], [10.5, 11.9]] )`

5. MultiLineString
   [ST_MultiLineString 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4095.html), [ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)
   ` { "type": "MultiLinestring", "coordinates": [[[10.0, 11.2], [10.5, 11.9]], [[11.0, 12.2], [11.5, 12.9], [12.0, 13.0]] }`

6. MultiPolygon
   [ST_MultiPolygon](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4097.html) [함수, ST_Geometry 함수](https://www.ibm.com/docs/ko/SSEPGG_11.5.0/com.ibm.db2.luw.spatialcol.topics.doc/doc/rsbp4057.html)
   ` { "type": "MultiPolygon", "coordinates": [[[[10.0, 11.2], [10.5, 11.9], [10.8, 12.0], [10.0, 11.2]]], [[[9.0, 11.2], [10.5, 11.9], [10.3, 13.0], [9.0, 11.2]]]] }`

7. GeometryCollection

   ` { "type": "GeometryCollection", "geometries": [ { "type": "Linestring", "coordinates": [[10.0, 11.2], [10.5, 11.9]] }, { "type": "Point", "coordinates": [10.0, 20.0] } ] }`

8. bbox
   좌표에서 계산됨.

9. coordinates
    [ longitude, latitude (, elevation)] (,)*
   ` { [1, 2] , [1, 2, 3] }`

10. Feature
    기능에는 특성이 추가된 단일 지오메트리 오브젝트가 포함되어 있습니다. 따라서 위의 지오메트리 유형에 대해 설명된 것과 같이 처리됩니다. 특성 요소 및 해당 요소가 있는 경우 'id' 요소는 무시됩니다.
    ` { "type": "Feature", "geometry": { "type": "…", "coordinates": […] "properties": […] } }`

11. FeatureCollection
     하나 이상의 기능.
    ` { "type": "FeatureCollection", "features": [ {"type": "Feature", (…) }, {"type": "Feature", (…) } ] }`