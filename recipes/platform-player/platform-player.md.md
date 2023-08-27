---
title: Platform Player
parent: Recipes
---

# Platform Player

> Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

A player controller for use in platform games. The script is far from production-ready, but should allow you to create some prototypes.

To prevent the player sticking to walls, a `Physics Material` has been assigned with a friction of `0`. So you need separate colliders for the top of the platform and the sides/walls.

<img src="./inspector-1x.webp" srcset="./inspector-1x.webp 1x, ./inspector-2x.webp 2x">

Some of the values in the graph will need to be tweaked to fit your character. For example the `Physics: Sphere Cast` radius.

<img src="./variables-1x.webp" srcset="./variables-1x.webp 1x, ./variables-2x.webp 2x">

<img src="./graph-1x.webp" srcset="./graph-1x.webp 1x, ./graph-2x.webp 2x">