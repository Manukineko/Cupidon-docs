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




































































## Parabola
The methods that will set the parabola parameters.
The default use case is to have those called in the create event or on an event (mouse click, jump) to set the curve once.  
However, you could also call them each steps to update your Parabola in-real time (eg: trajetory of an arrow based on a power, etc)

it just needs a start point, an end point and a control point to have a functioning parabola, but several other alternatives methods are available, especially to define an end point base on distance or to directly set the [vertex](#) position of the curve

---




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

!> **This method can't be use with the `apex_*` methods as those will fight to set the vertex coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |real |x position |
|`_y` |real |y position |

### `.end_Point(x,y)` → *struct*
Define the ending point.

!> **This method can't be use with the `end_By_*` methods as they will fight to set the end point coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_x` |real |x position |
|`_y` |real |y position |

**Returns:** return self to allow chaining.

### `.end_By_Distance(horizontal, vertical)` → *struct*
Define an ending point based on a vhorizontal and vertical distance from the starting point

!> **This method can't be use with the others `end_By_*` or the `end_point` method as they will fight to set the end point coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_distance_h` |real |Description |
|`_distance_v` |real |Description |

### `.end_By_Direction(distance, direction)` → *struct*
Defini an ending point based on a distance and a direction (use `lengthdir` internally.

!> **This method can't be use with the others `end_By_*` or the `end_point` method as they will fight to set the end point coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_distance` |real |a distance |
|`_direction` |real |a direction in degre |

**Returns:** self

### `.apex_Height(height, [x pos], [isometric])` → *struct*
Define the top height of the parabola (vertex) with a distance. It is **NOT** the control point's height.

!> **This method can't be use with others `apex_*` or the `control_point` method as they will fight to set the vertex coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_apex_height` |real |The height of the parabola |
|`[_x_ratio]=0.5` |real |the x position where the vertex is positioned. |
|`[_isometric]=false` |bool |This modify the height calculation between a kind of ortho view & Isometric view. |



---

### `.apex_Height_Alt([x pos], [y pos])` → *struct*
Define the top height of the parabola (vertex) with a ratio. Isometric mode isn't supported yet.

!> **This method can't be use with others `apex_*` or the `control_point` method as they will fight to set the vertex coordinate**

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_y_ratio]=0.5` |real |vertical ratio (0,1) to stay on the parabola, <0,1<: outside of the parabola. |
|`[_x_ratio]=0.5` |real |horizontal ratio (0,1) to stay on the parabola, <0,1<: outside of the parabola. |

### `.apex_Coord(x, y)` → *struct*
Define the top height of the parabola (vertex) with a coordinate. It is **NOT** the control point's coordinate

!> **This method can't be use with others `apex_*` or the `control_point` method as they will fight to set the vertex coordinate**

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

## Point

The following method allows to find or check the coordinate or orientation of any point on the curve.

?> You can completely use that instead of or in parallel with the Anchor if you want. 

---



### `.point_Get_X(_position)` → *real*
Get the x coordinate of a point on the prabola, at the given position.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |

**Returns:** the point's `x` value in the room

### `.point_Get_Y(_position)` → *real*
Get the `y` value of a point on the parabola at the given `position`

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |

**Returns:** the point's `y` value in the room

### `.point_Get_Orientation(_position)` → *bool*
return the angle of a point to the tangent of the parabola at its current position.
This method return the angle based on a position, ensuring the point maintains a natural orientation along the parabola.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |




### `.point_Is_At(_position, [_single_frame])` → *struct*
Return true when the position is reached.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |
|`[_single_frame]=true` |bool |return `true` __only__ when on the single frame (true) when the position is reached (then turn back to `false`) |








### `.point_Is_At_Checkpoint(_index, [_single_frame])` → *struct*
Like `motion_Is_At` but check the position of a Checkpoint instead

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_index` |real |the index of the checkpoint in the checkpoints array to check |
|`_single_frame` |bool |only on the frame it turns true |

**Returns:** true or false

## Anchor

The Anchor is a point whose coordinate and angle are stored in Cupidon's internal `x`, `y`and `angle` variables.

They are automatically updated when calling `anchor_Motion` and you retrieve those like this:

```gml
    // Instance step event
    x = myCupidon.x
    y = myCupidon.y
```

---



### Setters

Methods that will set several parameters use by the Updaters methods to update the Anchor.
Those are to be called in the create event or on an event once.


---



### `.anchor_Set(_position)` → *struct*
Set the anchor's coordinate `x` and `y` at the given poisiton on the parabola.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_position` |real |the position on the parabola. Between 0 (start point) and 1 (end point). A negative value is before the start point and a value superior to 1 is after the end point. |


---



### `.anchor_Speed(_speed, [_motion_unit])` → *lf*
the speed of the tracking point on the parabola (from the starting point to the ending point). it can be a Time, a Ratio or Steps.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_speed` |real |time: in second, ratio: percentage by steps between [0, 100], steps: gamemaker's steps |
|`[_motion_unit]="unit_time"` |string |The type of unit of the speed value set. |


























---



### `.anchor_Rotation([_speed], [_cycle_amount], [_force_cycle])` → *struct*
Calculate and set a rotation rate, and a behaviour for the rotation of the anchor point. Need to be called somewhere if rotation are handle internally.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_speed]=rotation_rate_default` |real |the rotation speed as an angle. By default, it use a rotation rate calculated for one full rotation per second |
|`_cycles_amount` |real |the number of complete rotations (cycle) (-1: illimited, 0: no rotation (equal to speed = 0), 1..n: complet rotations) |
|`_force_cycle` |bool |force the anchor to sync the amount of cycle (complete rotation) to the arrival on the end point. It will completely bypass the `_speed` if `cycle_amount` is above `0`. |

**Returns:** self


---



### `.anchor_On_End(_callback, [_args])` → {rv}
Set a callback when the anchor reaches the end point.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`the` |allback |callback to fire |
|`arguments` |args] |for the callback. |

