# Chapter 2

## Basic Components and Units {#sct:model_components}




```{figure} .../images/git-new-file.png
:name: fig:cell_basic

A cell, the main unit of our simulation. It consists of a nucleus bead
in the center with $R_{nuc} = 10 R_c$, connected to the cortex beads
with $R_c$ by visible black microtubule springs with rest length
$L_{mt} = 40R_c$. The individual cortex beads are connected to each
other via cortex springs. Not shown are the springs for cell pressure,
which connect each bead to the nucleus to represent hydrostatic pressure
within a biological
cell.
```

This model is a very simple and crude approximation of an epithelial
cell, consisting of beads and Hookean springs, as seen in figure
[1](#fig:cell_basic){reference-type="ref" reference="fig:cell_basic"}.
The center of our cell is occupied by a large nuclear bead, while we
represent the cell cortex by a number of smaller cortex beads. For these
simulations, we use $N_{beads} = 50$ as our default number of beads in a
membrane. The basic unit of length in our system is the radius of the
cortex beads, $R_c$.

Several sets of Hookean springs work to hold the cell together. The
nucleus is connected to cortex beads via long springs representing
microtubules, with a default value $L_{mt} = 40 R_c$. While in a
stationary model usually all cortex beads are connected to the nucleus,
for simulating a moving cell the number of microtubules must be limited,
as will be explained in [1.4](#){reference-type="ref" reference=""} . To
ensure the cell keeps its shape even in areas with low microtubule
density, pressure springs ($L_p = 40 R_c$) were introduced to mimic the
effects of hydrostatic pressure within a biological cell. Finally,
cortex springs connect neighbouring cortex beads. The rest length of
these springs is calculated by $L_c = 0.01 \pi L_{mt} / N_{beads}$ to
ensure even spacing for all choices of $N_{beads}$ and $L_{mt}$.

Each spring has a characteristic stiffness value $k$. By definition we
take the default stiffness of the cortex springs to be our unit for
stiffness, i.e. $K_c = 1 k_c$. In practise, we will often use a
different value for the cortex spring stiffness $K_c$ than our defined
$k_c$. The default values for microtubule stiffness $k_{mt}$ and
pressure stiffness $k_{p}$ are $k_{mt} = 0.5 k_c$ and $k_{p} = 0.1k_c$,
though they were changed for some simulation runs.

## Forces and Bead Positioning

### Hookean and Drag Forces in Different Dimensions

This crude model of a cell includes two forces acting between the
nucleus and cortex, and two additional forces acting between cortex
beads. To calculate the effect of these forces on the position of a
bead, we consider Hookes spring law for one dimension $$\label{eq:Hooke}
    \textbf{F} = -k \left( x - L\right)$$ where $k$ is the
characteristic spring stiffness, $x$ is the current bead position and
$L$ the spring rest length. However, due to the low Reynolds number and
hence relatively high viscosity of this system we also need to take into
account drag forces on the bead, represented by $$\label{eq:drag}
    \textbf{F}_{drag} = 6 \pi \eta R v$$ for a spherical body, with
$\eta$ the viscosity of our environment, $R$ the bead radius and $v$ the
bead velocity. Combining the equations
[\[eq:Hooke\]](#eq:Hooke){reference-type="ref" reference="eq:Hooke"} and
[\[eq:drag\]](#eq:drag){reference-type="ref" reference="eq:drag"} we can
write an equation of motion for our bead position $x$:
$$\label{eq:DE_for_position_1D}
    m \frac{d^2x}{dt^2} = -6\pi \eta R \frac{dx}{dt} - k\left(x-L\right).$$
A low Reynolds number allows us to disregard the inertial term (i.e. the
LHS of eq.
[\[eq:DE_for_position_1D\]](#eq:DE_for_position_1D){reference-type="ref"
reference="eq:DE_for_position_1D"}) and thus allowing us to solve for
$$x \approx e^{-t/\tau}, \quad\quad \tau = \frac{6\pi\eta R}{k}.$$ The
emergence of the characteristic timescale $\tau$ of the system gives us
the final base unit of the system, taking $tau = 1$ to be our measure of
time. [@Giri] computed the approximate value of $\tau$ in terms of
seconds to be $\tau = 0.003s$. For simulating our cells, we usually take
timesteps $\Delta t = 0.1 \tau$ and measure $\Delta t_{meas} = \tau$.

In multiple dimensions and with several forces, we can perform a similar
analysis. Using the equation of motion $$\label{eq:DE_for_position_2D}
    m \frac{d^2 \textbf{r}_i}{dt^2} = -6\pi \eta R_i \frac{d\textbf{r}_i}{dt} + \sum_j \textbf{F}_{ij}$$
where the subscript $i$ denotes the $i$th bead of the system, and
$\sum_j \textbf{F}_{ij}$ is the sum of all forces $F_j$ acting on that
bead. To solve this, we use numerical integration methods leading to
$$\label{eq:single_step}
    \textbf{r}_i \left(t + \Delta t\right) = \textbf{r} \left( t\right) + \frac{\sum_j \textbf{F}_{ij}}{6\pi\eta R_i}\Delta t$$

### Pressure

Although the pressure is implemented similarly to microtubules by using
a Hookean spring, the effective force a bead will experience due to
pressure will be slightly different. That is because in a biological
cell, the hydrostatic pressure is equal along the whole cell. As such,
the force $F_{p,eff}$ a bead will experience due to pressure is not the
force $F_{p,i}$ exerted by the local pressure spring. Instead, we take
the average over all springs
$$F_{p,eff} = \frac{1}{N_{beads}} \sum_i F_{p,i}$$ which is then
included in eq.
[\[eq:single_step\]](#eq:single_step){reference-type="ref"
reference="eq:single_step"} when adding up the forces acting on the bead
$i$.

### Bending Resistance

A final force which directly effects only the cortex beads is bending
resistence, which was implemented by . This force works to keep the
angle between two neighbouring cortex beads minimal, and is given by
$$\label{eq:Bend_resist}
    \textbf{F}_{bend} = \kappa \sin{\theta} \hat{\textbf{r}}$$ where
$\kappa$ is the cortex spring bending stiffness, $\theta$ the angle
between two neighbouring cortex beads and $\hat{\textbf{r}}$ the unit
vector pointing perpendicular to the vector between the two beads, as
seen in fig.

Note that the bending resistance pulls the bead to a different location
than microtubule and pressure springs do. The smallest deviation from
the equilibrium where all cortex beads are equally spaced with $L_{mt}$
and $L_c$ as given in section
[1.1](#sct:model_components){reference-type="ref"
reference="sct:model_components"} was found by Lucas de Kam [@Lucas] to
be $\frac{\kappa}{K_c} = 2.5$. The simulations are done with a default
value of $\kappa = 2.5 K_c$.

## Making the Cell Move

Cell movement was first implemented into this model by Giri et al.
[@Giri] and then further optimised by Lucas de Kam [@Lucas]. For a
moving cell, it is vital that only a subset of the cortex beads present
have a microtubule attached to them. The movement itself is achieved by
taking a cortex bead and inserting it at a different location determined
by the probability density function. This PDF is derived from the local
microtubule density, and thus we have a greater likelihood of bead
insertion near the front end of the cell, which is defined as the
section with most microtubules.

The displacement of the nucleus by bead insertion and deletion comes
from the tension forces caused by these events. Deletion of a bead
causes a contractile force between what used to be its neighboring
beads. At the location of insertion, the new neighbours are pushed away
into a new equilibrium position. These forces are translated to the
nucleus by the microtubule and pressure springs, and cause its movement.

In biological cells movement is caused by lamellipodia created by actin
filaments instead of microtubules. The reason for calling the
microtubule springs such is a remnant from the original model, which was
used to simulate a stationary, growing cell tissue, which relies
primarily on microtubules for keeping cell structure.

## Constraining Environments

The main environment simulated for this thesis was an array of spaced
pillars. These pillars are arranged in a triangular configuration, such
that the distance between the centers of any two neighboring pillars is
equidistant. We describe this distance by the parameter $d$. The nearest
distance between the boundaries of two neighbouring pillars is given by
$e$. .

![Three pillars with marked distances $d$ between the centers of two
neighbors, and $e$ between their
boundaries.](figures/array_geometry.png){#fig:array_geometry
width="0.5\\linewidth"}

The setup is modelled after Sadjadi et al. [@cmot2], who created
\"pillar forest chambers\" to study the movement of leukemia cells in
vitro. Using this paper as a reference, the default pillar radius was
set to $R_{pillar} = 40 R_c$, with an arrray side of
$L_{box} = 2000 R_c$ to allow ample space for migration. The pillar
spacing $d$ was varied between .

Cortex beads are prevented from entering an obstacle (i.e. a pillar or
wall) by pushing it to the nearest boundary of the object, should a bead
move into one.

The final setup is shown in figure
[3](#fig:cell_confined){reference-type="ref"
reference="fig:cell_confined"}.

![A cell in a pillared array, with $L_{box} = 2000R_c$,
$R_{pillar} = 40R_c$ and
$d = 200R_c$](figures/cell_in_pillared_confinement.png){#fig:cell_confined
width="0.7\\linewidth"}
