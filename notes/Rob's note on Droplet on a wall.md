---
title: Rob's note on Droplet on a wall
created: '2022-10-27T13:36:48.963Z'
modified: '2022-11-02T13:57:48.894Z'
---

# Rob's note on Droplet on a wall

note on Young's equation for contact angle. This seems like an undergraduate-level exercise but it's not trivial.

## Preamble

We have in mind a wetting droplet on a flat surface. (Either $2d$ or $3d$ setup.)

The liquid-vapour surface tension is $\gamma_{L V}$. The wall-liquid and wall-vapour surface tensions are $\gamma_{W L}$ and $\gamma_{W}$ respectively. In fact we only need two parameters which are

$$
\gamma_{1}=\gamma_{L V}, \quad \gamma_{2}=\gamma_{W V}-\gamma_{W L}
$$

Note: if $\gamma_{2}>0$ then the wall prefers to be wet (lower surface tension with liquid).

The contact angle for the droplet is $\theta$. Young's equation is

$$
\cos \theta=\frac{\gamma_{2}}{\gamma_{1}}
$$

This obviously works only if $\left|\gamma_{2}\right|<\gamma_{1}$. If $\gamma_{2}>\gamma_{1}$ then the whole wall has to be wet and there is no droplet. If $\gamma_{2}<-\gamma_{1}$ then we get a spherical/circular droplet that doesn't touch the wall.

This all holds on macroscopic scale.

### Minimisation of free energy

To derive Young's equation, it is sufficient to minimise the surface free energy, subject to the constraint that we have a fixed amount of liquid. The surface free energy (using language appropriate to 3d) is:

$$
F_{\text {surface }}=\gamma_{1} \times(\text { curved surface area })-\gamma_{2} \times(\text { planar surface area })
$$

(The zero of surface free energy is defined for a state with no liquid at all, and a completely dry wall.) We will implement the constraint by a Lagrange multiplier $\lambda$ so we have to extremise

$$
\gamma_{1} \times(\text { curved surface area })-\gamma_{2} \times(\text { planar surface area })-\lambda \times(\text { volume of droplet })
$$

Note: the statistical mechanical origin of the Lagrange multiplier is the Laplace pressure. We make this connection in a simple way. (There may be subtleties, but see elsewhere.) The droplet and vapour must have (strictly) equal chemical potential $\mu$ so let's parameterise in terms of $\mu$. Then we can approximate the total free energy as the sum of the grand free energies of the droplet and vapour: ${ }^{1}$

$$
F_{\text {bulk }}=\Phi_{\text {liq }}\left(\mu, V_{\text {liq }}, T\right)+\Phi_{\mathrm{vap}}\left(\mu, V_{\mathrm{vap}}, T\right)
$$

Using $\Phi(\mu, V, T)=-V P(\mu, T)$ where $P$ is pressure, this is

$$
\begin{aligned}
F_{\mathrm{bulk}} &=-V_{\mathrm{liq}} P_{\text {liq }}(\mu, T)-V_{\mathrm{vap}} P_{\mathrm{vap}}(\mu, T) \\
&=-\left[P_{\text {liq }}(\mu, T)-P_{\mathrm{vap}}(\mu, T)\right] \times V_{\mathrm{liq}}-V_{\mathrm{total}} P_{\mathrm{vap}}(\mu, T)
\end{aligned}
$$

${ }^{1}$ I suspect this should really be $F_{\text {bulk }}=\Phi_{\text {liq }}\left(\mu, V_{\text {liq }}, T\right)+\Phi_{\text {vap }}\left(\mu, V_{\text {vap }}, T\right)+\mu N_{\text {total }}$ which is the sum of the canonical free energies. In fact I suspect that the proper statement here is sth like

$$
F_{\text {bulk }}\left(N_{\text {total }}, V_{\text {liq }}, V_{\text {vap }}, T\right)=\inf _{\mu}\left[\Phi_{\text {liq }}\left(\mu, V_{\text {liq }}, T\right)+\Phi_{\text {vap }}\left(\mu, V_{\text {vap }}, T\right)+\mu N_{\text {total }}\right]
$$

The full problem to be solved would be $F\left(N_{\text {tot }}, V_{\text {tot }}, T\right)=\inf _{\text {droplet geometry }}\left[F_{\text {surface }}+F_{\text {bulk }}\right]$ which (swapping order of infs) is the same as

