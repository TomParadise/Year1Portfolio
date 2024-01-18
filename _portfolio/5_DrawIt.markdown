---
layout: project
title: Draw It!
description: A VR drawing game.
img: ../img/DrawIt/DrawItThumbnail.png 
published: true
---

This project was created as a university assignment in a group of 4.

‘Draw It!’ is a reimagining of the classic game Pictionary in virtual reality for the Oculus Quest. Create 3D drawings in virtual space using intuitive motion controls, allowing for easy ‘pick up and play’ gameplay for everyone! Be immersed in mesmerising environments which alter gameplay with their dynamic word banks. Play local with one headset or online with others!

<div class="owl-carousel owl-theme">
<iframe src="https://www.youtube.com/embed/LCaSdR38KLg"></iframe>
<a href="{{ site.baseurl }}/img/DrawIt/2-flower" target="_blank"><img src="{{ site.baseurl }}/img/DrawIt/2-flower.png" /></a>
<a href="{{ site.baseurl }}/img/DrawIt/3-fire.png" target="_blank"><img src="{{ site.baseurl }}/img/DrawIt/3-fire.png" /></a>
</div>

Utilising Unity's particle system and trail renderer components we have created a system that allows players to create 3D paintings in a virtual reality play space.

In the vr environment, take control of a paint palette and brush with customisable paint colour and brush width options! Hold the trigger to draw and release to stop, and change colours by simply touching the brush to the desired colour on the palette.

Different environments provide different word bank prompts to choose from! Our dynamic word bank system provides thematic prompts relevant to the selected stage.

Levels are split into a 3 stage round system: prompt selection, drawing, and post-drawing. The active player can freely choose a prompt from the whiteboard before pressing the button and beginning the countdown for the drawing stage whereby the secondary players must correctly guess the drawing before the timer runs out! After correctly guessing, or running out of time, players can relax and view their drawing from all angles before starting the next round.