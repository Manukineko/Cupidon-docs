# Planned Features


## TO-DO
This is a list of feature I'd like to implement in Cupidon.

**SOON** (but "time", you know ...) :

- [ ] `anchor scale` - with Animation curve support as well
- [ ] Motion looping
- [ ] Motion reverse
- [ ] lot of getters (anchor x, y, angle)
- [ ] add_Checkpoint return the checkpoint index.
- [ ] `edit_Checkpoint`
- [ ] `sort_Checkpoint`

**LATER**
- [ ] Sequence of Parabolas
- [ ] draw parabola and checkpoint with sprite.



## Description

### anchor_Scale
Allow to update a `scale` variable with the Anchor, that can be retrieve the same way than the other Anchor's variable.  
Would also support *Animation Curves* in order to animate the scale.

### Motion Looping
you would set different way of looping the anchor's motion once it reaches the end point.
*eg*: Ping-Pong, Jump, Round Trip

### Motion Reverse
Move the Anchor backward (from 1 to 0).  
That way you could use that to set a cursor on a gauge as a Speed meter or those button mashing mini-games XD

### Lot of Getters
I think it would be useful and more robust to get the public variable of the Anchor through method than through the dot noting (?) the variable itself.  
It would prevent the user to try to modify those variables directly.

### add_Checkpoint return the checkpoint index.
It would return a struct with two member : the index in the checkpoints array and the parameter itself.  
That way, a checkpoint could be store in a variable and use with the `*_checkpoint` methods

!> Oh, but it won't match if the Checkpoints array has been sorted :/

eg: 
```
myCheckpoint = trajectory.add_Checkpoint(0.5, myCallback)
trajectory.remove_Checkpoint(myCheckpoint.id)
```

### `edit_Checkpoint`
Allow to modify the parameter of a checkpoint directly.

### `sort_Checkpoint`
Sort the checkpoint in ascending or descending order

### Sequnce of Parabola
A system to queue parabolas or dynamically modify one once the Anchor reaches the end point.  
It can already be achieved but it is very ugly as you have to nest the `motion_On_End` method as a callback into another `motion_On_End` method.  


