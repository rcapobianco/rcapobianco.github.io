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

Now, we need to distinguish between the possible domains of existence for the orbits. First, noting that $0 \le 1-\cos\theta \le 2$, there are three different regimes: when $\mathcal{E} < 2$, and thus there is a "competition" between these two comparable contributions, leading to a bound motion. The case $\mathcal{E} = 2$ signals that the system has **exactly the energy needed** to reach the maximum value $\theta_{\max} = \pi$—this is the system's separatrix. The last case is $\mathcal{E} > 2$: here the square root is positive regardless of the values assumed by $\theta$, the system can do complete circular rotations, and therefore the orbit is unbound.

{% raw %}
- *Bound Orbit*, the case: $\mathcal{E} < 2$:

Here, the allowed regions for orbits strongly depend on the turning points. Imagine that we start the motion with the initial value problem: 

$$
\theta(t_0) = \theta_0 \ , \ \ \ \qquad \ \ \ \dot{\theta}(t_0) = \dot{\theta}_0 \ .
$$

Note that the initial velocity cannot be chosen separately from the energy. Besides, it is important to highlight here that, although we are dealing with a first-order differential equation, the numerical value of $\dot{\theta}_0$ does not play any important role in the solution; however, $\mathrm{sign}\, \dot{\theta}_0$ is required to fix the possible branch. The maximum value of the energy is reached exactly at the turning point of the motion, thus: 

$$
\frac{{\rm d}\theta}{{\rm d}\tau} =0 \ \ \ \rightarrow \boxed{ \mathcal{E} = 1 - \cos\theta_{\max} } 
$$

It is clear then that we must have: $\theta_0 \leq \theta_{\max}$; therefore, for a given value of $\mathcal{E}$, the motion is only allowed between $( -\theta_{\max}, \theta_{\max} )$. From here, it is easy to verify that for a particle starting from rest $\dot{\theta}_0 = 0$, which implies $\theta_{\max} = \theta_0$. Thus, our equation becomes:

$$
\left( \frac{{\rm d}\theta}{{\rm d}\tau} \right)^2 = \cos\theta - \cos\theta_{\max} \ , \ \ \ \rightarrow \ \ \ \boxed{
{\rm d}\tau = \xi_{\theta} \frac{{\rm d}\theta}{\sqrt{\cos\theta - \cos\theta_{\max} } } }
$$

with $\xi_\theta = \pm 1$ as the chosen sign, which is fundamental to set the integration onto the right branch. We rewrite the rhs by using the relation: $ \cos\theta = 1-2\sin^2\left(\frac{\theta}{2}\right) $, obtaining:

$$
{\rm d}\tau = \frac{\xi_{\theta}}{\sqrt{2}} \frac{{\rm d}\theta}{\sqrt{\sin^2\left( \frac{\theta_{\max}}{2} \right) - \sin^2 \left( \frac{\theta}{2} \right) } } \ .
$$

The first term here is just a constant, so we set: $k = \sin \left( \frac{\theta_{\max}}{2} \right)$, such that $0 < k < 1$. Now we perform the transformation:

$$
\sin \left( \frac{\theta}{2} \right) = k \sin \psi \ , \ \ \ \qquad \ \ \ {\rm d}\theta = \frac{2k \cos\psi}{\sqrt{ 1-k^2\sin^2\psi }} {\rm d}\psi \ ,
$$

such that $-\pi/2 \leq \psi \leq \pi/2$, and then we have:

$$
\frac{\xi_\theta}{\sqrt{2}} {\rm d}\tau = \frac{{\rm d}\psi}{\sqrt{1-k^2 \sin^2\psi} } \ , \ \ \ \rightarrow \ \ \ \xi_\theta \omega_0 \left( t-t_0 \right) = \int_{\psi_0}^{\psi} \frac{{\rm d}\psi'}{\sqrt{1-k^2 \sin^2\psi'} } \ , 
$$

This is precisely the form we want. At this stage, let us introduce the first elliptic function, the *Jacobi elliptic integral of the first kind*: 

$$
F \left( \psi, k \right) = \int_0^{\psi} \frac{{\rm d}\psi}{\sqrt{1-k^2 \sin^2 \psi} }.
$$

Applying that to our problem, we have:

$$
\int_{\psi_0}^{\psi} \frac{{\rm d}\psi'}{\sqrt{1-k^2 \sin^2\psi'} } = \int_{\psi_0}^{0} \frac{{\rm d}\psi'}{\sqrt{1-k^2 \sin^2\psi'} } + \int_{0}^{\psi} \frac{{\rm d}\psi'}{\sqrt{1-k^2 \sin^2\psi'} } = F(\psi, k) - F(\psi_0, k) \ ,
$$

the second term depends only on the initial conditions. From that, we can set our problem in terms of the $F(\psi, k)$ function as:

$$
F(\psi, k ) = \xi_\theta \omega_0 \left( t-t_0 \right) + F(\psi_0,k) := u(t)
$$

But remember, we are looking for a $\theta(t)$ solution, and to obtain that, we need to invert the above expression. This problem is part of the known as *Jacobi inversion problem*. The inversion of $F(\psi, k)$ is the Jacobi amplitude function:

$$
\psi(t) = F^{-1}(\psi,k) = \mathrm{am}(u(t),k) \ .
$$

Then we conclude:

$$
\theta(t) = 2 \arcsin\left[ k \, \mathrm{sn}\left( \xi_\theta \omega_0 (t-t_0) + F(\psi_0, k) , k \right) \right] \ ,
$$

