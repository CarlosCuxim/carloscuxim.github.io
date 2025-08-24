---
title: 'The area of an inscribed triangle'
published: 2025-08-19
draft: false
description: 'Various calculations to obtain a formula to get the area if an inscribed triangle'
tags: ['math']
toc: true
---

Some days ago, a friend presented me a problem: If you have a circle of radius
$r$, Which is the inscribed quadrilateral with the biggest area.

Currently I don't have an answer for that question, but I decided to try
something more easy. Which is the inscribed triangle with the biggest area?

Even if it seems more easy, I don't have a simple solution. The intuition tells
me that probably is the quadrilateral triangle, but in math intuition is not
enough, it's necessary a proof.

To attack the problem, I decided to take some suppositions. First, the circle
will be of radius $1$. Second the triangle will have three vertices, $A$, $B$
and $C$, that lies in the circle.Third $C$ will be the point $(-1,0)$ and last
I will express $A$ and $B$ with polar coordinates, as follows:

$$
  A = (1; \alpha),
  \qquad
  B = (1; \beta),
  \quad
  -\pi < \beta < \alpha < \pi.
$$

The first thought I had was: How I can get the area of the triangle? Well, this
is an interesting question, what I will do is to know how to get the area of
the parallelogram that defines two vectors. If I know this area, then I can
just divide by two and get the area of the triangle that defines two vector.
And how this can help me? Easy, if I know how to calculate the area of this
triangle I have two options to calculate the area of the triangle $\triangle
ABC$:

1. Use $C-A$ and $C-B$ as the vectors, since the triangle defined by these two
   vectors is congruent of the triangle $\triangle ABC$.
2. If $O$ is the origin $(0,0)$, then calculate the area of the triangles
   $\triangle AOB$, $\triangle BOC$ and $\triangle AOC$.

## The area of the parallelogram defined by two vectors

Suppose that we have two vectors $u$ and $v$
