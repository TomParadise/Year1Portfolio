---
layout: post
title: Rainforest Rampage Dev Diary
date: 2019-03-08 09:00:00
description: Dev Diary for Rainforest Rampage
category: Dev Diary
published: true
tags:
  - LLP
  - Dev Diary
  - c++
---
This is my developer diary for the third and final game assignment in the Low Level Programming Module - Rainforest Rampage.

#### Entry #1 ####
---

For this assignment we have been tasked with creating a digital version of the board game we have created
in the Play and Games module of our university course. It has to be programmed as an online networked game.
We can choose whether to have a peer-to-peer network or client-server network, my group has decided to create 
our game using the client-server network relationship.

For a rundown of our board game:

<ul>
	<li>The board is made up of hexagonal tiles</li>
	<li>You control an animal with lives and a score</li>
	<li>You move one tile each turn</li>
	<li>You have a target token that you must reach to gain points</li>
	<li>After moving, you draw a card from the deck</li>
	<li>The cards can be positive or negative</li>
	<li>Most card effects involve rolling a die to determine which tiles are effected</li>
	<li>Tiles start out forested and can be deforested</li>
	<li>Moving on a deforested tile deals damage</li>
	<li>If you take damage you lose a life</li>
	<li>You lose points if you are out of lives and take damage</li>
	<li>First to 200 points wins</li>
	<li>If all cards run out, the player with the most points wins</li>
</ul>

We have split the tasks up and I decided to choose to implement the cards into the game. This includes
the deck, cards, effects, interaction with players, interaction with tiles, creating and shuffling the deck.

#### Entry #2 ####
---

As I learned from the last assignment, since this is a group assignment, and since we are a small group,
any issues need to be brought up quickly. My teammate had made great progress on the online features
of the game but I had been struggling understanding it so we sat down together and went through all 
difficulties I was having. This greatly helped my understanding of how a networked game works and allowed me to
further develop my work on the game.

The way the cards work is that after the player takes a turn, the client draws a card and sends the card number to the server.
The server then decides what the client needs to do with this card, if it requires input (i.e. selecting a tile) it sends that to the client,
if not, it calculates and applies the effect of the card then sends the results to the clients.

I still need to implement some card effects and a new card we have decided to add from the feedback we received from the original board
game hand in.

#### Entry #3 ####
---
Since the last entry I have fixed and implemented all card effects including the new card design that we created from feeback for the original
board game assignment. I described it fully in detail in the Game Design Document giving the gameplay reasons why we decided to add it. Essentially,
we have made several small changes that improve the quality of life and game balance of this digital online implementation of the game compared to the physical board game.

It is quite puzzling deciding what elements of a feature need to be implemented on the client-side versus the server-side, so I had gone back and forth
with what is actually being sent to and from the server. Overall, the minimum amount of calculations should be done on the client-side so that more are processed on the server-side,
freeing up resources for the player. So, after the player moves, the server draws a card from the top of the deck and adds it to their hand. Depending on the type of card drawn, the server determines
if the player's turn ends or if they must use it. If it is card that can be used immediately, the server sends to the client that they need to select it. After selecting the card, the server determines the effect it will have.
Some cards require the player to select a specific tile, while others automatically apply their effect. There are a lot of back-and-forth interactions between the client and the server
and with this assignment being my first entry into working on a game with a client-server relationship I have struggled but learned a lot from it.

I also implemented an animation for the 'poacher' card's effect so that there is more visual feedback for the player to understand what is happening 
after the card is used. Within the HUD for the game we have a die that is rolled on screen after a card is selected. I implemented the poacher
effect after the die roll, giving a sense of progression to the impact of the card being used. I used the icon of the poacher that is used on the card
to connect the two and created a simple array of gameobjects. After the die has rolled, if the card was a poacher it sets a boolean to be true so that in the update function
of the HUD, the poacher effect is updated. The positions of the effects are also set immediately after the die has finished rolling. Depending on the type 
of poacher card (Number or Colour), and the value rolled on the die, the poacher effects' positions are set to the appropriate tiles being affected.
In each update, the opacity is increased over delta time and then decrease once fully visible, making them fade in and out. This gives a cleaner look and 
allows the player to take in what is happening as the icons fade in and out. Lastly, after a certain amount of time the boolean is set to false and they are no longer updated or rendered.

A large problem I encountered with this was due to the water tiles on the board. On specific dice rolls, the game would crash and after debugging for a long while I realised 
it was only with the number 1 dice roll. The problem was that all water tiles have a tile number of 1 as their default so it would loop through the array and try to change the transform 
for an element that is outside its bounds. Ultimately, it was a simply fix by checking if the tile was not of water type but the debugging took up a large portion of the day that could have been spent on enhancing
other features.

#### Post Mortem ####
---
Looking back at the development of this assignment, I can conclude that our group has had some severe issues regarding communication and teamwork.
As a 3 man team working on this task, with 1 member not contributing, it has been a struggle. This assignment is, without a doubt, the one I have had the most difficulty with across all modules.
As stated in a previous entry, I haven't previously worked on a networked game before but I have learned a great amount by working on this. I have also learned how other people can work at vastly different
paces to each other. since my two team members are essentially two ends of the extreme and I fall somewhere in between, I believe this has been one of the causes for the problems we have encountered while also being the 
reason we have a finished and working game.

While this assignment has been my toughest yet, I have also learned the most from it. Since the first assignment of this module, I have been improving my understanding and skills relating to object-oriented programming
and now I very confident in implemented OOP features as a standard. This project has also taught me all that I know about online networking. And while I will continually improve this, I have a good understanding of what 
should be calculated on the client-side and server-side respectively, as well as what really needs be sent between the client and server so as to reduce the amount of data being sent. So, it has been a huge learning experience for me
and I have attempted to understand and learn why some techniques are used over others and improvements to be made to my code and approach to programming. By the end of this, I am much more patient in planning before executing whereas before I 
had to just start working and build upon it and I believe this is due to my understanding and knowledge having been improved.


