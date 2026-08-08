The first thing in every script is to import meep, numpy, and matplotlib
```python
import meep as meep
import numpy as np
import matplotlib.pyplot as plt
```

We must define a computation cell for which the fields will be simulated in. A source will be placed on one end of the computation cell and we will observe the field propagation.
A cell of dimensions 16um x 8um x 0 um (x,y,z) is defined:
```python
cell = meep.Vector3(16,8,0)
```

Now the waveguide can be placed. Geometric objects can be defined shown [here](https://meep.readthedocs.io/en/latest/Python_User_Interface/#geometricobject). 

```python
geometry = [
    meep.Block(
        meep.Vector3(meep.inf, 1, meep.inf),
        center = meep.Vector3(),
        material = meep.Medium(epsilon = 12)
    )
]
```

Meep iterates over a list to define geometries. A slab waveguide with dimensions ∞ x 1 x ∞ is defined. Infinite dimensions are used to model an ideal slab waveguide.

Next the source is defined. It is defined [as such](https://meep.readthedocs.io/en/latest/Python_User_Interface/#source). A simple sinusoidal point source will be defined with [ContinuousSource](https://meep.readthedocs.io/en/latest/Python_User_Interface/#continuoussource).

```python
sources = [
    meep.Source(
        meep.ContinuousSource(frequency = 0.15),
        component = meep.Ez,
        center = meep.Vector3(-7,0)
    )
]
```

Something important to note is that the frequency is specified of units of `2πc` so the vacuum wavelength is 6.67μm or 2μm in the material.

The source should not be placed directly at the edge of the cell so that the boundary conditions do not interfere with the source.

Absorbing boundaries are added around the cell using [perfectly matched layers (PML)](https://meep.readthedocs.io/en/latest/Perfectly_Matched_Layer/). Without it a wave may reflect off of the cell boundary which is obviously not physical. With the PML the field will be perfectly absorbed at the boundary preserving accuracy ;)

```python
pml_layers = [meep.PML(1.0)]
```

Meep takes the structure and discretizes it space and time. The resolution is controllable by the variable `resolution` (who would've known). This gives the number of pixels per distance unit. The resolution is set to 10 pixels/μm which is also 67 pixels/wavelength, or 20 pixels/wavelength in the waveguide. In general **8 pixels/wavelength in the highest dielectric is sufficient**.

```python
resolution = 10
```

The last object to specify is `Simulation` which uses all the previously defined objects. [Details here](https://meep.readthedocs.io/en/latest/Python_User_Interface/#the-simulation-class)
```python
sim = meep.Simulation(
    cell_size = cell,
    boundary_layers = pml_layers,
    geometry = geometry,
    sources = sources,
    resolution = resolution
)
```

Now we can run the simulation until the desired timestep
```python
sim.run(until=200)
```

The dielectrics can be plotted as such:
```python
eps_data = sim.get_array(center=meep.Vector3(), size=cell, component=meep.Dielectric)
plt.figure()
plt.imshow(eps_data.transpose(), interpolation='spline36', cmap='binary') 
plt.axis('off') 
plt.show()
```
`eps_data` will get a grid of the dielectrics in an array thats compatible with NumPy. We are interested in what the waveguide looks like so we the dielectric component is specified. 
Meep returns the grid in (x, y) but matplotlib expects it in (y, x) so the eps_data grid is transposed. The interpolation is not necessary but it makes it look a bit smoother. It'll be useful when curves are drawn.

The electric field is plotted similarly.
```python
ez_data = sim.get_array(center=meep.Vector3(), size=cell, component=meep.Ez)
plt.figure()
plt.imshow(eps_data.transpose(), interpolation='spline36', cmap='binary')
plt.imshow(ez_data.transpose(), interpolation='spline36', cmap='RdBu', alpha=0.9) 
plt.axis('off') 
plt.show()
```

The two plots are finally generated ;)

![[Pasted image 20260514032328.png]]
![[Pasted image 20260514032344.png]]

Next I'd like to see an animation of the propagating field
I used ffmpeg to generate the mp4 file. I could also generate gifs if I wanted

```python
sim.use_output_directory()

sim.run(
    meep.at_every(0.1, meep.output_png(meep.Ez, "-Zc dkbluered"), meep.output_efield_z),
    until=200
)

for f in glob.glob("simple_waveguide-out/*.h5"):
    os.remove(f)

cmd = [
    "ffmpeg",
    "-framerate", "10",
    "-pattern_type", "glob",
    "-i", "simple_waveguide-out/*.png",
    "-crf", "18",
    "-vf", "scale=iw*4:ih*4:flags=neighbor",
    "-c:v", "libx264",
    "-pix_fmt", "yuv420p",
    "propagation.mp4"
]

subprocess.run(cmd, check=True)

for f in glob.glob("simple_waveguide-out/*.png"):
    os.remove(f)
```
This will generate png images in a new directory, generate a mp4 video and delete all the png files afterwards.