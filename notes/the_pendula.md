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

<div style="display:flex; align-items:flex-start; gap:20px;">

  <!-- Left column: image -->
  <div style="flex:0 0 40%; max-width:260px;">
    <img src="/assets/images/planar_pendulum_coordinates.png" style="width:100%; display:block;">
    <p style="font-size:14px; text-align:center; margin-top:5px;">
      Fig. 1 — Simple pendulum
    </p>
  </div>

  <!-- Right column: text -->
  <div style="flex:1; min-width:0;">
    <p>
    $$
    x = \ell \sin\theta , \ \ \ y = - \ell \cos\theta
    $$
    </p>

    <p>
    thus, the particle is subjected to a potential in the form
    </p>

    <p>
    $$
    U = m g \ell (1-\cos\theta)
    $$
    </p>

    <p>
    note that here we are setting the zero of the potential at the pendulum rest point, that is, at $\theta = 0$. Since we are considering the string to be inextensible, the motion is restricted to a circumference of radius $\ell$. The kinetic energy can be directly evaluated:
    </p>
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
T = \frac{2\pi}{\omega_0} = 2\pi \sqrt{\frac{\ell}{g}}
$$

Well, this is really beautiful. However, what happens as we step out of the small-angle approximation? To investigate that, let's take a different pathway. The system is conservative, and therefore, the total energy

$$
E =
\frac{m \ell^2}{2} \dot{\theta}^2
+
mg\ell \left(1-\cos\theta\right)
$$

is conserved. Rearranging the terms and solving for $\theta$, we obtain the *quadrature*

$$
t - t_0 =
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

first here, we note that physical solutions exist only for $E > mg\ell (1-\cos\theta)$, since the square root must be positive. This expression encodes all physical information of the motion. Note that, however, the rhs of the above quadrature is just a primitive in $\theta$, represented in an integral form. The problem now is: \textit{how do we solve the integral}? It happens that the above integral cannot be integrated in terms of elementary functions. If, on one hand, this equation may look simpler, since it is a first-order differential equation in time, on the other hand, because of the square factor, this equation already has two solution branches.  

The real advantage of this representation is that, from this integral form, we can directly obtain the analytical solution in terms of \textit{elliptic functions}. A detailed discussion of their theory is beyond the scope of this essay, but highly recommended—it is a truly beautiful formulation. Moreover, to do a proper discussion and make this text understandable and pedagogical, a practical introduction to the functions used here will be presented, as they are crucial for the discussion. As a first encounter, one may think of elliptic functions as generalizations of trigonometric functions—which are periodic with period $2\pi$—however, elliptic functions possess two periods. To illustrate, consider that $f$ is an elliptic function; then we have  

$$
f(z + \omega_1) = f(z) = f(z + \omega_2) \ .
$$

Functions like this can only be nontrivial, i.e., different from constant, when the ratio between the two periods, $\omega_1 / \omega_2$, is not purely real. Therefore, elliptic functions are part of complex analysis, even when they are evaluated on real arguments in physical problems. A particularly interesting feature to highlight here is that: if $f(z)$ is an elliptic function, and assuming that $\Phi(z)$ is a rational function, then $\Phi(f(z))$ is an elliptic function with the same periods as $f(z)$; this is a crucial point to solve the \textit{elliptic integral of third kind} that appears later.  

Our main objective here is to discuss the physics of different pendulum systems. In this context, elliptic functions will appear as solutions for specific differential equations. Pragmatically, to solve problems at that stage, we can think of elliptic functions as a class of \textit{special functions}, similarly to how **Legendre** or **Bessel** functions are used to solve special classes of differential equations.  

Now, it is time to solve the pendulum equation finally! The strategy will be simple: we will perform a set of transformations in order to cast the differential equation into the known elliptic integral form. Starting from the energy conservation:

$$
\dot{\theta}^2 = \frac{2}{m\ell^2}\left( E - mg\ell\left( 1-\cos\theta \right) \right) = 2\omega_0^{\,2} \left( \mathcal{E} - (1-\cos\theta) \right) \ ,
$$

where we have then defined the dimensionless parameter $\mathcal{E} = E / mg\ell$. A good practice when solving differential equations in physics is to always deal with dimensionless quantities; hence, we re-parametrize our time parameter as $ \sqrt{2\omega_0^{\,2}}\,{\rm d} t = {\rm d}\tau $. Therefore, we deal with the differential equation:

{% raw %}
$$
\left( \frac{{\rm d}\theta}{{\rm d}\tau} \right)^2 = \mathcal{E} - ( 1 - \cos\theta) \ .
$$
{% endraw %}

Now, we need to distinguish between the possible domains of existence for the orbits. First, noting that $0 \le 1-\cos\theta \le 2$, there are three different regimes: when $\mathcal{E} < 2$, and thus there is a "competition" between these two comparable contributions, leading to a bound motion; the case $\mathcal{E} = 2$ signals that the system has **exactly the energy needed** to reach the maximum value $\theta_{\max} = \pi$—this is the system's separatrix; the last case is $\mathcal{E} > 2$: here the square root is positive regardless of the values assumed by $\theta$, the system can do complete circular rotations, and therefore the orbit is unbound.
