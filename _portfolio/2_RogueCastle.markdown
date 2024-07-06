---
layout: project
title: Rogue Castle
description: A Procedural Tower Defense Game
img: ../img/RogueCastle/RogueCastleThumbnail.png 
published: true
---

Prepare your defenses against the skeleton siege on the castle! Place and upgrade your towers along a procedural expanding path as the waves grow more challenging each night. Can you defeat the skeleton hordes?

Rogue Castle is a procedural tower defense game I developed in Unity for WebGl play in a browser, available to play here:
<p align="center"><iframe src="https://itch.io/embed/2795390" width="552" height="167" frameborder="0"><a href="https://tomparadise.itch.io/rogue-castle">Rogue Castle - A Procedural Tower Defense Game by Tom Paradise</a></iframe></p>

I started development by implementing the procedural generation for the path to allow for junctions and long winding routes - ideal for a tower defense game! It uses a modified A* path finding algorithm on an expanding grid to generate paths of an ideal length. This is Repeated several times using the previous end point as the new start point and generating a random goal end point given range limitations and prepending or appending the grid size.
This results in a path with many twists and turns and lots of variation across outputs.

<div class="owl-carousel owl-theme">
<iframe src="https://www.youtube.com/embed/46MWv85q0og" width = "700" height="361" style="max-width:100%" data-external="1"></iframe>
<a href="{{ site.baseurl }}/img/RogueCastle/screenshot_01.png" target="_blank"><img src="{{ site.baseurl }}/img/RogueCastle/screenshot_01.png" /></a>
<a href="{{ site.baseurl }}/img/RogueCastle/screenshot_02.png" target="_blank"><img src="{{ site.baseurl }}/img/RogueCastle/screenshot_02.png" /></a>
<a href="{{ site.baseurl }}/img/RogueCastle/screenshot_03.png" target="_blank"><img src="{{ site.baseurl }}/img/RogueCastle/screenshot_03.png" /></a>
<a href="{{ site.baseurl }}/img/RogueCastle/screenshot_04.png" target="_blank"><img src="{{ site.baseurl }}/img/RogueCastle/screenshot_04.png" /></a>
<a href="{{ site.baseurl }}/img/RogueCastle/screenshot_05.png" target="_blank"><img src="{{ site.baseurl }}/img/RogueCastle/screenshot_05.png" /></a>
</div>