We focus here on the inf over the geometry.

$$
F\left(N_{\text {tot }}, V_{\text {tot }}, T\right)=\inf _{\mu} \inf _{\text {geometry }}\left[F_{\text {surface }}+\Phi_{\text {liq }}\left(\mu, V_{\text {liq }}, T\right)+\Phi_{\text {vap }}\left(\mu, V_{\text {vap }}, T\right)+\mu N_{\text {total }}\right]
$$

We are working at fixed $\mu$ so we treat the last term as constant. ${ }^{2}$ Then $V_{\text {liq }}$ is the droplet volume so comparing this expression with the droplet-volume term in our variational problem 4 gives $\lambda=P_{\text {liq }}(\mu, T)-P_{\text {vap }}(\mu, T)$. That is 4 ) can be interpreted as $F=F_{\text {surface }}+F_{\text {bulk }}$.

Note on physics: the pressure of the liquid inside the droplet ends up slightly larger than the pressure in the vapour, the difference is called Laplace pressure. This also means that the chemical potential $\mu$ must be very slightly larger than the coexistence value (because $P_{\mathrm{liq}}\left(\mu_{c}, T\right)=P_{\mathrm{vap}}\left(\mu_{c}, T\right)$ so non-zero Laplace pressure requires $\left.\mu \neq \mu_{c}\right)$. Other short notes: (i) Since we work on macro-scale, these differences are small (eg droplet curvature is a macroscopic length scale so Laplace pressure is small). (ii) This minimization over geometries only really makes sense in a canonical $(N V T)$ setup, but if we had (eg) a molecular dynamics simulation then the pressure and chemical potential inside the droplet could be measured (virial, widom insertion, etc).

### 2d case, by calculus of variations

Let's do the $2 \mathrm{~d}$ case. (Following wiki page on wetting but we go slowly and carefully.)

The height of the droplet above the plane is given by a function $f(x)$. We assume here that $f$ is single-valued which means that we are restricted to contact angles less than $\pi / 2$, this could presumably by relaxed but it's not quite trivial. (Would it be better to define $f$ parametrically from the start?)

We put the edges of the droplet at $\pm R$ and assume (for simplicity) that $f$ is an even function. Since $f^{\prime}$ is the gradient of the function, wetting angle obeys

$$
\tan \theta=-f^{\prime}(R), \quad \cos \theta=\frac{1}{\sqrt{1+f^{\prime}(R)^{2}}}, \quad \sin \theta=\frac{-f^{\prime}(R)}{\sqrt{1+f^{\prime}(R)^{2}}},
$$

(If we wanted to consider $\theta>\pi / 2$ then we would have to put $\pm$ in front of the the cosine formula and $\mp$ for the sine.) The arc length of the curved surface is $\int \sqrt{1+f^{\prime 2}} d x$ so we have to extremise

$$
2 \int_{0}^{R}\left[\gamma_{1} \sqrt{1+f^{\prime 2}}-\lambda f\right] d x-2 \gamma_{2} R
$$

but there is an additional constraint that $f(R)=0$. We are free to divide by 2 since this won't affect the minimiser, so we choose to extremise

$$
L([f], R)=\int_{0}^{R}\left[\gamma_{1} \sqrt{1+f^{\prime 2}}-\lambda f\right] d x-\gamma_{2} R-\mu f(R)
$$

over the function $f$ and the number $R$, where $\lambda, \mu$ are Lagrange multipliers. (It should be clear that $f$ is shorthand for $f(x)$, etc. But we write $f(R)$ if we need to consider the edge of the droplet.)

We could use some machinery but we do all from "first principles". So put $f \rightarrow f+\delta f$ and $R \rightarrow R+\delta R$ and compute the first variation of $L$, as

$$
\delta L=\int_{0}^{R}\left[\gamma_{1} \frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}} \delta f^{\prime}-\lambda \delta f\right] d x+\delta R\left[\gamma_{1} \sqrt{1+f^{\prime}(R)^{2}}-\lambda f(R)-\gamma_{2}-\mu f^{\prime}(R)\right]-\mu \delta f(R)
$$

This has to be zero for all $\delta R$ and for all choices of the function $\delta f$. As usual the next step is integration by parts, to get rid of $\delta f^{\prime}$. The only wrinkle is that there will be a boundary term. I get

