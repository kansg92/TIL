

# Polygon



GeoJSON에서 따르는 표준 구조



배열의 깊이는 총 최대 4중배열(Multi Polygon)으로 구성되어있다.

| 배열 깊이 | 의미                                         |
| --------- | -------------------------------------------- |
| `1차원`   | 도형 1개일 때 단일 점 (Point: `[x, y]`)      |
| `2차원`   | 선(LineString: `[[x, y], [x, y], ...]`)      |
| `3차원`   | 다각형(Polygon): 외곽선 + 구멍               |
| `4차원`   | 멀티 폴리곤(MultiPolygon): 여러 Polygon 모음 |



### 폴리곤의 구성요소

| 구성 요소    | 설명                                                |
| ------------ | --------------------------------------------------- |
| `shell`      | 외곽선 (Polygon의 테두리)                           |
| `holes`      | 내부에 뚫린 영역들. 면적 계산 시 제외됨             |
| 면적 `.area` | 외곽 면적에서 구멍들 면적 자동 차감됨 shell - holes |

정확한 폴리곤의 면적을 구하려면 shell 면적과 holes 면적을 구한구 shell - holes를 해주어야함



예시 코드 (EPSG 변환 포함)



```python
from pyproj import Transformer

# EPSG:900913 → EPSG:5186 변환기
transformer = Transformer.from_crs("EPSG:900913", "EPSG:5186", always_xy=True)

# WFS에서 받은 MultiPolygon 좌표 예시
coords_900913 = [
  [  # Polygon 1
    [ [14135000, 4511100], [14135100, 4511100], [14135100, 4511200], [14135000, 4511200], [14135000, 4511100] ]
  ],
  [  # Polygon 2
    [ [14135200, 4511300], [14135300, 4511300], [14135300, 4511400], [14135200, 4511400], [14135200, 4511300] ]
  ]
]

# 변환된 Polygon 리스트
polygons = []
for polygon_coords in coords_900913:
    # polygon_coords는: [exterior, hole1, hole2, ...]
    exterior = [transformer.transform(x, y) for x, y in polygon_coords[0]]
    holes = [ [transformer.transform(x, y) for x, y in hole] for hole in polygon_coords[1:] ]
    poly = Polygon(shell=exterior, holes=holes if holes else None)
    polygons.append(poly)

# MultiPolygon 생성 및 면적 계산
multi = MultiPolygon(polygons)
print("전체 면적 (㎡):", round(multi.area, 2))
```





Multi Polygon인경우

```python
for polygon_coords in r_it['geometry']['coordinates'] :
    exterior = [transformer.transform(x, y) for x, y in polygon_coords[0]]
    holes = [ [transformer.transform(x, y) for x, y in hole] for hole in polygon_coords[1:] ]
    poly = shapely.Polygon(shell=exterior, holes=holes if holes else None)
    polygons.append(poly)
multi = shapely.MultiPolygon(polygons)
intersection = multi.intersection(land)
ucode['area'] = round(intersection.area, 2)
```

