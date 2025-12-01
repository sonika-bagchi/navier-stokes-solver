# Finite Difference Methods for the Numerical Solution of the Heat Equation
*A formal description of numerical experiments in one and two spatial dimensions*

This repository contains a Jupyter notebook implementing explicit finite difference schemes for the numerical approximation of the heat (diffusion) equation in one and two spatial dimensions. The work includes the formulation of the discrete problem, stability considerations, several classes of initial data, and animations illustrating the temporal evolution of the solution. The notebook serves as a computational study in classical parabolic partial differential equations and explicit time-marching methods.

---

## 1. Mathematical Formulation

### 1.1 The Heat Equation in One Dimension

We consider the initial-boundary value problem
\[
\frac{\partial u}{\partial t} = \kappa \frac{\partial^2 u}{\partial x^2}, 
\qquad x \in [0,L], \quad t \ge 0,
\]
with prescribed Dirichlet boundary conditions
\[
u(0,t) = c_1,\qquad u(L,t) = c_2,
\]
and an initial condition \(u(x,0) = f(x)\).

### 1.2 The Heat Equation in Two Dimensions

In two spatial dimensions, the governing equation is
\[
\frac{\partial u}{\partial t} 
= \kappa \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} \right),
\qquad (x,y)\in [0,L_x]\times[0,L_y],\; t\ge 0,
\]
again with Dirichlet boundary data and a specified initial temperature field \(u(x,y,0) = f(x,y)\).

Both models describe the diffusion of heat in homogeneous, isotropic media.

---

## 2. Numerical Discretization

### 2.1 Spatial and Temporal Grids

For the one-dimensional case, the domain is discretized into \(N_x + 1\) grid points with uniform spacing
\[
\Delta x = \frac{L}{N_x}.
\]
The temporal domain is discretized as  
\[
t_n = n\Delta t,\quad n = 0,1,\ldots,N_t.
\]

For the two-dimensional case, uniform Cartesian grids with spacings \(\Delta x\) and \(\Delta y\) are used.

### 2.2 Finite Difference Scheme (FTCS)

The notebook implements the Forward Time, Centered Space (FTCS) explicit method. In one dimension, the update rule is
\[
u_i^{n+1} = u_i^n 
+ \kappa \frac{\Delta t}{\Delta x^2}\left( u_{i+1}^n - 2u_i^n + u_{i-1}^n \right).
\]

In two dimensions, the standard five-point Laplacian stencil is used:
\[
u_{i,j}^{n+1} = u_{i,j}^n
+ \kappa \Delta t\left(
\frac{u_{i+1,j}^n - 2u_{i,j}^n + u_{i-1,j}^n}{\Delta x^2}
+
\frac{u_{i,j+1}^n - 2u_{i,j}^n + u_{i,j-1}^n}{\Delta y^2}
\right).
\]

### 2.3 Stability Condition

The FTCS method is conditionally stable. For the one-dimensional case,
\[
\Delta t \le \frac{\Delta x^2}{2\kappa}.
\]

For two dimensions, the sufficient condition becomes
\[
\Delta t \le \frac{1}{4\kappa}\,\min\{\Delta x^2,\;\Delta y^2\}.
\]

The notebook automatically evaluates these conditions and reports whether the chosen discretization satisfies them.

---

## 3. Initial Conditions Implemented

Several initializations are included to illustrate distinct diffusion behaviors.

### 3.1 One-Dimensional Heated-End Configuration (Primary Simulation)

The first simulation models a rod with elevated temperatures at both ends:
\[
u(0,0) = u(L,0) = 500,\qquad 
u(x,0) = 0 \ \text{for} \ 0 < x < L.
\]
The Dirichlet boundary values remain fixed at 500 for all time. This configuration produces symmetric inward heat propagation.

### 3.2 One-Dimensional Gaussian Initial Condition

A second simulation employs a smooth initial condition:
\[
u(x,0) = \exp\!\left(-\frac{(x - L/2)^2}{2\sigma^2}\right),
\]
with boundary values held constant at their initial endpoints.

### 3.3 Two-Dimensional Gaussian Initial Condition

A radially symmetric Gaussian profile serves as the initial condition:
\[
u(x,y,0) = A \exp\!\left(-\frac{(x-x_0)^2 + (y-y_0)^2}{2\sigma^2}\right),
\]
demonstrating isotropic diffusion on a rectangular grid.

### 3.4 Two-Dimensional Constant Initial Condition

A uniform initial temperature distribution evolves under the same explicit update, allowing visualization of diffusion under homogeneous initial data.

---

## 4. Computational Implementation

The notebook uses:

- **NumPy** for vectorized numerical updates  
- **Matplotlib** for visualization and animation  
- **HTML5 video export** for reliable display of time evolution  
- Efficient slicing operations for interior-grid updates in 1D and 2D  
- Automatic construction of simulation arrays sized according to discretization parameters  

All computations are performed in pure Python without external PDE libraries, providing a transparent view of the underlying numerical scheme.

---

## 5. Visualization of Solutions

Animations are generated for all simulations, including:

- 1D time-evolving line plots  
- 1D space–time heatmaps  
- 2D animated heatmaps showing full spatial evolution  

These visualizations provide qualitative confirmation of expected diffusive behavior, such as smoothing of discontinuities, inward propagation from high-temperature boundaries, and radial spreading of Gaussian profiles.

---

## 6. Reproducibility

### Dependencies
- Python 3.8+  
- NumPy  
- Matplotlib  
- Jupyter Notebook  

### Execution
Run:
```bash
jupyter notebook