$$
\begin{aligned}
\delta L=\left[\begin{array}{r}
\left.\gamma_{1} \delta f \frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right]_{0}^{R}-\int_{0}^{R}\left[\gamma_{1} \frac{d}{d x}\left(\frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right)+\lambda\right] \delta f d x
\end{array}\right.\\
&+\delta R\left[\gamma_{1} \sqrt{1+f^{\prime}(R)^{2}}-\lambda f(R)-\gamma_{2}-\mu f^{\prime}(R)\right]-\mu \delta f(R)
\end{aligned}
$$

${ }^{2}$ I believe that this is ok if we look for locally-stable droplet shapes by local minimization wrt droplet geometry, but we need something more if we want to compare qualitatively different states. (Recalling previous footnote, we have to separately minimize over $\mu$ for each geometry, we can't just compare at fixed $\mu$ or fixed $V_{\text {liq. }}$.) This looks bad but we can simplify a bit, using $f(R)=0$ (droplet edge) and $f^{\prime}(0)=0$ (by symmetry). We get

$$
\delta L=\left[\gamma_{1} \frac{f^{\prime}(R)}{\sqrt{1+f^{\prime}(R)^{2}}}-\mu\right] \delta f(R)-\int_{0}^{R}\left[\gamma_{1} \frac{d}{d x}\left(\frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right)+\lambda\right] \delta f d x+\delta R\left[\gamma_{1} \sqrt{1+f^{\prime}(R)^{2}}-\gamma_{2}-\mu f^{\prime}(R)\right]
$$

Since $\delta L=0$  forall function $\delta f$ etc. then all three objects in [..] must vanish. Fi rthe first $[...]$ we see that

$$
\mu=\gamma_{1} \frac{f^{\prime}(R)}{\sqrt{1+f^{\prime}(R)^{2}}}
$$

Putting this into the third $[\cdots]$ we get

$$
\gamma_{2}=\gamma_{1}\left[\sqrt{1+f^{\prime}(R)^{2}}-\frac{f^{\prime}(R)^{2}}{\sqrt{1+f^{\prime}(R)^{2}}}\right]=\gamma_{1} \frac{1}{\sqrt{1+f^{\prime}(R)^{2}}}=\gamma_{1} \cos \theta
$$

This is Young's equation (2) so we are done.

Finally, consider the second $[\cdots]$, which gives us

$$
\lambda=-\gamma_{1} \frac{d}{d x}\left(\frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right)=\gamma_{1}\left[\frac{-f^{\prime \prime}}{\sqrt{1+f^{\prime 2}}}+\frac{f^{\prime 2} f^{\prime \prime}}{\sqrt{1+f^{\prime 2}}}\right]=\frac{-\gamma_{1} f^{\prime \prime}}{\left(1+f^{\prime 2}\right)^{3 / 2}}
$$

This last expression reduces (by a standard formula) to $-\gamma_{1} / r_{c}$ where $r_{c}$ is the (signed) radius of curvature of the droplet. ${ }^{3}$ So this equation means the droplet has constant curvature, it is an arc of a circle, there are also other ways to see this. ${ }^{4}$ Moreover, $\lambda=\gamma_{1} /\left|r_{c}\right|$. Physically, $\lambda$ is a Lagrange multiplier for the liquid volume, which should be a pressure: in fact this seems to be the Laplace pressure.

For $3 \mathrm{~d}$ : this computation is quite easily adapted if we assume circular symmetry. Eg the curved area becomes $\int_{0}^{R} \sqrt{1+f^{\prime}(r)^{2}} 2 \pi r d r$ and the volume $\int_{0}^{R} f(r) 2 \pi r d r$. All goes through, ${ }^{5}$ in this case $\lambda=2 \gamma_{1} / r_{c}$ which is indeed Laplace pressure in $3 d$

\section{2d case, after assuming droplet shape}

If we assume that $f$ is an arc of a circle (radius $r$ ), we can compute the relevant lengths and areas, we should extremise

$$
L(\theta, r)=2 \gamma_{1} r \theta-2 \gamma_{2} r \sin \theta-\lambda r^{2}[\theta-(1 / 2) \sin 2 \theta]
$$

where $\lambda$ is Lagrange multiplier. Differentiating with respect to $\theta$ and $r$ gives two equations

$$
\begin{aligned}
&0=2 r\left[\gamma_{1}-\gamma_{2} \cos \theta\right]-\lambda r^{2}[1-\cos 2 \theta] \\
&0=2\left[\gamma_{1} \theta-\gamma_{2} \sin \theta\right]-2 \lambda r[\theta-\sin \theta \cos \theta]
\end{aligned}
$$

${ }^{3}$ One way to see this is to consider a generic circle of (positive) radius $r_{c}$, that is $f(x)=\sqrt{r_{c}^{2}-x^{2}}+k$. Then $\frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}=-x / r_{c}$ so indeed $\left|\frac{d}{d x} \frac{f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right|=1 / r_{c}$. Since this expression is defined locally on the circle, it means that we can compute the curvature of any line by approximating it locally as a circle and using this formula.

${ }^{4}$ Alternatively we can see that $f$ is an arc of a circle by integrating the equation given by the second $[\ldots]$ to get $(\lambda x+C) \sqrt{1+f^{\prime 2}}=-\gamma_{1} f^{\prime}$. By assumption $f^{\prime}(0)=0$ so $C=0$. Then solve the resulting equation which gives a circle.

${ }^{5}$ Dropping an overall numerical factor of $2 \pi$, I get sth like

$$
\delta L=\left[\gamma_{1} \delta f \frac{r f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right]_{0}^{R}-\int_{0}^{R}\left[\gamma_{1} \frac{d}{d r}\left(\frac{r f^{\prime}}{\sqrt{1+f^{\prime 2}}}\right)+\lambda r\right] \delta f d r+\delta R\left[\gamma_{1} R \sqrt{1+f^{\prime}(R)^{2}}-\lambda R f(R)-\gamma_{2} R-\mu f^{\prime}(R)\right]-\mu \delta f(R)
$$

All works fine for the contact angle. For the second [ $\cdots]$, set it to zero and integrate the equation to get $\gamma_{1} r f^{\prime} / \sqrt{1+f^{\prime 2}}+\lambda r^{2} / 2=C$. This holds as $r \rightarrow 0$ so $C=0$. Then we can check that $f=\sqrt{r_{c}^{2}-r^{2}}+k$ still works in this equation, with $r_{c}=\lambda /\left(2 \gamma_{1}\right)$. If one eliminates $\lambda$ between these two equations then some algebra gives

$$
2\left(\gamma_{1} \cos \theta-\gamma_{2}\right)(\sin \theta-\theta \cos \theta)=0
$$

We only care about $0<\theta<\pi$ so the second bracket is never zero. Hence the first bracket must be zero and we get Young's equation.

Also note that we recover $\lambda=\gamma_{1} / r$, so this $\lambda$ is still the pressure.

This computation is not particularly transparent, it does seem possible that we would be better to parameterise by a different variable $($ instead of $r)$

## 3d case, after assuming droplet shape

Repeating the $2 \mathrm{~d}$ computation, we get in this case

$$
L(\theta, r)=2 \pi \gamma_{1} r^{2}(1-\cos \theta)-\gamma_{2} \pi r^{2} \sin ^{2} \theta-\lambda \frac{\pi r^{3}}{3}(2+\cos \theta)(1-\cos \theta)^{2}
$$

(The object that multiplies $\lambda$ is a formula for the volume of a spherical cap.) We write everything in terms of $c=\cos \theta$ and differentiate with respect to $c$ and $r$ to get two equations:

$$
\begin{aligned}
&0=2 \pi r^{2}\left(-\gamma_{1}+\gamma_{2} c\right)-\lambda \pi r^{3}\left(1-c^{2}\right) \\
&0=4 \pi r\left[\gamma_{1}(1-c)-\gamma_{2}\left(1-c^{2}\right)\right]+\lambda \pi r^{2}(2+c)(1-c)^{2}
\end{aligned}
$$

As before we can eliminate $\lambda$ and all simplifies to

$$
\gamma_{2}=c \gamma_{1}
$$

which is Young's equation again. 6

${ }^{6}$ We assumed $c \neq 1$ in deriving this, similar to our assumption $\theta \neq 0$ in the $2 \mathrm{~d}$ case. This might be relevant if we want to include the possibility of complete wetting for $\gamma_{2}>\gamma_{1}$.
