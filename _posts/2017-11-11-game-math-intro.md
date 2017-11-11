---
layout: post
title: Do we need math in game dev?  
categories: [GameDev]
tags : [unity,game-dev]
comments : true
---

If you (like me) want to understand the basic math behind the game development, you're not alone. We need to understand the math or physics if we want to build advanced stuff. So today i want to write a bit about the vectors and the angles between them

##  Magnitude of a Vector

```csharp
Vector2 x = new Vector2();
var magn = x.magnitude;
```

This is actually the length of the Vector like in the coordinate system. Let's say you want to calculate the magnitude by yourself, then you can;

- Get the square of sum of x + y
- Sqrt the sum (Square Root)

and done you have the magnitude!

```csharp
var x = 4; var y = 5;
var sumSq = x^2 + y^2;
var magnitude = Mathf.sqrt(sumSq);
```

## Angle between 2 Vectors

So we wanna get the angle between two vectors, in order to trigger some events maybe shoot or idk your call, assuming we have 2 vectors

- get the *dotProduct* of the 2 vector
- divide them over the *dotProduct* of their *magnitudes*
- and you get the **cosine** of the angle
- InverseCosine that cosine angle and you get the angle in radians
- multiply that angle by 180 / PI and boom

> Unity `Math.Acos(float f)` is a built-in method to inverse the cosine for you!