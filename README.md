# Physics-Informed Neural Networks (PINNs) for approximating solutions of the Benjamin-Bona-Mahony (BBM) equation

In this repo, I archive all my work on the project, from my initial Python notebooks to all my PDF slides that were used (in Portuguese).

We aim to approximate solutions of the following problem: 

$$
\begin{aligned}
    u_t + u_x + u \, u_x - \, u_{xxt} &= 0, \quad &&\quad (x,t) \in  (-10, 20) \times (0,4) \\
   u(x,0) &= u_0(x),                 \quad &&\quad x \in (-10, 20),\\
   u(-10,t) &= g_1(t) \\
   u(20,t) &= g_2(t)                      \quad &&\quad t \in (0,4),
\end{aligned}
$$

where 
- $u_0$ is the **initial condition** at $t = 0$;
- $g_1, g_2$ are **boundary conditions** for the problem.

### Travelling solution for the BBM

The BMM is a _nonlinear partial differential equation_ and has a travelling wave solution of the form

$$
\begin{alignat*}{2}
    u(x,t) = Asech^2(k(x - ct)),
\end{alignat*}
$$

where 
- $A > 0$ is given and called the **amplitude**;
- $k = \displaystyle \sqrt{\frac{A}{12+4A}}$, called the **frequency**;
- $c = 1 + \displaystyle \frac{A}{3}$, called the **velocity**.

With the goal of providing the best scenario for the PINNs, we use this solution evaluated at initial time and boundary. 

The problem is then written as:

$$
    \begin{alignat*}{2}
        u_t + u_x + u u_x - u_{xxt} &= 0, &\qquad& (x,t) \in  (-10, 20) \times (0,4),\\
        u(x,0) &= Asech^2(kx), &\qquad& x \in (-10, 20),\\
        u(-10,t) &= Asech^2(k(-10 - ct)), \\
        u(20,t) &= Asech^2(k(20 - ct)), &\qquad& t \in (0,4),
    \end{alignat*}
$$

where $A > 0$, $k = \sqrt{\frac{A}{12+4A}}$ e $c = 1 + \frac{A}{3}$.
