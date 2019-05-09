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
amount of time to figure out and I finally sorted it out by finding this image: 
<img src ="{{ site.baseurl }}/img/collisionNormal.png"> 
and a 2-Dimensional implementation from the answer on this post: https://gamedev.stackexchange.com/questions/136073/how-does-one-calculate-the-surface-normal-in-2d-collisions
. The answer does not explain how to calculate the orthogonal unit vectors Ux and Uy but I determined they are distance vectors from the source to the edge of the colliding object, 
in the direction closest to the player.

After finding the collision normal, the resultant velocity is calculated and the position updated.


#### Entry #3 - Checkpoints ####
---

For checkpoints, I plan to create a similar system to the Unity implementation with checkpoint collision boxes and a 'checkpoint manager' attached to each player
that tracks their current checkpoint and updates the distance to the next one for positioning. I have already created the checkpoint and checkpoint manager classes
so all that is needed are the checkpoint positions. In the player physmodel class, I added a check to the collided bounding box to see if it is a checkpoint and if it is to 
check if it is the next checkpoint for the player to pass through. Each player has a checkpoint manager attached and this deals with checking for this.

Also in the player physmodel, each update, the distance to the next checkpoint is calculated and sent to the race_manager, like in the Unity implementation, and player positions
are updated.


#### Entry #4 - Mesh Colliders Attempt ####
---

I had originally planned to implement a mesh collider sysmem for tracks so that the collider would be automatic and allow for full models to be imported and used immediately.
But, I have decided to give up on this due to time limitations and issues with DirectX and visual studio on my home PC preventing me from using the debug build option (despite it working
on the University lab PCs).

I have a fair understanding of how I wanted to create a mesh collider: 
<ul>
	<li>Models consist of many meshes</li>
	<li>Meshes consist of many mesh parts</li>
	<li>Mesh parts contain meta data associated with the model's vertices</li>
</ul>
<img src ="{{ site.baseurl }}/img/meshcollider.png"> 

Here is a piece of code that iterates through the model's meshes and mesh parts. It also checks that they are not null pointers. My goal was to store the vertices in a matrix and 
triangulate between them to create a collider with many triangular faces. But, I do not have enough experience to do this and due to the lack of time and lack of track collisions,
have decided to drop mesh colliders and move on to another idea.

#### Entry #4 - Track Collisions ####
---

Since mesh collisions were dropped, I have decided the next best way to implement track collisions is to break up the track into individual pieces and map bounding boxes onto each piece.
So, We can use a few track piece models, such as a straight piece and a corner piece, and place multiple together to form a track. Once my team member creates the models, I can set the values 
for the bounding box extents and add gravity (reduce y value) to the players so that you collide with and can fall off the track.

#### Entry #5 - Finished Track Collisions & AI ####
---

The track bounding boxes are in place and gravity has been added, this also meant I could add the respawn mechanic from the Unity implementation if the player's y value drops below the track.
Ideally, we would use a collision volume where if collided, the player would respawn at their previous checkpoint, but since we have a flat track, we can just check if the y value falls below 
a certain point.

I decided to work on implementing a basic AI to the game since my team member didn't create one of value and was severely hard coded. So, I created a bot that finds the direction to the next checkpoint
and rotates until it is facing within a certain range of that direction, then it accelerates towards it and rotates to face the next checkpoint upon reaching it. This allows it to move around any created track
without requiring any hard coded positions. Moving forward with this I would I add some variance to the movements so that the AI is less predictable and allows for multiple at once.