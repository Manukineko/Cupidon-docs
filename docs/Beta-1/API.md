# API

## `Cupidon(_start_x, _start_y, _distance_h, _distance_v, _height, _isometric, _internal, _scope)` (*constructor*)
Create a Parabola as a Quadratic B�zier Curve. The parabola has an anchor point with an x and y coordinate as well as an angle to use in order to attach an object or any thing else that can use them.
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


## Curve

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

## Anchor

The Anchor is a point whose coordinate are stored in the `x` and `y` variable.
 They are automatically updated when calling `anchor_Motion` and you retrieve those like this:
```gml
 // Instance step event
 x = myCupidon.x
 y = myCupidon.y
```

### `.anchor_Set(position)` → *struct*
Set the internal point's `x` and `y` on the parabola.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |
