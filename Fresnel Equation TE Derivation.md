*Consider* a dielectric interface with refractive indices of $n_1$ and $n_2$. Some oblique plane wave is incident on this interface and some of the fields are transmitted and reflected.
![[Pasted image 20260719151315.png]]
The goal is to find how much of the incident field is reflected and transmitted. I know through experiment that the angle that the beam is in and the refractive indices affects these quantities. So I will consider what happens at the boundary between the two materials. Starting with the boundary conditions:
$$\vec{E}_{1t}=\vec{E}_{2t}$$
$$\vec{H}_{1t}=\vec{H}_{2t}$$
Of course assuming that there is no free charge and current density at the boundary.

The tangential E-fields are calculated: $$\vec{E}_i + \vec{E}_r = \vec{E}_t \qquad ...(1)$$
And the tangential magnetic fields are calculated: $$\vec{H}_i \cos{\theta_1} - \vec{H}_r \cos{\theta_1}=\vec{H}_t \cos{\theta_2}$$
The E and H fields are related through the wave impedance $\eta$ which can be described as a scaled vacuum impedance $\eta = \frac{\eta_o}{n}$. 
$$\frac{\vec{E}_i}{\eta_1}\cos{\theta_1}-\frac{\vec{E}_r}{\eta_1}\cos{\theta_1}=\frac{\vec{E}_t}{\eta_2}\cos{\theta_2}$$
$$n_1\vec{E}_i\cos{\theta_1}-n_1\vec{E}_r\cos{\theta_1}=n_2\vec{E}_t\cos{\theta_2} \qquad ...(2)$$
It's assumed that $\vec{E}_i$ is known because we are the god-like figures producing that field. Plugging $(1)$ into $(2)$ we can find the reflected E-field. $$\vec{E}_r = \frac{n_1\cos{\theta_1}-n_2\cos{\theta_2}}{n_1\cos{\theta_1}+n_2\cos{\theta_2}}\vec{E_i}$$
$$r=\frac{\vec{E}_r}{\vec{E}_i}=\frac{n_1\cos{\theta_1}-n_2\cos{\theta_2}}{n_1\cos{\theta_1}+n_2\cos{\theta_2}} \qquad...(3)$$
And the same can be done to find the transmitted E-field:
$$\vec{E}_t=\frac{2 n_1 \cos{\theta_1}}{n_1 \cos{\theta_1} + n_2 \cos{\theta_2}} \vec{E}_i$$
$$t=\frac{\vec{E}_t}{\vec{E_i}}=\frac{2 n_1 \cos{\theta_1}}{n_1 \cos{\theta_1} + n_2 \cos{\theta_2}} \qquad...(4)$$

$\theta_1$ and $\theta_2$ are related trough Snell's law so Fresnel's equations can be described through only the incident angle.
$$n_1 \sin{\theta_1}=n_2 \sin{\theta_2}$$
$$n_1^2\sin^2{\theta_1}=n_2^2\sin^2{\theta_2}$$

$$\cos{\theta_2}=\sqrt{1-(\frac{n_1}{n_2})^2\sin^2{\theta_1}} \qquad...(5)$$
Plugging $(5)$ into $(3)$
$$r=\frac{n_1\cos{\theta_1}-n_2\sqrt{1-(\frac{n_1}{n_2})^2\sin^2{\theta_1}}}{n_1\cos{\theta_1}+n_2\sqrt{1-(\frac{n_1}{n_2})^2\sin^2{\theta_1}}} \qquad...(6)$$
Three cases will be considered. When $n_1 \lt n_2$, $n_1 \gt n_2$ when $\theta_1 \lt \theta_{crit}$, and $n_1 > n_2$ when $\theta_1 \gt \theta_{crit}$

In the first case $n_1 < n_2:$
Equation $(6)$ will always be real and negative corresponding to a phase shift of $\varphi = \pi$. 

In the second case $n_1 \gt n_2$ when $\theta_1 \lt \theta_{crit}:$
Rewriting Equation $(5)$ in terms of $\theta_{crit}$
$$\cos{\theta_2}=\sqrt{1-\frac{\sin^2{\theta_1}}{\sin^2{\theta_{crit}}}} \qquad...(7)$$
$\cos{\theta_2}$ will always be real and positive and $r$ will be real and positive.

In the third case $n_1 > n_2$ when $\theta_1 \gt \theta_{crit}:$
$$\cos{\theta_2}=-j\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1} \qquad...(8)$$
The reason the square root must be taken as negative is because for this condition total internal reflection will occur. The field cannot propagate into the second material so it will become an evanescent wave. As a result of this the reflection coefficient will be complex. Plugging $(8)$ into $(3):$
$$r=\frac{n_1\cos{\theta_1}+jn_2\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}}{n_1\cos{\theta_1}-jn_2\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}}$$
Defining some variables for cleanliness:
$$a=n_1\cos{\theta_1}$$
$$b=n_2\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}$$
$$r=\frac{a+jb}{a-jb}$$
Converting to polar form
$$r=\frac{\sqrt{a^2+b^2}e^{j\theta}}{\sqrt{a^2+b^2}e^{-j\theta}}=e^{j2\theta}$$
$$\theta=\tan^{-1}(\frac{b}{a}) \qquad...(9)$$
And the phase shift is found to be:
$$\varphi=2\theta \qquad...(10)$$
Substituting $(10)$ into $(9)$
$$\tan{(\frac{\varphi}{2})=\frac{b}{a}}=\frac{n_2\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}}{n_1\cos{\theta_1}}$$
$$n_2=n_1\sin{\theta_{crit}}$$
$$\tan{(\frac{\varphi}{2})=\frac{b}{a}}=\frac{n_1\sin{\theta_{crit}}\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}}{n_1\cos{\theta_1}}=\frac{\sin{\theta_{crit}}\sqrt{\frac{\sin^2{\theta_1}}{\sin^2\theta_{crit}}-1}}{\cos{\theta_1}}=\frac{\sqrt{\sin^2{\theta_1}-\sin^2{\theta_{crit}}}{}}{\cos{\theta_1}}$$
Using the identity
$$\sin^2{A}-\sin^2{B}=\cos^2{B}-\cos^2{A}$$
$$\tan{(\frac{\varphi}{2})}=\frac{\sqrt{\cos^2{\theta_{crit}}-\cos^2{\theta_1}}}{\cos{\theta_1}}=\sqrt{\frac{\cos^2{\theta_{crit}}-\cos^2{\theta_1}}{\cos^2{\theta_1}}}=\sqrt{\frac{\cos^2{\theta_{crit}}}{\cos^2{\theta_1}}-1}$$
The final result is: $$\tan{(\frac{\varphi}{2})}=\sqrt{\frac{\cos^2{\theta_{crit}}}{\cos^2{\theta_1}}-1}$$

