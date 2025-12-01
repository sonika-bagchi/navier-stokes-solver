# Finite Difference Methods for the Numerical Solution of the Heat Equation
*A formal description of numerical experiments in one and two spatial dimensions*

This repository contains a Jupyter notebook implementing explicit finite difference schemes for the numerical approximation of the heat (diffusion) equation in one and two spatial dimensions. The work includes the formulation of the discrete problem, stability considerations, several classes of initial data, and animations illustrating the temporal evolution of the solution. The notebook serves as a computational study in classical parabolic partial differential equations and explicit time-marching methods.

---

## 1. Mathematical Formulation

### 1.1 The Heat Equation in One Dimension

We consider the initial-boundary value problem

**Heat equation (1D):**  
$u_t = \kappa\, u_{xx}$ for $x \in [0,L]$ and $t \ge 0$.

**Boundary conditions:**  
$u(0,t) = c_1$,  
$u(L,t) = c_2$.

**Initial condition:**  
$u(x,0) = f(x)$.

### 1.2 The Heat Equation in Two Dimensions

**Heat equation (2D):**  
$u_t = \kappa (u_{xx} + u_{yy})$ for $(x,y)\in[0,L_x]\times[0,L_y]$, $t \ge 0$.

The initial condition is $u(x,y,0) = f(x,y)$, with Dirichlet boundary conditions applied on the domain boundary.

---

## 2. Numerical Discretization

### 2.1 Spatial and Temporal Grids

The domain $[0,L]$ is discretized with $N_x + 1$ uniformly spaced grid points:

$\Delta x = L / N_x$.

The temporal domain is discretized as $t_n = n\Delta t$, where $n = 0,\ldots,N_t$.

For 2D simulations, uniform Cartesian grids are used in both $x$ and $y$.

### 2.2 Finite Difference Scheme (FTCS)

The notebook implements the classical Forward Time, Centered Space (FTCS) explicit method.

**1D update rule:**  
$u_i^{n+1} = u_i^n + \kappa (\Delta t / \Delta x^2)(u_{i+1}^n - 2u_i^n + u_{i-1}^n)$.

**2D update rule:**  
$u_{i,j}^{n+1} = u_{i,j}^n + \kappa \Delta t\left[(u_{i+1,j}^n - 2u_{i,j}^n + u_{i-1,j}^n)/\Delta x^2 + (u_{i,j+1}^n - 2u_{i,j}^n + u_{i,j-1}^n)/\Delta y^2\right]$.

### 2.3 Stability Condition

For 1D, FTCS stability requires:

$\Delta t \le \Delta x^2 / (2\kappa)$.

For 2D, a sufficient stability condition is:

$\Delta t \le \min(\Delta x^2, \Delta y^2) / (4\kappa)$.

The notebook computes these conditions automatically and reports whether the chosen discretization is stable.

---

## 3. Initial Conditions Implemented

### 3.1 One-Dimensional Heated-End Configuration (Primary Simulation)

The first simulation models a rod whose endpoints are maintained at a fixed high temperature:

$u(0,0) = u(L,0) = 500$,  
$u(x,0) = 0$ for $0 < x < L$.

The boundary temperatures remain fixed at 500 for all $t > 0$, producing symmetric inward diffusion.

### 3.2 One-Dimensional Gaussian Initial Condition

$u(x,0) = \exp[-(x - L/2)^2 / (2\sigma^2)]$.

The boundary conditions remain constant throughout the simulation.

### 3.3 Two-Dimensional Gaussian Initial Condition

$u(x,y,0) = A\exp[-((x-x_0)^2 + (y-y_0)^2)/(2\sigma^2)]$.

This produces radially symmetric diffusion behavior.

### 3.4 Two-Dimensional Constant Initial Condition

A uniform initial temperature field is evolved using the same explicit scheme.

---

## 4. Computational Implementation

The notebook uses:

- NumPy for vectorized numerical operations  
- Matplotlib for static plots and animations  
- HTML5 video export for reliable visualization  
- Efficient slicing for interior-grid updates in both 1D and 2D  

All computations are implemented directly, without reliance on external PDE-solving libraries, providing transparency in the numerical scheme.

---

## 5. Visualization of Solutions

The simulations include:

- Time-evolving 1D line plots  
- Space–time heatmaps for 1D diffusion  
- Animated heatmaps for 2D simulations  

These visualizations clearly demonstrate characteristic diffusive behavior such as smoothing of discontinuities, inward propagation from heated boundaries, and radial spreading of Gaussian temperature profiles.

---

## 6. Reproducibility

### Dependencies

- Python 3.8+  
- NumPy  
- Matplotlib  
- Jupyter Notebook  
