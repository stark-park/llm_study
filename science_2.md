> ### Q
> 1. What is the Kutta-Joukowski theorem?
> 2. Can you prove the Kutta-Joukowski theorem?

> ### A
> Kutta-Joukowski 정리  
> 44초 동안 생각

Below are a detailed explanation of the Kutta–Joukowski theorem and a sketch of a classical proof. While the full rigor might require more mathematical details, this outline captures the essence of standard derivations used in aerodynamics and potential flow theory.

---

**1. What is the Kutta–Joukowski Theorem?**

The Kutta–Joukowski theorem is a fundamental result in aerodynamics and fluid mechanics that relates the lift force acting on a two-dimensional body (such as an airfoil) to the circulation of the flow around it. In its simplest form, the theorem states:

\[
L' = \rho U \Gamma
\]

where:  
- \(L'\) is the lift force per unit span (force per unit length in the direction perpendicular to the free-stream velocity),  
- \(\rho\) is the density of the fluid,  
- \(U\) is the uniform free-stream velocity (far upstream), and  
- \(\Gamma\) is the circulation of the velocity field around the body.

Circulation \(\Gamma\) is defined by the line integral of the tangential component of the velocity field around a closed loop encircling the airfoil:

\[
\Gamma = \oint_C \mathbf{u} \cdot \mathbf{t}\, ds
\]

where \(C\) is a contour that loops once around the airfoil, \(\mathbf{u}\) is the velocity field, and \(\mathbf{t}\) is the unit tangent to the contour.

Physically, the Kutta–Joukowski theorem tells us that if there is a net circulation of flow around a body, it experiences a lift force. The sign and magnitude of the circulation determine the magnitude and direction of this lift.

---

**2. A Proof of the Kutta–Joukowski Theorem**

*Assumptions:*
1. **Steady, Inviscid, Incompressible, and Irrotational Flow:** We assume the flow around the airfoil can be modeled as a potential flow. Incompressibility implies that the velocity field \(\mathbf{u}\) can be expressed in terms of a velocity potential \(\phi\) with \(\nabla^2 \phi = 0\). Irrotationality implies that the circulation and vorticity are related in a certain way, and that away from boundaries, the flow is potential.
2. **Far-Field Conditions:** Far away from the airfoil, the flow is uniform with speed \(U\) in the \(x\)-direction, and the pressure approaches the freestream pressure \(p_\infty\).
3. **Kutta Condition (for an airfoil):** The chosen circulation is such that the flow leaves the trailing edge smoothly, ensuring a physically meaningful solution for the circulation. Though the Kutta condition is not strictly necessary for the statement of Kutta–Joukowski, it’s often invoked to determine the unique \(\Gamma\) for a given airfoil shape and angle of attack.

*Outline of the Proof:*

**Step 1: Momentum and Pressure Relations**  
Start with the steady form of the incompressible Euler equations. For a steady, inviscid flow, the momentum equation is:

\[
\rho (\mathbf{u} \cdot \nabla) \mathbf{u} = -\nabla p.
\]

This can be integrated along a streamline to give Bernoulli’s equation:

\[
\frac{p}{\rho} + \frac{|\mathbf{u}|^2}{2} = \text{constant on a streamline}.
\]

Because the flow is irrotational, this constant is the same throughout the entire flow field (not just along a single streamline) if we assume a simply connected domain outside the body.

**Step 2: Control Volume and Force on the Body**  
Consider a large control volume surrounding the airfoil. The lift force on the body can be related to the net momentum flux of the fluid. By applying the linear momentum equation in integral form to a control volume that encloses the airfoil, we obtain an expression for the lift in terms of the fluid velocity and pressure distributions on the control surface.

The lift (per unit span) on the body can also be expressed as:

\[
L' = \int_{\text{surface}} (-p \, \mathbf{n}) \cdot \mathbf{e}_L \, dS,
\]

where \(\mathbf{e}_L\) is the unit vector in the lift direction (normally perpendicular to the freestream velocity direction), and \(\mathbf{n}\) is the outward normal vector on the body surface.

**Step 3: Transformation to a Circulation Integral**  
To link the lift to circulation, we employ several key steps found in potential-flow theory. One common approach uses the complex potential framework and the Blasius integral formula from complex analysis, but here we’ll keep it in a more physical vector form.

- Introduce a contour \(C\) that follows just outside the body, encompassing the airfoil once in the counterclockwise direction.
- Parametrize this contour in the flow field. Since the flow is irrotational, one can define a complex potential \(w(z)=\phi(x,y) + i \psi(x,y)\) in two dimensions (where \(\phi\) is the velocity potential and \(\psi\) is the stream function). In complex analysis treatments, the lift can be directly computed from contour integrals of the complex velocity around the body.
  
A more physical argument without heavy complex analysis tools is as follows:

**Key Idea:** Consider the circulation \(\Gamma = \oint_C \mathbf{u} \cdot d\mathbf{s}\). If you deform the contour \(C\) into a large circle at infinity, the contribution of the body’s presence introduces a nonzero circulation. At infinity, the flow is uniform \(U\hat{i}\) plus a circulation component due to the airfoil.

**Step 4: Using Bernoulli’s Equation and Pressure Differences**  
From Bernoulli’s equation, the pressure difference on the upper and lower surfaces of the airfoil is related to differences in local speed. A circulation around the body modifies these speeds (faster over one surface, slower over the other), resulting in a pressure difference and hence a net lift force.

Now, integrate the pressure distribution around the airfoil. One can show that this net pressure difference, when translated into a lift force, is directly proportional to \(\rho U \Gamma\).

**A More Formal Complex Analysis Derivation (Sketch)**:

1. **Complex Potential and Velocity:** Represent the flow using a complex potential \(w(z)\). For a body with circulation \(\Gamma\), far from the body, the complex velocity \(f(z) = dw/dz\) looks like \(f(z) = U - i\frac{\Gamma}{2\pi (z - z_0)} + \dots\), where the term \(-i\Gamma/(2\pi(z-z_0))\) represents a vortex of circulation \(\Gamma\).

2. **Blasius Formula:** In complex analysis of potential flow, the force on a body can be computed using the Blasius theorem:
   \[
   F_x - iF_y = i\rho \int_C f(z)^2 dz,
   \]
   where \(F_x\) and \(F_y\) are the horizontal and vertical components of the force and the integral is taken around the body contour.

   For large contours and focusing on the leading term in \(f(z)\), the integral reduces nicely, and one finds that the lift (the vertical component, \(F_y\), which corresponds to \(-\text{Im}(F_x - iF_y)\)) is exactly \(\rho U \Gamma\).

3. **Conclusion:** The manipulations show that when you evaluate the contour integral, the only surviving term that contributes to a net vertical force is the one associated with the circulation. This leads to the elegant and simple formula for the lift.

---

**Final Result:**

After going through the steps (either via a control-volume argument or the complex analysis approach), we arrive at the Kutta–Joukowski relation:

\[
L' = \rho U \Gamma.
\]

This is a remarkably simple yet powerful result. It demonstrates that, in an inviscid, irrotational, steady flow, the generation of lift on a body is directly determined by the amount of circulation in the flow around it.