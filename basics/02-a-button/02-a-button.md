---
title: 02. A Button
parent: Basics
---

# 02. A Button

> Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

This example builds on the [01. A Simple Player](../01-a-simple-player/01-a-simple-player) example, and demonstrates a simple button that switches between two colors.

Start by creating a game object with a sprite in a dark brown color. Add a `CircleCollider2D` component and set **Is Trigger** to `True`.

<img src="./button-inspector.webp" srcset="./button-inspector.webp 2x" alt="Button Inspector">

Next, set the **Tag** of the player game object to `Player` (at the top of the Inspector), since we will use the tag to identify whether it is in fact the player that has entered the button's trigger. 

Create a new **Script Graph** and set up three **Graph** variables:

- `isEnabled` of type `Boolean`
- `initialColor` of type `Color`
- `isPlayerOnButton` of type `Boolean`

A `Boolean` is a type of data that can be either `true` or `false`. **Graph** variables are variables that only exist within that particular graph and cannot be accessed or modified elsewhere.

<img src="./graph-variables.webp" srcset="./graph-variables.webp 2x" alt="Graph Variables">

**On Start**, the button stores the initial color of the sprite, in order to toggle between its initial color and a "switched on" color defined in the graph.

**On Update**, the button checks whether the `Jump` button has been pressed down. If so, the `isEnabled` variable is flipped from `true` to `false` and vice-versa. Based on the value of `isEnabled`, the button either sets its "on" or "off" color that we stored in the **On Start** flow. `Jump` by default maps to the *spacebar* or the *A* button on an Xbox controller. 

Finally, the **On Trigger Enter/Exit 2D** events check if it is a game object tagged `Player` that has entered or exited the collider. If so, the `isPlayerOnButton` variable is set to `true` or `false` respectively.

[<img src="./graph.webp" srcset="./graph.webp 2x" alt="Graph">](./graph.webp)