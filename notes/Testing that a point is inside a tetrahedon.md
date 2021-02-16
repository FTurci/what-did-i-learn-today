---
title: Testing that a point is inside a tetrahedon
created: '2021-01-31T09:34:10.842Z'
modified: '2021-01-31T09:37:36.179Z'
---

# Testing that a point is inside a tetrahedon

One can use determinants.

Ref: http://steve.hollasch.net/cgindex/geometry/ptintet.html

Let the tetrahedron have vertices
```
        V1 = (x1, y1, z1)
        V2 = (x2, y2, z2)
        V3 = (x3, y3, z3)
        V4 = (x4, y4, z4)
```
and your test point be

        P = (x, y, z).
Then the point P is in the tetrahedron if following five determinants all have the same sign.
```
             |x1 y1 z1 1|
        D0 = |x2 y2 z2 1|
             |x3 y3 z3 1|
             |x4 y4 z4 1|

             |x  y  z  1|
        D1 = |x2 y2 z2 1|
             |x3 y3 z3 1|
             |x4 y4 z4 1|

             |x1 y1 z1 1|
        D2 = |x  y  z  1|
             |x3 y3 z3 1|
             |x4 y4 z4 1|

             |x1 y1 z1 1|
        D3 = |x2 y2 z2 1|
             |x  y  z  1|
             |x4 y4 z4 1|

             |x1 y1 z1 1|
        D4 = |x2 y2 z2 1|
             |x3 y3 z3 1|
             |x  y  z  1|
```

Some additional notes:

- If by chance the D0=0, then your tetrahedron
- is degenerate (the points are coplanar).
- If any other Di=0, then P lies on boundary i (boundary i being that boundary formed by the three points other than Vi).
- If the sign of any Di differs from that of D0 then P is outside boundary i.
- If the sign of any Di equals that of D0 then P is inside boundary i.
- If P is inside all 4 boundaries, then it is inside the tetrahedron.
- As a check, it must be that D0 = D1+D2+D3+D4.
- The pattern here should be clear; the computations can be extended to simplicies of any dimension. (The 2D and 3D case are the triangle and the tetrahedron).
- If it is meaningful to you, the quantities bi = Di/D0 are the usual barycentric coordinates.
- Comparing signs of Di and D0 is only a check that P and Vi are on the same side of boundary i.


In Python, one can use `shapely`
