<h1 align = "center"> cUpido∩ </h1>
<p align = "center">
<!--img src = "https://i.imgur.com/m255R2h.png" /> <br-->
A small library to create trajectories with Quadratic Bezier Curves that loves you.<br><br>
Download the lastest version <a href = "https://github.com/manukineko/Cupidon/releases">here</a>
</p>

<div class="tip">
  <p>Cupidon is quite usable but still in very Beta, with probable bugs and a lot of typos as I have yet :</p>
  <ul>
  <li>extendly tested it in context in my own game project</li>
  <li>find a way to switch my brain to english when you are an old french guy living in Japan.</li>
  </ul>
  <p>I am also all hears about methods and features naming or logic improvements as I'm also yet :</p>
  <ul>
  <li>to become as a skilled programmer as everyone else on the <a href = "https://discord.com/invite/RDYyRqBswD">Gamemaker Kitchen</a>'s discord 😭.</li>
  </ul>
</div>

## What is Cupidon
I was quite frustrated when I wanted an object to follow a simple trajectory, without the hustle of using ballistic maths or physics.  
I just wanted a nice reusable parabola, with predictable and controlable parameter to know where it starts, where it ends and how it would behave.

Cupidon's parabola are just Quadratic Bézier Curves with some wistles.

This library allows you to create such a **parabola** and its main use case is to assign the values of its built-in **anchor point** to anything that can use a coordinate and/or an angle (an object, an instance, a constructor, a sprite).  
You put the `anchor_motion` methods to be updated at each step in your code, and it will update the anchor's value, which you just have to get and assign to that "anything" thing to be updated accordingly, like this :

```gml
// attached object step event or where you want
x = myParabola.x
y = myParabola.y
image_angle = myParabola.angle
```

A parabola (well, a Quadratic Bézier Curve) needs three point : a tart point, an end point and a control point between the two and which would define the "shape" of the curve.
Severals methods are available to define thoses points in differents ways.

## What are the Features

- Create a Quadratic Bé zier Curve easily
- Built-in Anchor point
	- attach anything that can use a coordinate or/and an angle to it.
- Anchor point's motion
	- manage rotation and orientation internally.
	- set its position on the Parabola manually
- Move the anchor point along the parabola
	- time the movement to a duration
	- stop on the end point
- Rotate the anchor point
	- Sync the rotation to a number of rotation
- Orient the Anchor point to the parabola (think "arrow" or "rocket" XD)
- Use an Animation Curve to animate the Anchor's motion
- Fire a callback whent the Anchor reaches the end point
- Checkpoints - set one or more checkpoints along the Parabola
	- fire a callback when reached by the Anchor point
	- fire once or/and only on a single frame
- get any point's coordinate from a position on the Parabola
	- manage a second anchor point manually
- check an arbitrary position on the Parabola or a checkpoint's to execute additional code manually when reached by the Anchor point.
- Draw the Parabola and its points
	- draw the checkpoints too !
	
## What does Cupidon mean ?

I first wanted to call that library "Bisou" (kiss) to refere to those "airkiss" in mangas and comics with a small heart shape describing a small parabola.  
But then I was thinking about a more straight forward "Archer", because Bow and Arrow describe perfectly what is a parabola and what is the main purpose of that library.  

That's how I got an epiphany with the name Cupidon.

> **Cupidon** is the french name of [Cupid](https://en.wikipedia.org/wiki/Cupid), the small god of love and desire in the Roman mythology, and often portrayed as an archer.

You can say that I've killed two lovebirds with one arrow (🥁)

And in japanese "don" can be referred to the sound of something hitting something else.  

As for the way I have written "Cupidon" that way in the title, the lowercase `c` refer to how I prefix my asset in Gamemaker with the capital `U` that follows matching the camelCase convention. The final `n` is the "intersection" math symbol and, both with the capital `U` is a perfect representation of a ... Parabola.

