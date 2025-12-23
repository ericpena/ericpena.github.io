+++
title = "Throwing at Wall"
tags = ["physics"]
date = "2024-02-21"
description = "The article provides a solution to a David Morin textbook problem, determining the optimal angle to throw a ball at a wall for maximum height based on physics principles"
+++

### D. Morin 3.47

You throw a ball with speed $v_0$ at a vertical wall, a distance $l$ away. At what angle should you throw the ball so that it hits the wall as high as possible? Assume $l < v_0^2/g$.

-------------------------

In general,

$$y = y_0 + v_{0,y}t - \frac{1}{2}gt^2 = y_0 + v_{0}\cdot\sin(\phi)\cdot t - \frac{1}{2}gt^2$$
$$x = x_0 + v_{0,x}t = x_0 + v_{0}\cdot\cos(\phi)\cdot t$$

The time it takes to hit the wall is,

$$t_{\text{wall}}=\frac{l}{v_0\cdot \cos(\phi)}$$

The height expression of the ball becomes,

$$h=\frac{v_0\sin(\phi)l}{v_0\cos(\phi)}-\frac{gl^2}{2v_0^2\cos^2(\phi)}=l\tan(\phi)-\frac{gl^2}{2v_0^2\cos^2(\phi)}$$

In order to determine the angle that produces the maximum height when hitting wall, we need to take maximize this function with respect to the angle, $\frac{\partial h(\phi)}{\partial \phi}$.

Since,
$$\frac{\partial}{\partial \phi}\tan(\phi) = \frac{\cos^2(\phi)+\sin^2(\phi)}{\cos^2(\phi)}=\sec^2(\phi)$$
$$\frac{\partial}{\partial \phi}\frac{1}{\cos(\phi)} = \frac{\sin(\phi)}{\cos^2(\phi)}=\sec(\phi)\cdot \tan(\phi)$$

$$\phi^* = \tan^{-1}\left( \frac{v_0^2}{gl} \right)$$