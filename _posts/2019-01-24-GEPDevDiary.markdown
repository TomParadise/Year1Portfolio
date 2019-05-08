---
layout: post
title: Game Engine Programming Dev Diary
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
This is my developer diary for the MarioKart assignment in the Game Engine Programming Module.

#### Entry #1 - Unity 'Alpha' Post #1 ####
---
For this assignment we have been tasked with making a MarioKart-like racing game using DirectX. 
For this beginning stage, we must create a basic alpha prototype of the game in the Unity game engine.
We distributed tasks within the team, and I have chosen to create the tracks and sort out checkpoints and 
player positioning.

I have decided to create individual track pieces that can be used to form whole tracks instead of creating a single track model
or even using a model from online because one of the ideal deliverables is to implement a level editor into the final DirectX version.
Also, by using track pieces we can create multiple tracks between us within Unity instead of having to work with the troubles of Maya and
exporting to Unity.

My experience with making models in Maya for Unity is that scaling can be a big issue since shapes in Unity don't tell you their exact dimensions 
but instead their scale relative to their default size. So, I need to ensure the scale of the track is suitable for the size of the player-controlled karts.

#### Entry #2 - Unity 'Alpha' Post #2 ####
---
Since the last post, I have created the track pieces and alligned them to form a simple oval shaped track and started on checkpoints.

For the track pieces I had to go back-and-forth between Unity and Maya and keep tweaking the size until it looked appropriate but, eventually,
I reached a size that looked good. The pieces all fit together well and, in Unity, you can enable a mesh collider on models by simply adding the module
and checking a box. I imagine this will not be as easy in DirectX and I will have to create my own system for creating mesh colliders from models.

For the checkpoints, I found a video detailing how MarioKart Wii's checkpoint system works (https://youtu.be/mmJ_LT8bUj0?t=435 timestamped at checkpoint explanation) 
and how it allows for shortcuts in the track. The author of the video uses this image to explain it: 

<img src ="{{ site.baseurl }}/img/mariokartcheckpoints.png">

Essentially, there are normal checkpoints (in blue), key checkpoints (in red), and the starting line (in pink).
The blue checkpoints are used for respawning if you fall off the track, the key checkpoints are used to determine if the player has travelled around the whole track
as you must pass through all of them before the finish line to complete a lap.

In our Unity alpha implementation, I have created simple box triggers that are referenced in a script on the players. When the player passes through a trigger, 
if it's checkpoint number is 1 greater than their current stored checkpoint number then the stored number increments by 1. Once you reach the starting checkpoint again, if your current stored
checkpoint number is the maximum, it resets and increments the lap counter.

Moving forward I need to figure out how to determine the positions of each player because, currently, it will only update after you pass through a checkpoint.

#### Entry #2 - Unity 'Alpha' Post #3 ####
---
I have now fully implemented player positioning to our Unity alpha. Each update on the player, the distance between them and the next checkpoint is calculated and sent
to the race manager. Also, every time a player passes through a checkpoint, they pass their current checkpoint to the race manager. In the race manager, there are arrays for 
player checkpoints and player distances each with their respective values for each player. Each time a player's checkpoint is updated, it loops through the array of checkpoint values
and if the current checkpoint is higher and the player's position is higher (e.g. 3rd instead of 2nd) then their positions are swapped. I initially used an array for player laps 
but it was causing the nested loops to become quite large and since it compared checkpoints anyway I removed it and didn't reset the checkpoint to 0 at lap completion (e.g. if there
are 4 checkpoints in the track, after 2 laps the value would be 8). Also, when a player's distance to next checkpoints is updated, it loops through the checkpoint values and if the current checkpoint is 
higher and the player's distance is lower (i.e. closer to the next checkpoint) and their position is higher (e.g. 3rd instead of 2nd) then it swaps their positions like the previous loop but this time using 
player distance as well. I assume this is similar to how the MarioKart games determine position and it works perfectly. I initially tried incrementing and decrementing the positions of the players instead of swapping
them but encountered a bug where positions would go very high and low (into the 40s and below 0). But by swapping them, the array of positions is sorted from lowest to highest (1st position to 4th) and functions as intended.

Lastly, I implemented respawning by simply creating a trigger volume below the track so if the player falls off, their position is set to their current checkpoint and direction is set to the checkpoint's 
forward vector so they are ready to continue racing.