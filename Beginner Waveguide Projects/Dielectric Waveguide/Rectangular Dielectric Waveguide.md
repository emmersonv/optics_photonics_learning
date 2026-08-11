**Effective Index Method**
The effective index method will collapse a 2D geometry into two 1D planar geometries. Take a rectangular $Si$ waveguide surrounded by $SiO_2$. The waveguide can be split into two sections, a y-independent section and a x-independent section. The TE/TM mode will be defined for one of the direction and the effective index will be found. This index will be used to solve the next section and that effective index will be the parameter for the entire waveguide.
*Add photos to make it a bit more clear*

**Rectangular Waveguide Analysis**
Take the effective obtained from the Planar Dielectric Waveguide and treat it as the core for the next section where the cladding is still $SiO_2$. This was solved assuming a TE polarization, however since the orientation of the waveguide is flipped for the other section the E-field is now perpendicular to the boundary, so the TM solution must be used to get the waveguide parameters.

Starting with the Helmholtz equation for the magnetic field $$\nabla^2\vec H +k^2 \vec H = 0 \qquad...(1)$$
The field should propagate down the waveguide with some field profile in the $y$ direction **(add a photo)**, so the solution is assumed to be $$\vec H = H_x(y)e^{j(\omega t - \beta z)} \qquad...(2)$$
Plugging $(2)$ into $(1)$ will yield the following result: $$\frac{d^2H_x(y)}{dy^2}+\left(k^2-\beta^2\right)H_x(y)=0$$
Where $k^2 - \beta^2$ can be written as $k_y^2$ $$\frac{d^2H_x(y)}{dy^2}+k_y^2H_x(y)=0 \qquad...(3)$$
This will yield the same form of solutions as the TE case, however we are interested in the E-field distributions. The electric field is related to the magnetic field by Ampere's Law: $$\nabla \times \vec H = \epsilon\frac{\partial \vec E}{\partial t} = j\omega \epsilon \vec  E \qquad...(4)$$
Calculating the cross product of the $H$ field results in $$\nabla \times \vec H = \frac{\partial H_x}{\partial z}\hat{y} - \frac{\partial H_x}{\partial y}\hat{z}=-j\beta H_x(y) e^{j(\omegat-)}$$


The self consistency condition for the TM polarization is $$\tan{(\pi\frac{d}{\lambda}\sin{\theta}-m\frac{\pi}{2})=\frac{n_{SiO_2}^2}{n_{eff}^2}\sqrt{\frac{\sin^2{\overline{\theta}_c}}{\sin^2{\theta}}-1}} \qquad...(1)$$
Solving this for the same width $d$ will yield $\sin\theta = 0.425$, $\beta = 9.91$, and $n_{eff} = 2.44$.

