---
title: Platform Player
parent: Recipes
---

# Platform Player

> Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

<video autoplay loop muted playsinline>
	<source src="./demo.mp4" type="video/mp4">
</video>

Download the graph: [PlatformPlayer.asset](./PlatformPlayer.asset)

A minimal player controller script for simple platforming. It supports walking on slopes and jumping.

Most of the complexity in this graph comes from better handling slope movement and jumping. It is possible to extract some more simple ideas from this graph, like how to orient the game controller input to the camera.

However, I think this can serve as a decent starting point for building your own player controller.

## Player setup

The player is set up with a `Capsule Collider` and a `Rigidbody`. Freeze Rotation is enabled on all three axes. For smoother movement, interpolation is enabled as well.

<img src="./player-1x.webp" srcset="./player-1x.webp 1x, ./player-2x.webp 2x">

## Variables

A few variables are used to store the current state of the player controller. An important note is that the player will only be considered grounded on objects that match the `groundLayer` - this can be set to multiple layers, but I do recommend to separate at least walls and ground.

<img src="./variables-1x.webp" srcset="./variables-1x.webp 1x, ./variables-2x.webp 2x">

## Graph

I have separated the graph into three images, though they are all part of the same script graph.

### On Start

<img src="./graph-start-1x.webp" srcset="./graph-start-1x.webp 1x, ./graph-start-2x.webp 2x">

### On Update

<img src="./graph-update-1x.webp" srcset="./graph-update-1x.webp 1x, ./graph-update-2x.webp 2x">

### On Fixed Update

In order to calculate the slope direction in accordance with the game controller input, we need to perform a number of steps.

1. Create a vector from the controller input and clamp it to `1.0`.
2. Rotate the input around the Y-axis to match the camera's view.
3. Get the ground's normal vector from the raycast.
4. Calculate a direction along the ground/slope that keeps the XZ-direction but modifies Y. For this, we can use this equation: <br><img src="./equation.svg">
5. Normalize the direction and use the input magnitude and `moveSpeed` to determine to velocity along the ground.

<img src="./graph-fixed-update-1x.webp" srcset="./graph-fixed-update-1x.webp 1x, ./graph-fixed-update-2x.webp 2x">
