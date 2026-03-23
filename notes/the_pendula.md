---
layout: page
title: The Pendula
date: 2026-03-23
permalink: /notes/the_pendula/
---

A few systems are as familiar to physicists as the pendulum. It is among the first systems to be discussed in a mechanics course, and the one, re-framed as a harmonic oscillator, that appears in all fields of physics. The simplest model--a mass, an inextensible string, and gravity--yet it reveals a subtle beauty. 

However, that is only the first chapter in the long history of the pendulum in physics. That is the main objective of this page: \textbf{The pendula} will be our ship to navigate through classical mechanics and dynamical systems. We will start with the simple planar pendulum in the small-oscillation approximation, and gradually sail toward more complex systems. As we relax our assumptions, the simplicity fades away, elementary functions give way to elliptic functions, and eventually, integrability is lost altogether, requiring a numerical approach.

For this essay, some knowledge of classical mechanics will be helpful. We will also \textit{touch} on the theory of elliptic functions, for which a small introduction is provided. Additionally, codes are provided alongside the solutions discussed here. The goal is not to be exhaustive but to explore how much physics remains hidden in a system we often take for granted. 

Think of this as a working notebook: from the simple swing of a mass to the edge of chaos. I am glad you are here.

# The Planar Pendulum

We start with the simplest system: a point mass attached to an inextensible string of fixed length, moving under the influence of gravity. The system is a two-dimensional problem with the coordinates (see Fig. 1):

<div style="display:flex; gap:20px; align-items:flex-start;">

<div style="flex:1; max-width:250px;">

<img src="/assets/images/planar_pendulum_coordinates.png" width="100%">

<p style="font-size:14px; text-align:center;">
Fig. 1 — Simple pendulum
</p>

</div>

<div style="flex:2;">

$$
x = \ell \sin\theta , \ \ \ y = - \ell \cos\theta
$$

thus, the particle is subjected to a potential in the form:

$$
U = m g \ell \left( 1 - \cos\theta \right)
$$

note that here we are setting the zero of the potential at the pendulum rest point, that is, at $\theta = 0$. Since we are considering the **string to be** inextensible, the motion is restricted to a circumference of radius $\ell$. The kinetic energy can be directly evaluated:

</div>

</div>



$$
\mathcal{K} = \frac{m}{2} v(t)^2
= \frac{m}{2} \left( \dot{x}^2 + \dot{y}^2 \right)
= \frac{m\ell^2}{2}\dot{\theta}^2
$$

where the dot represents the derivative with respect to time $t$. Therefore, using the Lagrangian $\mathcal{L} = \mathcal{K} - U$, we obtain the second-order differential equation for $\theta$ as

$$
\ddot{\theta} + \omega_0^{\,2} \sin\theta = 0
$$

with $\omega_0^{\,2} = g/\ell$, a constant that has units of inverse time squared. This is the famous **pendulum equation**. At first glance, this may look simple enough, but actually it is already a nonlinear differential equation.

Considering the special regime $\theta \ll 1$, we can take the linear expansion for the sine function $\sin\theta \approx \theta$, and therefore

$$
\ddot{\theta} + \omega_0^{\,2} \theta = 0
$$

which is the famous *harmonic oscillator equation*. Assuming that we are dealing with the initial value problem (IVP), with initial conditions

$$
\theta(t_0) = \theta_0
\qquad
\dot{\theta}(t_0) = \dot{\theta}_0
$$

the general solution is

$$
\theta(t) =
\theta_0 \cos\left(\omega_0 (t - t_0)\right)
+
\frac{\dot{\theta}_0}{\omega_0}
\sin\left(\omega_0 (t - t_0)\right)
$$

This is the *typical* solution often described in classical mechanics textbooks. The system oscillates between $(\theta_{\min}, \theta_{\max})$ with a period

$$
T = \frac{2\pi}{\omega_0}
=
2\pi \sqrt{\frac{\ell}{g}}
$$

Well, this is really beautiful. However, what happens as we step out of the small-angle approximation? To investigate that, let's take a different pathway. The system is conservative, and therefore the total energy

$$
E =
\frac{m \ell^2}{2} \dot{\theta}^2
+
mg\ell \left(1-\cos\theta\right)
$$

is conserved. Rearranging the terms and solving for $\theta$, we obtain the *quadrature*

$$
t - t_0
=
\int_{\theta_0}^{\theta(t)}
\frac{d\theta'}
{\sqrt{
\frac{2}{m\ell^2}
\left(
E - mg\ell (1-\cos\theta')
\right)
}}
:= \mathcal{F}(\theta(t))
$$
