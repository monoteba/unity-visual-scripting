---
title: 01. A Simple Player
parent: Basics
---

# 01. A Simple Player

Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

This example demonstrates a simple 2D player character that can be moved up, down, left and right. The player is using a rigid body so that it can collide with walls and other objects.

Start by creating a new GameObject with a `Rigidbody2D` and `BoxCollider2D` component. 

On the `Rigidbody2D` set...

- **Body Type** to `Dynamic`
- **Gravity Scale** to `0`
- **Interpolate** to `Interpolate`
- **Freeze Rotation** to `True` (ticked on)

![Player Inspector](./player-inspector.jpg)

Create a new **Script Graph** with an **Object** variable[^1] named `moveSpeed` of type `Float` with an initial value of `3.0`. A `Float` is simply a number with decimals. This variable is used in the **Get Variable** node. An **Object** variable, is a variable that can be accessed through the object the graph is added to. This is also how you can expose variables in the Unity inspector, and tweak them as needed.

The two **Input.Get Axis Raw** nodes use the `Horizontal` and `Vertical` input names. These are defined in Unity's **Input Manager** which can be modified under **Edit > Project Settings... > Input Manager**. In short, they allow the player to use the arrow keys, WASD, and the left analog stick on game controllers as input by default.

The *output* of **Input.Get Axis Raw** is a value between `-1.0` and `1.0`. For the `Horizontal` axis this translates to *left* and *right*, and for the `Vertical` axis it translates to *down* and *up*.

> A small side effect of adding the two axes together is that the player moves faster diagonally. We won't fix this in this example.

### On Update and On Fixed Update

**On Update** is a special event that is called every frame of our game. This is where most of your real-time logic will happen. It is where we gradually frame-by-frame move objects to create the illusion of smooth movement. It is also where we may check if the human player presses any buttons. **On Update** syncs perfectly with when the image is rendered on to the screen.

**On Fixed Update** on the other hand, is called at a fixed interval that is separate from **On Update** and does not sync with the screen or **On Update**. Its primary function is to simulate physics which may need to happen more frequently in complex scenarios or less often to consume less energy from mobile device. **On Fixed Update** should generally be used whenever you are modifying a `Rigidbody` or `Rigidbody2D`, which we are here.

Detecting input, especially the exact moment a button is pressed down or release, should happen during **On Update**. This is because **On Fixed Update** does not update in-sync with the input system, and it is therefore possible to miss a button press. Since we are responding to movement input *continuously* we are less concerned with this detail.

[![Graph](./graph.jpg)](./graph.jpg)

---

[^1]: A *variable* is some data that is referenced by name. For example, `moveSpeed` references some data, in this case the number `3.0`. We know it is a number, since its data-type is `Float`. If it was some other data-type, the zeros and ones stored in the computer's memory would mean something else, like the letter 'a'.