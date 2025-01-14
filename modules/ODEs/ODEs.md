---
layout: default
title: Ordinary Differential Equations
has_children: true
has_toc: true
nav_exclude: true
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Ordinary Differential Equations

Most physical phenomena are ultimately described by a relationship
between changing quantities, resulting in differential equations. If
such an equation only contains one independent variable (such as time)
and hence only total derivatives (and no partial derivatives) we
classify it as an
**[ordinary differential equation](http://mathworld.wolfram.com/OrdinaryDifferentialEquation.html)**
(**ODE**). An ODE of order $$n$$ contains no derivatives higher than
the $$n$$-th derivative:

$$
F(t, y, y^{(1)},  \dots, y^{(n)}) = 0
$$

The *dependent* variable $$y = y(t)$$ is a function of the
*independent variable* $$t$$ and $$y^{(n)} = \frac{d^{n}y}{dt^{n}}$$
is the $$n$$-th derivative with respect to $$t$$. A *linear ODE* only
contains first powers of $$y$$ or its derivatives. A *non-linear ODE*
may contain higher powers. There often exist methods to solve linear
ODEs analytically but this is impossible for most non-linear
ODEs. Solutions of an ODE are fixed by the initial conditions[^1],
e.g., $$y_0 = y(t_{0})$$ and similar for all higher derivatives. For
an ODE of order $$n$$, exactly $$n$$ initial conditions are needed.

Using ODE integration algorithms (*integrators*) we can solve linear
*and* non-linear ODEs of any order *numerically*. The basic idea is to
start with the initial conditions and then propagate $$y$$ for a small
step $$h$$ to numerically compute $$y(t_0 + h)$$ and all its
derivatives. By repeating the process, one *extrapolates* from the
initial condition to any "later" value of $$t$$.

We will first study the simplest integrator, the *Euler* algorithm, and
then look at a more robust class of integrators, the *Runge-Kutta*
schemes.


## Introductory example: The bouncing ball

We will introduce the basic ideas for solving ODEs by looking at
a very simple physical example: the bouncing ball with Newton's
equations of motion

$$
\frac{d^2 y}{dt^2} = -g
$$

where $$g$$ is the constant acceleration due to gravity[^2] and
$$y(t)$$ is the position of the ball as a function of time (its
trajectory).

The forward Euler scheme for any *first order ODE* 

$$
\frac{dy}{dt} = f(y, t)
$$

is

$$
y(t + h) = y(t) + h f(y(t), t).
$$

In order to solve the original 2nd order equation of motion we make
use of the fact that one $$n$$-th order ODE can be written as $$n$$
coupled first order ODEs, namely

$$
\begin{align}
\frac{dy}{dt} &= v\\
\frac{dv}{dt} &= -g.
\end{align}
$$

Solve each of the first order ODEs with the Euler algorithm:

$$
\begin{align}
y(t + h) &= y(t) + h v(t)\\
v(t + h) &= v(t) - h g.
\end{align}
$$

In class we developed a simple simulation for free fall and for the
bouncing ball.

* [bounce_ball_numpy.ipynb]({{ site.nbviewer.resources }}/10_ODEs/bounce_ball_numpy.ipynb):
  simulation and graphing with [matplotlib]({% link
  modules/scientific_python/matplotlib.md %})



## Resources ##

* _Computational Modelling_: Chapter **2**
* _Computational Physics_: Chapter **9**
* Weisstein, Eric
  W. ["Ordinary Differential Equation."](http://mathworld.wolfram.com/OrdinaryDifferentialEquation.html)
  From MathWorld — A Wolfram Web Resource.
* _[Numerical Recipes in C](http://apps.nrbook.com/c/index.html)_, WH
  Press, SA Teukolsky, WT Vetterling, BP Flannery. 2nd
  ed, 2002. Cambridge University Press. Chapter **16**.


------------------------------------------------------------

## Footnotes

[^1]:

     Solutions to ODEs can also be restricted by *boundary conditions*
     (values of the solution on the domain boundary) but this leads to
     difficult Eigenvalue problems and will not be considered in this
     lesson.
	 
[^2]:

     The boundary condition at the floor is that the ball bounces back
     elastically, i.e., the velocity is reversed on collision.

