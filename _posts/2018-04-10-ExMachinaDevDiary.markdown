---
layout: post
title: Ex Machina Dev Diary
date: 2018-12-13 09:00:00
description: Dev Diary for Ex Machina
category: LLP
published: true
tags:
  - LLP
  - Dev Diary
  - c++
---
This is my developer diary for the second game assignment in the Low Level Programming Module - Ex Machina.

#### Entry #1 ####
---
For this assignment we have been tasked with creating a game that takes an idea presented in the film - Ex
machina. We need to focus on:

<ul>
	<li>Object oriented programming</li>
	<li>Dynamic memory management</li>
	<li>Use of game frameworks</li>
	<li>Correct usage of the STL</li>
	<li>Game Scene Management</li>
</ul>

My group has pitched and started work on a top down 2D game where you play as Ava and collect and swap out various body parts, such
as arms and legs. The theme we are going with is 'what does it mean to be human?', and the genres of gameplay will be stealth/survival. So,
we plan for the levels to play out so that you hide from cameras and guards while collecting synthetic body parts to disguise yourself
and lower a detection rating for later levels. Since there are four of us in the group, we plan to make four levels: two in the Bluebook 
facility, and two in the city after you have escaped.

We all decided to work on different features of the game, and I decided to work on the player as a whole. This will include an inventory, picking up
items, the player movement, and camera movement so the camera follows the player around the level.

At this stage, we have a basic scene manager set up, many classes set up such as gameObject and player and a basic menu system. Since the last 
assignment, I feel I have greatly improved my understanding of OOP as it was previously something I struggled with, especially during my A-Level
computing course, and I am finding it easier to implement a class-based structure.

For the player movement, we wanted something similar to Hotline Miami, which is another 2D top-down game. Currently, I've implemented an acceleration
and deceration system for the player. While moving in a direction, the player accelerates up to a maximum velocity, once you stop moving in that direction,
the velocity decelerates to 0. If you are moving in opposite directions, i.e. left and right or up and down, then the velocity in that axis decelerates to 0.
This gives a smooth movement for the player but the max acceleration and rate of acceleration needs to be tweaked so that it is not floaty and the player does 
not slide too much.

For the next entry I will tweak this movement and work on camera movement.

#### Entry #2 ####
---

Due to the deadline approaching fast, I haven't updated this dev diary as much as I would have liked but at this stage I have implemented camera movement so 
that it follows the player around the level.

For the camera to follow the player it needs to move in the opposite direction the player moves in. And, for the camera to actually move, it needs to move
all gameobjects in the scene in this opposite direction.

However, if the player and the camera is moving at the same time, the player will be moving twice as fast. So, I originally planned on halving the player movement
when the camera is moving and setting the camera's max movement to half the original max, giving a resultant velocity of the original move velocity. But, this
means that you need more checks for if the player's speed is above the halved max, and you would need to remove the cap after the camera stops moving which means
the player begins accelerating again. While testing, this removed some of the smoothness of the original movement so I instead stopped the player's movement when the camera moves.
So, when the camera loops through the gameobjects, it checks that each one isnt the player before applying the movement to it so that the player stays in one place on the screen
while everything else moves around them. I also had an issue whereby the player would begin accelerating again once the camera stopped moving since the player wasnt actually moving, so
while the camera moved, the player's movement was 0 and caused the acceleration once the camera stopped. I fixed this by still calculating the player movement while the camera
moved but not applying it. So, the camera movement check is being done when the player movement is being applied instead of when it is being calculated.

Also, I only set the camera to start moving once the player reaches half way across the screen and if there is space in the level for the camera to move.

Lastly, I had to set up the camera's starting position relative to the player's starting position. So, the system I made for this considers the size of the screen and the distance
from where the camera would be if it was centred on the player to the level bounds. If the distance is negative, it adds it on to the camera pos. This way if the camera were 
to show outside the level bounds, it will instead move so that it is off-centred from the player but stays within the bounds.



#### Post Mortem ####
---

Overall, the game we created was missing many features and was not fun to play. Although we had many issues as a team working on this group project, we
still managed to create some in-depth systems that pushed the project forward. Overall, we should have tried harder to work out the internal
problems we had but going forward this is something that we can at least think about and reflect on. 

The physics I implemented for the player and camera movement worked very well and felt smooth. I am quite content with how it turned out and have improved
my programming capabilities throughout this assignment.