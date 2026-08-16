When light is channeled through a waveguide the entire field isn't contained in the core since the boundary conditions of a dielectric does not force the tangential fields to be 0. As a result some of the fields will spill out into the cladding where the attenuation constant $\alpha$ describes the distance for which the field will drop by a factor of $e^{-1}$. If another waveguide is placed in this region then the two waveguides will couple.

The amplitudes of the fields in the two waveguides are governed by the two coupled differential equations
$$\frac{da_1}{dz}=-j\kappa_{21}e^{j\Delta\beta z}a_2(z)$$
$$\frac{da_1}{dz}=-j\kappa_{12}e^{j\Delta\beta z}a_1(z)$$
Where $\Delta\beta = \beta_1 - \beta_2$ and $$\kappa_{21} = \frac{1}{2}\left(n_2^2-n^2\right)\frac{k_o^2}{\beta_1}\int_a^{a+d}u_1(y)u_2(y)dy$$
$$\kappa_{21} = \frac{1}{2}\left(n_1^2-n^2\right)\frac{k_o^2}{\beta_2}\int_{-a-d}^{-a}u_2(y)u_1(y)dy$$
$\kappa_{21}$ and $\kappa_{12}$ are the coupling coefficients between the two waveguides. *derive this another time, for now just use these results*
The integral is a result from the projection of the mode of one waveguide to the other waveguide over the region that's being perturbed. $2a$ is the distance between cores and $d$ is the width of the waveguides. 

So how does the attenuation constant $$