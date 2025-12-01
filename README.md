# Numerical Methods for PDEs: From 1D Linear Advection to the 2D Incompressible Navier–Stokes Equations
*A progression through foundational and advanced finite-difference methods for partial differential equations*

This repository contains a Jupyter notebook implementing a sequence of increasingly sophisticated numerical solvers for partial differential equations (PDEs). The project begins with the one-dimensional linear advection equation, advances to two-dimensional diffusion and Poisson equations, and culminates in a full solver for the two-dimensional incompressible Navier–Stokes equations using a projection (fractional-step) method. 

The notebook demonstrates the development of numerical PDE techniques in a principled, pedagogical progression that mirrors core material in scientific computing, applied mathematics, and computational fluid dynamics (CFD).

---

## 1. Overview of the Progression

This project is organized around three major stages:

### **Stage 1 — 1D Linear Advection Equation**
- Introduces finite difference methods
- Examines discretization in space and time
- Demonstrates stability considerations (CFL condition)
- Implements a central-difference advection scheme
- Evolves a Gaussian initial condition

### **Stage 2 — 2D Diffusion and Poisson Equations**
- Extends numerical methods to two spatial dimensions
- Uses the discrete Laplacian operator
- Solves the Poisson equation iteratively (Gauss–Seidel relaxation)
- Lays the foundation for pressure solves in the Navier–Stokes equations

### **Stage 3 — 2D Incompressible Navier–Stokes Equations**
- Implements the classical projection method
- Advances velocity fields using advection, diffusion, and pressure gradients
- Solves the pressure Poisson equation each timestep to enforce incompressibility
- Produces 2D velocity fields and streamlines
- Demonstrates the numerical structure of modern CFD algorithms

This structured progression highlights the mathematical and computational concepts that scale from basic 1D PDEs to full fluid dynamics simulations.

---

## 2. 1D Linear Advection Equation

The first part of the notebook considers the linear advection equation:

$u_t + c\,u_x = 0$

with constant advection speed $c$.

### **Numerical Scheme**
A central-difference discretization of the spatial derivative is used:

$u_i^{n+1} = u_i^n - c\,(dt / 2dx)\,(u_{i+1}^n - u_{i-1}^n)$.

A Gaussian initial condition is evolved forward in time, demonstrating:

- Numerical dispersion
- Stability sensitivity to the CFL condition $c\,dt/dx \leq 1$
- The role of spatial resolution in wave propagation

This stage introduces core ideas used later for nonlinear advection in Navier–Stokes.

---

## 3. 2D Diffusion and Poisson Equation

To prepare for incompressible flow computations, the notebook next implements the two-dimensional diffusion equation and the Poisson equation. 

### **Diffusion Equation**
The isotropic diffusion equation

$u_t = \kappa (u_{xx} + u_{yy})$

is discretized using:

- Forward Euler in time
- Central differences in space
- The 5-point Laplacian stencil

### **Poisson Equation**
The Poisson equation

$\nabla^2 p = f(x,y)$

is solved using iterative relaxation (Gauss–Seidel scheme). This solver becomes the core of the pressure projection step in the Navier–Stokes method.

This stage introduces:

- Construction of 2D Cartesian grids
- Boundary conditions for scalar fields
- Iterative elliptic solvers used widely in CFD and numerical PDEs

---

## 4. 2D Incompressible Navier–Stokes Solver

The final and most advanced portion of the notebook implements a complete solver for the incompressible Navier–Stokes equations:

$u_t + (u\cdot\nabla)u = -\nabla p + \nu \nabla^2 u$

$v_t + (u\cdot\nabla)v = -\nabla p + \nu \nabla^2 v$

$\nabla\cdot u = 0$.

### **Numerical Method: Projection (Fractional-Step) Method**

The solver follows three main steps each timestep:

#### **1. Compute the Intermediate Velocity**
Predictor step without pressure:

$u^\* = u^n + dt \Big[ - (u\cdot\nabla)u + \nu \nabla^2 u \Big]$

$v^\* = v^n + dt \Big[ - (u\cdot\nabla)v + \nu \nabla^2 v \Big]$.

#### **2. Solve the Pressure Poisson Equation**
The pressure ensures incompressibility:

$\nabla^2 p^{n+1} = \frac{1}{dt} (\nabla \cdot u^\*)$.

This is solved iteratively with the previously implemented Gauss–Seidel Poisson solver.

#### **3. Correct the Velocity Field**
The final divergence-free velocity is:

$u^{n+1} = u^\* - dt\, p_x$

$v^{n+1} = v^\* - dt\, p_y$.

### **Visualization**
The notebook produces:

- 2D contour plots of pressure
- Streamlines of the velocity field
- Vector-field plots (quiver-style)

These demonstrate correct incompressible flow behavior and the impact of pressure projection.

---

## 5. Numerical Methods and Stability Considerations

Across the three stages, several important numerical concepts appear:

- Finite difference discretization in space and time
- CFL conditions for hyperbolic PDEs
- Stability limits for explicit diffusion
- Iterative methods for solving elliptic PDEs
- Pressure–velocity coupling via the projection method
- Handling boundary conditions in multi-dimensional PDEs

These concepts reflect standard methods in scientific computing, and their implementation forms an excellent foundation for more advanced simulation work.

---

### **Dependencies**
- Python 3.8+
- NumPy
- Matplotlib
- Jupyter Notebook
