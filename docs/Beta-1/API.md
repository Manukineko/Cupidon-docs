# API

## `Cupidon(_start_x = undefined, _start_y = undefined, _distance_h = 0, _distance_v = 0, _height = 0, _isometric = false, _internal = true, _scope = other)` (*constructor*)
Create a Parabola as a Quadratic Bézier Curve. The parabola has an anchor point with an x and y coordinate as well as an angle to use in order to attach an object or any thing else that can use them.
It also has methods to update the anchor position and rotation along the Parabola.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_start_x]` |real |The start point x coordinate |
|`[_start_y]` |real |The start point y coordinate |
|`[_distance_h]=0` |real |The horizontal distance to the end point |
|`[_distance_v]=0` |real |The vertical distance to the end point |
|`[_height]=0` |real |the height of the parabola |
|`[_isometric]=false` |bool |calculate the height as kind of fake isometric view. Default is orthogonal |
|`[_internal]=true` |bool |Manage all anchor's transforms calculation internally with the `anchor_Motion` method |
|`[_scope]=other` |id.instance |the scope. used internally to set the start point to the calling instance by default. |


































































**Methods**
### `.simple_Parabola(_start_x, _start_y, _distance_h, _distance_v, _height, _isometric)` → *struct*
Create a simple parabola (mimicing parametric equations) with default values

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_start_x` |real |start point coordinate |
|`_start_y` |real |end point coordinate |
|`[_distance_h]=100` |real |the horizontal distance to the end point |
|`[_distance_v]=0` |real |the vertical distance to the end point |
|`[_height]=100` |real |the height of the parabola |
|`[_isometric]=false` |bool |toogle the fake isometric calculation |

**Returns:** self

### `.start_Point(x,y)` → *struct*
Define the starting point

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |real |x position |
|`_y` |real |y position |

**Returns:** return self to allow chaining.

### `.control_Point(x,y)` → *struct*
Define the control point position (the middle point)
**Shouldn't be use neither with another `apex_*` method as it will change the height calculated by those methods as well**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |real |x position |
|`_y` |real |y position |

### `.end_Point(x,y)` → *struct*
Define the ending point

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |real |x position |
|`_y` |real |y position |

**Returns:** return self to allow chaining.

### `.end_By_Distance(horizontal, vertical)` → *struct*
Define an ending point based on a vhorizontal and vertical distance from the starting point

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_distance_h` |real |Description |
|`_distance_v` |real |Description |

### `.end_By_Direction(distance, direction)` → *struct*
Defini an ending point based on a distance and a direction (use `lengthdir` internally.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_distance` |real |a distance |
|`_direction` |real |a direction in degre |

**Returns:** self

### `.apex_Height(height, x pos, isometric)` → *struct*
Define the top height of the parabola (vertex) with a distance. It is **NOT** the control point's height.
**Shouldn't be use neither with another `apex_*` method nor `apex_Point` as it will change the height calculated by those methods as well**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_apex_height` |real |The height of the parabola |
|`[_x_ratio]=0.5` |real |the x position where the vertex is positioned. |
|`[_isometric]=false` |bool |This modify the height calculation between a kind of ortho view & Isometric view. |


