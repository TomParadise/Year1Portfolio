---
layout: post
title: Game Engine Programming DirectX Dev Diary
date: 2019-01-24 09:00:00
description: Dev Diary for Game Engine Programming
category: Dev Diary
published: true
tags:
  - GEP
  - Dev Diary
  - c++
  - DirectX
---
This is my developer diary for the DirectX implementation of the MarioKart assignment in the Game Engine Programming Module.

#### Entry #1 - Physics beginning ####
---

We have now been been tasked with implementing game engine features for the MarioKart game in DirectX and it has been revealed we are
using DirectX 12. In our group, we have redistributed elements that each member will undertake and I have chosen the game's physics.
I have no experience with DirectX going into this but I know there are many useful library files when it comes to game physics such as 
Math.h and BoundingBox.h.

The first thing I decided to implement is giving simple axis-alligned bounding boxes to 3D gameObjects that require collisions. So, I modified
gameObject 3D to create a bounding box for the object if the collision boolean is true. The size of the bounding box is also set relative to the scale 
of the object and for players, the centre is updated each tick to match the objects position.

#### Entry #2 - Collisions ####
---

The way I planned to do collisions is to check after each update of the player's movement if they are colliding with an object and to bounce them 
away at the correct angle. So, since the players need access to all gameobjects, I pass the vector of objects to them during initialisation in the gameplay scene.
After the player's movement updates each tick in the PhysModel class, it loops through the vector and checks if either bounding box is colliding. If they are,
the normal to the collision is calculated and the reflected movement vector is determined and applied. Calculating the collision normal took me a considerable 
amount of time to figure out and I finally sorted it out by finding this image: <img src ="{{ site.baseurl }}/img/collisionNormal.png"> and a 2-Dimensional 
implementation from the answer on this post: https://gamedev.stackexchange.com/questions/136073/how-does-one-calculate-the-surface-normal-in-2d-collisions .
