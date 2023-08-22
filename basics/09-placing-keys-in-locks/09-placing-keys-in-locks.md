---
title: 09. Placing Keys In Locks
parent: Basics
---

# 09. Placing Keys In Locks

> Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

Continuing from example [08. Picking Up A Key](../08-picking-up-a-key/08-picking-up-a-key), we will now add a *Lock* the *Key* can be placed in.

## The Lock

The first step is to create a new game object that will act as the *Lock*. The *Lock* should have two `BoxCollider2D` components: One for detecting when the *Player* is nearby and one to that prevents the *Player* from walking through it.

The `BoxCollider2D` that detects when the *Player* is nearby should be larger than the *Lock* itself and set to be a trigger. The inner collider should simply match the graphics and **not** set as a trigger.

![Lock Colliders](./lock-colliders.jpg)

The *Lock* *triggers* two custom events, `OnEnterLock` and `OnExitLock`, which will be received by the *Player*.

The *Lock* also *receives* a custom event, `OnUnlock`, which will be *triggered* by the *Player*. This flow will then receive the *Key* and set its position to the same as the *Lock* and disable the collider on the *Key* to prevent further interaction with it.

[![Lock Graph](./lock-graph.png)](./lock-graph.png)

## The Player

On the *Player* graph, add an additional **Graph** variable called `activeLock`. This is where we will store which *Lock* we are currently nearby.

![Player Variables](./player-variables.jpg)

The first thing to set up, are the two *event* receivers for `OnEnterLock` and `OnExitLock`. The `OnEnterLock` event will send a reference to the *Lock* so that we can later communicate with it.

[![Player Graph 1](./player-graph-1.jpg)](./player-graph-1.jpg)

The second and last bit, is to *trigger* the `OnUnlock` event on the *Lock*, in case one is nearby. That is, if some *Lock* has sent an event to the *Player* about that they entered the *Lock's* trigger.

Modify the logic where the *Player* previously released the *Key* to also include the event that potentially tells the *Lock* to unlock (the part highlighted in yellow).

[![Player Graph 2](./player-graph-2.jpg)](./player-graph-2.jpg)

Right now, any *Key* can be used on any *Lock*. In the next example, we will look at how to restrict *Keys* to only work with certain *Locks*.