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

#### Post Mortem ####
---

