Why use dielectrics instead of conductors for optical waveguides? At super high frequencies (such as with visible light) the attenuation of a metal waveguide is large due to conductor losses. By relying on dielectric materials this issue is totally eliminated.
So why not use this solutions in applications where metal waveguides are used? It's for the same reason why metal waveguides aren't used for audio transmission. They are bulky, expensive, and overkill for the application.

**Operation**
Dielectric waveguides work off the principle of total internal reflection. From Snell's law we will determine the angle for which total internal reflection occurs: $$n_1\sin{\theta_1}=n_2\sin{\theta_2}$$
Solving for $\sin{\theta_1}:$ $$\sin{\theta_1}=\frac{n_2}{n_1}\sin{\theta_2}$$Total internal reflection will occur when the refracted ray is parallel to the boundary ($\theta_2 = \frac{\pi}{2}$)
$$\sin{\theta_{crit}} = \frac{n_2}{n_1}$$
Where $\theta_{crit}$ is the minimum angle for which total internal reflection occur. It's apparent that $n_1 > n_2$ to satisfy $\sin{\theta_{crit}} \le 1$. 

So this means a light beam must be fired at a shallow enough angle to support propagation, otherwise some light will be lost in the form of refraction.

**Supported Modes**
Exactly like the planar mirror waveguide we know the upwards plane wave must have the same phase as the twice-reflected plane wave. Consider the path difference of a twice-reflected ray and a forward propagating ray to obtain the self-consistency condition. (This time I'll actually do the math)
![[Pasted image 20260718140032.png]]

First finding $\overline{AC}:$ $$\sin{\theta}=\frac{d}{\overline{AC}}$$
$$\overline{AC}=\frac{d}{\sin{\theta}}$$
Then finding $\overline{AB}:$
The line $\overline{BC}$ and the line are perpendicular $\overline{AB}$ since the phases at points $B$ and $C$ must match. Triangle $ABC$ can be constructed to solve for line $\overline{AB}$
$$\cos{2\theta}=\frac{\overline{AB}}{\overline{AC}}$$
Using the identity
$$\cos{2\theta}=1-2sin^2{\theta}$$
$$\overline{AB}=\overline{AC}\cos{2\theta}=\frac{d}{\sin{\theta}}(1-2\sin^2{\theta})=\frac{d}{\sin{\theta}}-2d\sin{\theta}$$
$$\overline{AC}-\overline{AB}=2d\sin{\theta}$$
Now we obtain the accumulated phases at point $B$ and $C$ (twice reflected)
Point $B$: $$\phi_B=k\overline{AB}$$
Point $C$: $$\phi_C=k\overline{AC}-2\varphi$$
Where $\varphi$ is the accumulated phase shift from reflected off the dielectric boundary.
And the phase difference is: $$\Delta\phi=\phi_C-\phi_B=k\overline{AC}-2\varphi-k\overline{AB}=k(\overline{AC}-\overline{AB})-2\varphi=2kd\sin{\theta}-2\varphi=2d\frac{2\pi}{\lambda}\sin{\theta}-2\varphi$$
The phase difference must be a multiple of $2\pi$ so that points $A$ and $B$ have the same phasefront.
$$\Delta\phi=2d\frac{2\pi}{\lambda}\sin{\theta}-2\varphi=2\pi n$$
$$d\frac{2\pi}{\lambda}\sin{\theta}-\varphi=\pi n \qquad...(1)$$where $n$ is a positive integer. The phase shift $\varphi$ is obtained from the Fresnel equations derived [here](obsidian://open?vault=photonics&file=Fresnel%20Equation%20TE%20Derivation). For now only consider the TE polarization. The accumulated phase for the TE mode is: $$\tan{(\frac{\varphi}{2})}=\sqrt{\frac{\cos^2{\theta_{crit}}}{\cos^2{\theta_1}}-1} \qquad...(2)$$
Plugging $(1)$ into $(2)$ reveals the self-consistency condition$:$
$$\tan{(\pi\frac{d}{\lambda}\sin{\theta}-m\frac{\pi}{2})=\sqrt{\frac{\sin^2{\overline{\theta}_c}}{\sin^2{\theta}}-1}} \qquad...(3)$$
The bounce angles may be found graphically:
![[Pasted image 20260720230056.png|487]]
Here I used $n_{core} = 3.48, n_{clad} = 1.44, d = 4\mu m, \lambda=1.55\mu m$

The $\tan$ plots are space $\frac{\lambda}{2d}$ apart and contains one intersection. The plot will extend up to $\sin{\overline{\theta}_c}$, so the number of modes are:
$$M \doteq \frac{\sin{\overline{\theta}_c}}{\lambda/2d}=\frac{2d}{\lambda_o}NA$$
**Field Profile**
Next we would like to see what the field is inside of the waveguide. The method used in the [planar mirror waveguide](obsidian://open?vault=photonics&file=Beginner%20Waveguide%20Projects%2FPlanar%20Mirror%20Waveguide) can be used here. Since $\sin{{\theta}_m}$ doesn't simplify to something very nice (self-consistency condition of the mirror waveguide made it super pretty) $k_y$ can be kept in terms of $\sin{\theta_m}$. Instead of doing this I will try to obtain the same result using Maxwells equations. 

Beginning with Helmholtz: $$\nabla^2 \vec{E} + k^2 \vec{E}=0 \qquad...(4)$$
Assume that the solution is some traveling wave with some sort of distribution: $$\vec{E}(x,y,z) = u(x,y)e^{-j\beta z} \qquad...(5)$$
After plugging $(5)$ into $(4)$ we will obtain this result: $$\nabla^2_tu(x,y) + (k^2-\beta^2)u(x,y)=0 \qquad...(6)$$
Where $\nabla^2_t$ is transverse Laplacian. Since the propagation is in the $z$ direction $\nabla^2_t = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$.
$k^2_c$ can be defined as such: $$k^2_c=k^2 - \beta^2$$
For some field to propagate in the waveguide $\beta$ must satisfy $n_{clad} k_o \lt \beta \lt n_{core} k_o$. Here are two interpretations:

1. $\beta$ is primarily determined by the core since that's where it is concentrated the most. The wavevector in the core can be written as $k^2_{y} = k^2_o n^2_{core} - \beta^2$. In the cladding it can be written as $k^2_{y} = k^2_o n^2_{clad} - \beta^2$. They must share the same longitudinal component and if the cores index is high enough then it is possible for $k_y$ in the cladding to be imaginary resulting in an evanescent wave. This is total internal reflection!
2. Coming from the other way around, it's clear that the field in the cladding has to be an evanescent wave. Otherwise the field would be non-zero at infinity which would break the entire point of trying to guide the wave somewhere.

In the core $\beta \lt k$ and in the cladding $\beta \gt k$. This will result in the following solutions to $(6)$: $$u_{core}(y)=A_{core}\sin(k_cy) + B_{core}\cos(k_cy) \qquad...(7)$$ $$u_{clad}(y) = A_{clad}e^{\alpha y} + B_{clad}e^{-\alpha y} \qquad...(8)$$
Where $\alpha^2 = \beta^2 - k^2$ can be written in terms of the mode angle:
$$\alpha^2=n^2_1k_o^2 \cos^2{\theta_m}-n^2_2k^2_o=k_o^2\left(n^2_1 \cos^2{\theta_m-n^2_2}\right)=n_2^2 k_o^2\left(\frac{n^2_1}{n^2_2}\cos^2{\theta_m}-1\right)=n_2^2 k_o^2 \left(\frac{\cos^2{\theta_m}}{\cos^2{\overline{\theta}_m}}-1\right)$$
Where $\cos{\overline{\theta}_m}=\frac{n_2}{n_1}$
$$\alpha=n_2k_o \sqrt{\frac{\cos^2{\theta_m}}{\cos^2{\overline{\theta}_m}}-1}$$
As $\theta_m$ increases then $\alpha$ will decrease, meaning that the field will penetrate deeper into the cladding. Higher order modes aren't as confined to the core of the waveguide.


$k_c$ is just the y component of the wavevector, so $k_c = k\sin{\theta_m} = \frac{2\pi}{\lambda}\sin{\theta_m}$.

$$u_{core}(y) \propto \begin{cases}
\cos(\frac{2\pi}{\lambda}\sin{\theta_m}y), \quad m = 0,2,4,... \\
\sin(\frac{2\pi}{\lambda}\sin{\theta_m}y), \quad m = 1, 3, 5, ...
\end{cases} \qquad \frac{-d}{2}\le y \le \frac{d}{2}$$
$$u_{clad}(y) \propto \begin{cases}
e^{-\alpha y}, {\quad y \ge \frac{d}{2}} \\
e^{\alpha y}, \quad y \le -\frac{d}{2}
\end{cases}$$
The proportionality constants can be solved for by using the normalization. $$\int_{-\infty}^{\infty}u^2(y)dy=1$$ **I'll use this to confirm the amplitudes of the mode in simulation.**

**Dispersion Relation**
Writing the self consistency condition in terms of $\beta$ and $\omega$ will yield the dispersion relation.
$$k_yd - \varphi=\pi m \qquad...(9)$$
$k_y$ can be written as $k_y = \sqrt{k^2 - \beta^2} = \sqrt{\frac{\omega^2}{c_1^2}-\beta^2} \quad$
And $\varphi$ can also be written in terms of $\beta$ and $\omega$. Plugging $\cos{\theta}=\frac{\beta}{\frac{\omega}{c_1}}$ and $\cos{\overline{\theta}_m}=\frac{n_2}{n_1}=\frac{c_1}{c_2}$ into $(2)$ $$\tan^2\left(\frac{\varphi}{2}\right)=\frac{\beta^2-\frac{\omega^2}{c_2^2}}{\frac{\omega^2}{c_1^2}-\beta^2}$$
Plugging these results into $(9)$
$$\tan^2\left(\frac{d}{2}\sqrt{\frac{\omega^2}{c_1^2}-\beta^2}-m\frac{\pi}{2}\right)=\frac{\beta^2-\frac{\omega^2}{c_2^2}}{\frac{\omega^2}{c_1^2}-\beta^2} \qquad...(10)$$

**Simulation**
The goal is to make a single mode $Si$ $SiO_2$ waveguide that supports 2 modes at 1550nm. The refractive index of $Si$ is $n_{Si} = 3.4$ and the refractive index of $SiO_2$ is $n_{SiO_2} = 1.46$. Solving for the NA: $$NA = \sqrt{n_{Si}^2-n_{SiO_2}^2}=3.07$$
The number of modes can be calculated as $$M \doteq \frac{2d}{\lambda_o}NA$$
The waveguide thickness to support the first mode must be $d = 252 nm$ and $d = 505nm$ for the second mode. So the waveguide thickness has the constraint $d \ge 252nm$. I'll choose the thickness to be $d = 200nm$. 

I'm interested to see what the propagation constant will be. The self-consistency condition can be written in terms of the NA. $$\sin(\overline{\theta}_c)=\sin(90\degree - \theta_c)=\cos(\theta_c) \qquad...(I)$$
$$\sin^2(\theta_c)+\cos^2(\theta_c)=1$$
$$\cos^2(\theta_c)=1-\sin^2(\theta_c)=1-\frac{n_{SiO_2}^2}{n_{Si}^2}=\frac{n_{Si}^2-n_{SiO_2}^2}{n_{Si}^2}=\frac{NA^2}{n_{Si}^2} \qquad ...(II)$$
Combining $(I)$ into $(II)$
$$\sin^2(\overline{\theta}_c)=\frac{NA^2}{n_{Si}^2}$$
And the self consistency condition will be expressed as $$\tan{(\pi\frac{d}{\lambda}\sin{\theta}-m\frac{\pi}{2})=\sqrt{\frac{NA^2}{n_{Si}^2\sin^2{\theta}}-1}} \qquad...(11)$$
Plotting this for the waveguide parameters:
![[Pasted image 20260805175749.png]]

So this is a single mode fiber with a bounce angle $\sin(\theta) \approx 0.61$. The propagation constant can easy be calculated as such: $$\beta=k_on_{Si}\cos(\theta)$$
$$\beta^2=k_o^2n_{Si}^2\cos^2{\theta}=k_o^2n_{Si}^2\left(1-\sin^2\theta\right)$$
$$\beta=\frac{2\pi}{\lambda_o} n_{Si}\sqrt{1-\sin^2{\theta}}=11.28\mu m^{-1}$$
And the effective index can be calculated as $n_{eff} = \frac{\beta}{k_o}=2.7$. The waveguide was simulated in Lumerical. The simulated effective index is $n_{eff,sim} = 2.702$. Pretty much the same thing ;)

Here is the mode profile:
![[Pasted image 20260805222328.png]]
This is for the m = 0 mode which matches the symmetric shape predicted in the equation for $u_{core}(y)$ and $u_{clad}(y)$. 

The phase velocity/group velocity can be found using the dispersion relation $(11)$. Another transcendental equation will be obtained by taking the derivative of this equation so I'll just plot $\beta$ against $\omega$ and use that. ***(use matlab instead itll be so much easier to plot)***

***Once you obtain that plot compare it against what Lumerical is spitting out:***