**Returns:** self

### Updaters

Methods that update the Anchor's transforms. They should be call each steps.

---



### `.anchor_Motion([_on_end])` → {rv}
The main method. it update the anchor's coordinate on the parabola, but also ist roation or orientation, and its scale when `motion_Internal_Transform` is set to `true`

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_on_end]=false` |bool |Trigger the callback when the end of the parabola is reached. |


















































































































---



### `.anchor_Rotate()` → {rv}
Rotate the Anchor. Need to be called each steps if rotation are handle externally and is bypassed if handle internally.
If `anchor_Rotation` isn't called upstream, the method assumes that the Anchor point want to be rotated and thus, will force a default rotation rate of one cycle per second.

!> **This method can't be use with `anchor_Orient` as both will fight to update the `angle` variable.**


---



### `.anchor_Orient()` → {rv}
set the angle of the anchor point to the tangent of the parabola at its current position.
This method updates the angle based on the motion ratio (position), ensuring the Anchor maintains a natural orientation along the parabola.
Need to be called each steps if `motion_Internal_Transform` is `false`.

!>	**This method can't be use with `anchor_Rotate` as both will fight to update the `angle` variable.**


---



### Motion
Those methods relate to all motion behaviour regarding the Anchor.  
you can control the Anchor's , well ... motion on the parabola when `anchor_Motion` is used, basically like using a media player, with Play, Pause, etc, but also set an *Animation Curves* to smoothly animate the anchor's progress on the parabola.

---



### `.motion_Play()` → {rv}
start the anchor. Can be use to resume as well.


---



### `.motion_Pause()` → {rv}
Pause the tracking point.


---



### `.motion_Reset()` → {rv}
Stop the tracking point. it will goes back to the start of the parabola.


---



### `.motion_Resume()` → {rv}
Resume the tracking point (from the pause state).


---



### `.motion_Toggle_Pause()` → {rv}
Toggle between pause and resume.


---



### `.motion_Set_AnimCurve(_animcurve)` → {rv}
Set an Animation Curves to be use as the position on the parabola

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_animcurve` |Asset.GMAnimCurve |theAnimation Curve to use |























---



### `.motion_Internal_Transforms(_internal)` → {rv}
Set the global behaviour for handling the anchor transformation rotate and scale.
It manages if those transformations should be handle internally by the `anchor_Motion` method or with their dedicated methods (eg: `anchor_Rotate`).

?> `anchor_Scale` is a **planned feature**.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_internal` |bool |true for internal, false for external |







## Checkpoints

Checkpoints is a feature that allows to define different position on the parabola that, once reached by the Anchor
can trigger a callback. They are like an anchor targeted and automated version of the method `point_Is_At`.  
There are optional parameters to manage a checkpoint's behaviour.

---




### `.add_Checkpoint(_position, [_callback], [_args], [_single_frame], [_once], [_sort])` → {rv}
Add a checkpoint to the parabola's checkpoints array.


---




---



### `.remove_Checkpoints_All()` → {rv}
Remove all the checkpoints from the checkpoints array.


---




---



### `.edit_Checkpoint(index or ref, variable or struct)` → {rv}
?> Planned Feature - see Roadmap


---



### `.sort_Checkpoints(sorting)` → {rv}
?> Planned Feature - see Roadmap


---



## Drawing

You can draw the parabola with the start and end point with a color, but also any or all checkpoints (if set).  
However, that is really basic and I guess you would want to use your own implementation, using the `point_Get_*` methods.  


### `.draw([_point_number], [_start_color], [_end_color], [_color1], [_color2])` → {rv}
draw the parabola as a line of points.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_point_number]=16` |real |the number of point that formed the parabola |
|`[_start_color]=c_red` |Constant.Color |The start point color |
|`[_end_color]=c_red` |Constant.Color |The end point color |
|`[_color1]=c_white` |Constant.Color |The first gradient color for the parabola's points |
|`[_color2]=c_white` |Constant.Color |The second gradient color for the parabola's points |


---



### `.draw_Checkpoint([_index], [_color], [_size], [_outline])` → {rv}
Draw one or all checkpoint on the parabola as a diamond shape

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`[_index]=all` |real,Constant.All |the checkpoint to draw |
|`[_color]=c_green` |Constant.Color |the chckpoint color |
|`[_size]=6` |real |the size of the shape the size of the diamond shape |
|`[_outline]=false` |bool |outline (true) or fill (false) |

**Returns:** self


---



### `.draw_Debug([_seg], [_curve_color])` → {rv}
Draw a debug representation of the parabola.
it will draw the parabola as points linked by a line, the line between the start and end point, the start point, the end point, the controle point and the vertex point.

| Parameter | Datatype  | Purpose |
|-----------|-----------|---------|
|`_seg` |real |number of segment of the line representing the parabola. Higher value is more precise but also mor expensive. |




























