# API

## `Cupidon([_start_x], [_start_y], [_distance_h], [_distance_v], [_height], [_isometric], [_internal], [_scope])` (*constructor*)
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

































































## Curve
     The methods that will set the parabola

**Methods**
### `.simple_Parabola(_start_x, _start_y, [_distance_h], [_distance_v], [_height], [_isometric])` → *struct*
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

**Returns:** self

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

### `.apex_Height(height, [x pos], [isometric])` → *struct*
Define the top height of the parabola (vertex) with a distance. It is **NOT** the control point's height.

!> **Shouldn't be use neither with another `apex_*` method nor `apex_Point` as it will change the height calculated by those methods as well**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_apex_height` |real |The height of the parabola |
|`[_x_ratio]=0.5` |real |the x position where the vertex is positioned. |
|`[_isometric]=false` |bool |This modify the height calculation between a kind of ortho view & Isometric view. |



---

### `.apex_Height_Alt([x pos], [y pos])` → *struct*
Define the top height of the parabola (vertex) with a ratio. Isometric mode isn't supported yet.

!> **Shouldn't be use neither with another `apex_*` method nor `apex_Point` as it will change the height calculated by those methods as well**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_y_ratio]=0.5` |real |vertical ratio (0,1) to stay on the parabola, <0,1<: outside of the parabola. |
|`[_x_ratio]=0.5` |real |horizontal ratio (0,1) to stay on the parabola, <0,1<: outside of the parabola. |

### `.apex_Coord(x, y)` → *struct*
Define the top height of the parabola (vertex) with a coordinate. It is **NOT** the control point's coordinate
**Shouldn't be use neither with another `apex_*` method nor `apex_Point` as it will change the height calculated by those methods as well**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |any* |x position |
|`_y` |any* |y position |

**Returns:** self

### `.curve_Length([precision])` → *ngth*
Calculate the parabola's length (this is a slow method).

?> I discourage using it each steps

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_precision]=100` |real |the precision of the calculation. a higher value means a better precision but at a cost of performance. |

### `.curve_Length_Ext([method], [precision])` → *real*
Calculate the parabola's length using different approaches.
- 0: Approximation by summing segments.
- 1: Numerical integration (Simpson's Rule).
- 2: Analytical formula (if applicable).

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_method]=0` |real |Select the calculation method. |
|`[_precision]=100` |real |The precision level for calculation. Only if the method is set at 0 |

**Returns:** The length of the parabola.

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

### `.anchor_Motion([_on_end])` → *struct*
Update the anchor's coordinate on the parabola. This method is to be call each frame to be fully exploited.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_on_end]=false` |bool |Trigger the callback when the end of the parabola is reached. |










































































































### `.anchor_Rotate()` → *struct*
Rotate the point. Should be called in the step event.

---

### `.anchor_Orient()` → *real*
set the angle of the anchor point to the tangent of the parabola at its current position.
This method updates the angle based on the motion ratio (position), ensuring the tracker maintains a natural orientation along the parabola.

---

### `.anchor_Speed(_speed, [_motion_unit])` → *real*
the speed of the tracking point on the parabola (from the starting point to the ending point). it can be a Time, a Ratio or Steps.
The method also calculate a basic rotation_rate.

### `.rotation([_speed], [_cycle_amount], [_force_cycle])` → *bool*
calculate and set a rotation rate, and a behaviour for the rotation of the anchor point

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_speed]=rotation_rate` |real |the rotation speed. By default, it use the rotation rate calculated by the method `anchor_Speed` |
|`_cycles_amount` |real |the number of complete rotations (cycle) (-1: illimited, 0: no rotation (equal to speed = 0), 1..n: complet rotations) |
|`_force_cycle` |bool |force the anchor to sync the amount of cycle (complete rotation) to the arrival on the end point. |

**Returns:** self

### `.anchor_On_End(_callback, [_args])` → {rv}
Set a callback when the anchor reaches the end point.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`the` |allback |callback to fire |
|`arguments` |args] |for the callback. |

**Returns:** self

## Point
	 The following method allows to find or check the coordinate or orientation of any point on the curve.
	 ?> You can completely use that instead of or in parallel with the Anchor if you want. 

### `.point_Get_X(_position)` → {rv}
Get the x coordinate of a point on the prabola, at the given position.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |

**Returns:** the point's `x` value in the room

### `.point_Get_Y(_position)` → {rv}
Get the `y` value of a point on the parabola at the given `position`

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |

**Returns:** the point's `y` value in the room

### `.point_Get_Orientation(_position)` → {rv}
return the angle of a point to the tangent of the parabola at its current position.
This method return the angle based on a position, ensuring the point maintains a natural orientation along the parabola.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |




### `.point_Is_At(_position, [_single_frame])` → {rv}
Return true when the position is reached.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |
|`[_single_frame]=true` |bool |return `true` __only__ when on the single frame (true) when the position is reached (then turn back to `false`) |








### `.point_Is_At_Checkpoint(_index, [_single_frame])` → {rv}
Like `motion_Is_At` but check the position of a Checkpoint instead

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_index` |real |the index of the checkpoint in the checkpoints array to check |
|`_single_frame` |bool |only on the frame it turns true |

**Returns:** true or false
