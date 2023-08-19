---
title: 04. Animating The Door
parent: Basics
---

# 04. Animating The Door

Using **Unity 2021.3.27f1** and **Visual Scripting 1.8.0**. The project is using the **2D Core** template.

![Demo](./demo.gif)

In this example we will animate the door using only scripts, so that it moves from one position to another with a smooth motion.

Start by adding two additional **Object** variables to the door graph:

- `animationDuration` of type `Float`
- `animationCurve` of type `Animation Curve`

We can use the **Animation Curve** to control easing of the door, or even give it a bounce effect! Together with the `animationDuration` we get complete control of the motion from start to end.

In addition, we add a **Graph** variable named `animationTime` of type `Float`. We will use this variable to remember how far the animation has progressed. Initially, we set the value `animationTime` to be the same as `animationDuration`, thereby assuming that the animation is "done" when our game starts. The animation is then restarted whenever the door is toggled.

![Graph Variables](./graph-variables.jpg)



[![Graph](./graph.jpg)](./graph.jpg)