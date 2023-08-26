---
title: 11. Play an Animation
parent: Basics
---

# 11. Play an Animation

> Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

This example uses the `Animator` component to play an `AnimationClip`. If you are unfamiliar with setting up Animation Clips and Animator Controllers, I recommend you find a tutorial elsewhere, for example at Unity's own learning site:

- [Animator Controllers](https://learn.unity.com/tutorial/animator-controllers-2019-3)
- [Introduction to Sprite Animations](https://learn.unity.com/tutorial/introduction-to-sprite-animations)

For this example, I have prepared a small Unity Package which contains two sprite animation clips and an `Animator Controller` with the necessary states set up. You can download the package here: [gate.unitypackage](./gate.unitypackage).

While this example is using a 2D sprite animation, the steps for controlling animations are the same.

## Setting up the Gate Game Object

In this example I will be using an animation of a gate opening.

The first step is to set up a new game object with an `Animator` component that has an `Animator Controller` assigned. 

<img src="./gate-inspector-1x.webp" srcset="./gate-inspector-1x.webp 1x, ./gate-inspector-2x.webp 2x" alt="Gate Inspector">

In addition to the game object, I have added three child game objects that each have a `BoxCollider2D`. They act as colliders for the edge of the gate and the gate itself.

<img src="./gate-colliders-1x.webp" srcset="./gate-colliders-1x.webp 1x, ./gate-colliders-2x.webp 2x" alt="Gate Colliders">

## The Animator Controller

The `Animator Controller` is set up with two *states*: *Idle* and *Open*. The *Idle* state is the default state (indicated by the orange color) and is simply a single frame. The *Open* state is a short sprite animation of the gate opening.

We will use the names of the *States*, rather than the animation clips themselves, later in our Script Graph. 

<img src="./gate-animator-1x.webp" srcset="./gate-animator-1x.webp 1x, ./gate-animator-2x.webp 2x" alt="Animator Controller">

Below is the *Gate@Open* animation clip in the **Animation** window.

<img src="./gate-animation-1x.webp" srcset="./gate-animation-1x.webp 1x, ./gate-animation-2x.webp 2x" alt="Animation Clip">

## The Gate Script Graph

For the *Gate's* script graph, we just create a **Custom Event** node that can be triggered by another script.

We then use an **Animator: Play (State Name)** node to play an animation by providing it the name of the *state* we would like to play. In this case, we use the value `Open`. That's all there is to it!

In addition, we disable the collider for the gate so that the player can walk through it. The gate collider is set up using an **Object** variable called `gateCollider` and is of type `Game Object`.

<img src="./gate-variables-1x.webp" srcset="./gate-variables-1x.webp 1x, ./gate-variables-2x.webp 2x" alt="Gate Variables">

[<img src="./gate-graph-1x.webp" srcset="./gate-graph-1x.webp 1x, ./gate-graph-2x.webp 2x" alt="Gate Graph">](./gate-graph-2x.webp)

## Making the Lock Open the Gate

The last piece of this example, is triggering the *event* from the *Lock* that we've made previously.

For the *Lock's* script graph, add an **Object** variable named `gate` of type `Game Object` and assign the *Gate* game object to it.

<img src="./lock-variables-1x.webp" srcset="./lock-variables-1x.webp 1x, ./lock-variables-2x.webp 2x" alt="Lock Variables">

Then add the highlighted nodes to the existing flow of the *Lock's* `OnUnlock` event that will trigger the `OpenGate` event on the *Gate*.

[<img src="./lock-graph-1x.webp" srcset="lock-graph-1x.webp 1x, lock-graph-2x.webp 2x" alt="Lock Graph">](./lock-graph-2x.webp)

## Bonus Info

In addition to using **Animator: Play (State Name)** you can also use **Animator: Cross Fade In Fixed Time (State Name, Fixed Transition Duration)**. The `Fixed Transition Duration` expects a certain number of seconds, like `0.25` that defines how long the transition should be.

Note that *cross fading* does not work with sprites, but is very useful when using 3D animation or animating other properties that can be smoothly transitioned between. 

<img src="./crossfade-1x.webp" srcset="./crossfade-1x.webp 1x, ./crossfade-2x.webp 2x" alt="Cross Fade">

I recommend you look up Unity's Scripting API documentation for more information about `Play()` and `CrossFadeInFixedTime()`. Though it is written for C# scripting, the explanations also apply to visual scripting.

- [Animator.Play](https://docs.unity3d.com/ScriptReference/Animator.Play.html)
- [Animator.PlayInFixedTime](https://docs.unity3d.com/ScriptReference/Animator.PlayInFixedTime.html)
- [Animator.CrossFade](https://docs.unity3d.com/ScriptReference/Animator.CrossFade.html)
- [Animator.CrossFadeInFixedTime](https://docs.unity3d.com/ScriptReference/Animator.CrossFadeInFixedTime.html)