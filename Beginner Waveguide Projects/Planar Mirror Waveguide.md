From the ray optics point of view mirrors can be used to reflect a ray to guide it to the desired position. This idea is revisited at the viewpoints of wave optics. 

**Perfect mirror boundary condition**
Ideal mirrors are modeled as perfect electric conductors (PECs) since there is no transmission or absorption. First lets discuss the boundary conditions of ideal mirrors:

The tangential electric field must be 0. $$E_{\parallel} = 0$$If you consider an infinite sheet of a PEC then any tangential E-field will cause a infinite current. If a finite sheet is considered then there will be charge buildup at the end of the sheet and will eventually cancel the tangential field.

**Modes**
So, two mirrors are parallel and are separated by a distance d. When some TE plane wave is injected it will reflect off one of the mirrors and will gain a phase of π. This is because the reflected wave needs to eliminate the incident field at the interface as to satisfy the tangential electric field boundary condition. For a stable wave to propagate through the waveguide the incident and reflected waves must constructively interfere perfectly. If it does not then some portion of the field will cancel as the waves travel through the waveguide and eventually vanish.

There are a few ways to model this. *Fundamentals of Photonics, Saleh* uses a self-consistency approach. After the wave reflects twice it should reproduce itself. See the figure below to see what I mean. The incident wave phasefront must match with the twice-reflected wave phasefront. Fields that satisfy this condition are known as modes. 
*Modes are fields that maintain the same transverse distribution and polarization at all locations along the waveguide axis (Saleh)*![[Pasted image 20260627191002.png]]
The phase difference between B and C should be some integer of 2π so the phases at B and C are found and the difference is then taken. After some trig the self-consistency condition is found. $$\sin\theta_{m}=m\frac{\lambda}{2d}, \qquad m=1,2,...$$
For a given frequency only certain angles will be supported. Since sine obviously can't exceed 1 the waveguide will also only support a limited number of modes.

This means the wavevectors are quantized. The upwards/downwards wavevectors are broken into its components. 
$$k_{y}=nk_{o}\sin\theta_{m}=\frac{2\pi}{\lambda}\sin\theta_{m}=m\frac{\pi}{d}$$
Similarly for the z component $$k_{z}=\beta=k\cos\theta_{m}$$$$\beta^2=k^2cos^2\theta_{m}=k^2(1-\sin^2\theta_{m})=k^2-\frac{m^2\pi^2}{d^2}$$
**Field Distribution**

Now that we found the condition required for some field that a waveguide is happy to carry along the field distribution inside of it is of interest. There will be two fields in the waveguide, a plane wave that propagates in the $(0, k_{y}, \beta_{z})$ direction and another in the $(0, -k_{y}, \beta_{z})$ direction. The upwards wave is defined as such. It is assumed that $A_{m}$ is defined. (Maybe because this is the wave thats being injected?)$$E_{x}^+(y,z)=A_{m}e^{-jk_{y}y-j\beta_{m} z}$$
The total field in the waveguide is the superposition of the upwards and downwards wave. $$E_{x}(y,z)=E_{x}^++E_{x}^-=A_{m}e^{-jk_{y}y-j\beta_{m} z} + Be^{jk_{y}y-j\beta_{m} z}$$ The coefficient B must be solved. The boundary conditions are applied once again and B is found to be: $$B=e^{-j(m-1)\pi}A_m$$What's interesting is if $m=1$ is selected then the downwards wave will have no accumulated phase relative to the upwards wave. *Let me try to unpack why:* The downwards wave comes from the reflection of the incident wave, so it will obtain a phase $e^{j\pi}$. Afterwards it will propagate back towards the center of the waveguide and will obtain a phase of: $$e^{-jk_{y}\frac{d}{2}}=e^{-jm\pi}=e^{-j\pi}$$ So the accumulated phases actually cancel out.

The total field in the waveguide is follows $$E_{x}(y,z)=A_{m}e^{-jk_{y}y-j\beta_{m} z} + e^{-j(m-1)\pi}A_{m}e^{jk_{y}y-j\beta_{m} z}$$
I didn't do the math on my tablet so I'll write out the math on here. You're welcome :)
$$E_{x}(y,z)=A_{m}e^{-j\beta_{m}z}[e^{-jk_{y}y}+e^{-j(m-1)\pi}e^{jk_{y}y}]$$
For odd m: $$E_{x}(y,z)=A_{m}e^{-j\beta_{m}z}[e^{-jk_{y}y}+e^{jk_{y}y}]=2A_{m}\cos(k_{y}y)e^{-j\beta_{m}z}$$
And for even m:
$$E_{x}(y,z)=A_{m}e^{-j\beta_{m}z}[e^{-jk_{y}y}-e^{jk_{y}y}]=2jA_{m}\sin(k_{y}y)e^{-j\beta_{m}z}$$

The complex amplitude is written in the form $$E_{x}(y,z)=a_{m}u_{m}(y)e^{-j\beta_{m}z}$$ where $$u_{m}(y)=
\begin{cases}
A\cos(m\pi\frac{y}{d}), \qquad m = 1,3,5,...
\\
Bsin(m\pi\frac{y}{d}), \qquad m = 2,4,6,...
\end{cases}$$
$u_{m}(y)$ is normalized to satisfy $$\int_{-\frac{d}{2}}^{\frac{d}{2}}u_{m}^2(y)dy=1$$ Simply plug that bad boy in and the result is $$A = B = \sqrt{\frac{2}{d}}$$ The field coefficient must work out to $2A_{m}$ and $2jA_{m}$ in the odd and even mode, respectively. As such $a_{m}$ is chosen to be $a_{m}=\sqrt{2d}A_{m}$ for the odd mode and $a_{m}=j\sqrt{2d}A_{m}$ for the even mode.

The field distribution $a_{m}$ is shown to give a nice mental picture. As the mode $m$ will vary in the transverse plane at a greater $k_{y}$.
![[Pasted image 20260628014225.png]]


**Simulation**
From here on I'm going to stick with Lumerical. It's much faster to construct geometry.
I will generate a waveguide where $d=1{\mu}m$

![[Pasted image 20260705224920.png]]
A few things are at play here. First I placed a rectangular structure with a width of 1um and a refractive index of $n=1.4$. A 2D FDTD simulation region was placed on a cross section of the waveguide in the XY plane. PML layers were placed on the left and right sides of the structure to emulate an infinite waveguide and metal boundaries are set above and below the simulation region. 
The mesh works best when it is larger than the FDTD simulation region (I did not look into why this is the case) and two ports, input and output, are placed away from the PML layer to avoid overmeshing (i think thats where its called?)

I would like to see the mode profiles, but before I do that let me find out how many modes that this waveguide supports. 

From the self-consistency equation: $$M\underset{\cdot}{=}\frac{2d}{\lambda}$$
Where $\underset{\cdot}{=}$ is reduced to the nearest integer. $\lambda$ denotes the wavelength in the medium, but in Lumerical a global wavelength is defined so lets define it as such in this equation.
$$\lambda=\frac{\lambda_o}{n}$$
$$M=n\frac{2d}{\lambda_o}=1.4\frac{2(1{\mu}m)}{1{\mu}m}=2.8\underset{\cdot}{=}2$$
Which explains why any $M$ greater than $M=3$ has large attenuation. The mode isn't supported!

Anyways, the fundamental TE mode is injected and the field profile is plotted:
![[Pasted image 20260706222635.png]]
The half-sinusoid shape along the y axis is exactly what we expect ;) Plotting a slice of x just to confirm the field profile:
![[Pasted image 20260706222927.png]]