where $\mathrm{sn}(u,k) = \sin(\mathrm{am}(u,k))$. The motion is oscillatory for $\theta_{\max} < \pi$, or analogously $k<1$. Remember, as previously mentioned, elliptic functions are doubly periodic. In this case, the two periods of $\mathrm{sn}(u,k)$ are: 

$$
\omega_1 = 4K(k) \ , \ \ \ \qquad \ \ \  \omega_2 = 2 i K(1-k), 
$$

where $K(k) = F(\pi/2, k)$ is known as *complete elliptic integral of the first kind*, it has real modulus for $|k| \le 1$, and this is precisely the period of our motion we are interested in. Therefore, the planar pendulum motion has a period:

$$
T= \frac{4}{\omega_0}K(k) \ ,
$$

where we just dropped the sign $\xi_\theta$. To show explicitly that this reproduces the known small-angle periods, consider that around zero, $K(k \approx 0)$ accepts the expansion:

$$
K(k \approx 0) = \frac{\pi}{2} \left( 1 + \frac{k^2}{4} + \mathcal{O}(k^4) \right),
$$

and then we recover the harmonic oscillator period $T = 2\pi/\omega_0$ at first order.

A very interesting and *unexpected* feature completely absent in the small-angle approximation can be seen here explicitly: the period of the oscillatory motion is strictly related to its amplitude!

$$
T = \frac{4}{\omega_0}K(k) = \frac{4}{\omega_0}K\left( \sin\left( \frac{\theta_{\max}}{2} \right) \right) \ .
$$

Oscillatory motion requires $\theta_{\max} < \pi$. As $\theta_{\max} \rightarrow \pi$, $k \rightarrow 1$ and $K(k)$ diverges logarithmically. Physically, this corresponds to the pendulum approaching the unstable equilibrium point. The equations of motion are still satisfied, but the period becomes infinite; thus, it would require an infinite time for the pendulum to complete a swing. This is exactly the indication of the separatrix!
{% endraw %}

{% raw %}
- *Separatrix*, the case $\mathcal{E} = 2$:

At the separatrix, we deal with the equation:

$$
\mathcal{E} = 0 \ , \ \ \ \rightarrow \ \ \ \boxed{ \frac{{\rm d}\theta}{{\rm d}\tau} = \xi_{\theta} \sqrt{1 + \cos\theta} }
$$

By rewriting the equation using the relation: $ 1 + \cos\theta = 2 \cos^2 \left( \frac{\theta}{2} \right)$ we find:

$$
{\rm d}\tau = \xi_\theta \frac{{\rm d}\theta}{\sqrt{2} \cos\left( \frac{\theta}{2} \right)} = \xi_\theta \sqrt{2} \sec{\rm x} {\rm d x}
$$

where: $\theta(t) = 2{\rm x}(t)$. The above integral can now be directly evaluated:

$$
\int \sec{\rm x} \, {\rm d x} = \ln \left( | \sec{\rm x} - \tan{\rm x} | \right) + C = \ln \left( \left| \tan \left( \frac{\pi}{4} + \frac{\theta}{4} \right) \right| \right) + C \ .
$$

Then, after some simple manipulation, we obtain the separatrix exact solution:

$$
\theta(t) = 4 \arctan \left( \tan \left( \frac{\theta_0 + \pi}{4} \right) \exp\left( \xi_\theta \omega_0 (t-t_0) \right) \right) - \pi \ .
$$

This special regime, the separatrix, is exactly the curve that separates the two distinct types of motion in the planar pendulum, the bounded and the unbounded. Note that we have a very interesting behaviour here: starting from an initial point $\theta_0 \neq \pi$, the pendulum will swing to approach the equilibrium points $(-\pi,\pi)$ depending on the sign $\xi_\theta$; however, those points cannot be reached in a finite time. Another interesting feature is that, by setting the initial condition $\theta_0 = \pi$ and $\mathcal{E} = 2$, it marks exactly the unstable equilibrium orbits. This means that the pendulum will then be there until even an infinitesimal perturbation changes the system.
{% endraw %}

{% raw %}
- *Unbound Orbits*, the case $\mathcal{E} > 2$:

Back to the conservation of energy: 

$$
\frac{{\rm d}\theta }{{\rm d}\tau} = \xi_\theta \sqrt{\mathcal{E} - (1-\cos\theta)} \ ,
$$

which is now positive regardless of the value of $\theta(t)$. Now we once again perform: $1 - \cos\theta = 2\sin^2\varphi$, where $\varphi = \theta/2$, obtaining:

$$
{\rm d}\tau = \xi_\theta \sqrt{\frac{1}{\mathcal{E}}} \frac{{2 \rm d}\varphi}{\sqrt{1-j^2 \sin^2\varphi} } \ ,
$$

where we defined $ j = \sqrt{2/\mathcal{E}}$. The expression is now again in Jacobi's form with $0 < j < 1$ and $-\pi/2 < \varphi < \pi/2$, therefore: 

$$
F(\varphi,j) = \xi_\theta \sqrt{\frac{\mathcal{E}}{2}}\omega_0 \left( t-t_0 \right) + F\left( \frac{\theta_0}{2}, j \right) := u(t) \ ,
$$

and now the inversion is straightforward: 

$$
\theta (t) = 2 \mathrm{am} \left( \xi_\theta \sqrt{\frac{\mathcal{E}}{2}}\omega_0 \left( t-t_0 \right) + F\left( \frac{\theta_0}{2}, j \right) , j \right) \ ,
$$

where $\mathrm{am}(u(t),j)$ is the amplitude function. In this scenario, the pendulum has more than enough energy to complete a full rotation regardless of the starting conditions $( \theta_0 , \dot{\theta_0} )$ and, since the system is conservative, the orbits repeat themselves indefinitely.
{% endraw %}

