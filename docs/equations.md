# Equations 

## Variables 

As of 2024, the Dyablo Whole-Sun branch solves the magnetohydrodynamics equations with viscosity and thermal conduction. The code evolves a set of equations expressed as conservative variables $\mathbf{U}$ or primitive variables $\mathbf{Q}$. 

The **conservative variables** are the following : 

$$
\mathbf{U} = [\rho, \rho \mathbf{u}, E_{tot}, \mathbf{B}]^T
$$

with $\rho$ the density, $\mathbf{u}$ the fluid velocity, $E$, the total energy and $\mathbf{B}$ the magnetic field. The total energy is expressed as 

$$
E_{tot} = E_{kin} + E_{mag} + \rho e = \dfrac{1}{2}\rho\mathbf{u}\cdot\mathbf{u} + \dfrac{1}{2}\mathbf{B}\cdot\mathbf{B} + \rho e
$$

Where $e$ is the internal energy defined by the equation of state.

The **primitive variables** are defined as

$$
\mathbf{Q} = [\rho, \mathbf{u}, P_{tot}, \mathbf{B}]^T
$$

where $P_tot$ is the total pressure, defined as the sum of the fluid pressure $P$ and the magnetic pressure:

$$
P_{tot} = P + P_{mag} = P + \dfrac{1}{2}\mathbf{B}\cdot\mathbf{B}
$$

The conversion between the primitive and conservative variable is straight-forward except for the conversion between the total energy term and the total pressure term which requires an **equation of state**. For an **ideal gas**, we use the following relation : 

$$
e = \dfrac{P}{\rho(\gamma-1)}
$$

with $\gamma$ the specific heat ratio.

## Equations

The equations solved are generally of the form of conservation equations with source terms : 

$$
\dfrac{\partial \mathbf{U}}{\partial t} + \nabla \cdot \mathbf{F}(\mathbf{U}) = \mathbf{S}(\mathbf{U})
$$

where $\mathbf{F}$ is a flux expressed as a function of the conservative variables and $\mathbf{S}$ a source term.

More precisely, the Whole-Sun branch evolves the following equations:

 1. Conservation of Mass
$$
\dfrac{\partial \rho}{\partial t} + \nabla\cdot \rho\mathbf{u} = 0
$$

 2. Conservation of momentum
$$
\dfrac{\partial \rho\mathbf{u}}{\partial t} + \nabla \cdot (\rho\mathbf{u}\otimes\mathbf{u} - \mathbf{B}\otimes\mathbf{B} + P_{tot}\mathbb{I} - \tau) = \rho\mathbf{g}
$$

where $\mathbb{I}$ is the identity matrix, $\tau$ the viscosity tensor and $\mathbf{g}$ the gravitational acceleration. The viscosity tensor is a $ndim\times ndim$ matrix whose elements are defined as follows : 

$$
\tau_{ij} = \mu \left(\dfrac{\partial u_i}{\partial x_j} + \dfrac{\partial u_j}{\partial x_i} - \delta_i^j\dfrac{2}{3}(\nabla \cdot \mathbf{u})\right)
$$

with $\delta_i^j$ being the Kroenecker delta and $\mu$ the (shear) dynamic viscosity coefficient. Bulk viscosity is set to zero for the moment.

 3. Conservation of energy
 $$
\dfrac{\partial E_{tot}}{\partial t} + \nabla\cdot([E_{tot}+P_{tot}]\mathbf{u} - \mathbf{B}(\mathbf{B}\cdot\mathbf{u}) - \tau\cdot\mathbf{u} - \kappa \nabla T) = \rho\mathbf{u}\cdot \mathbf{g}
 $$