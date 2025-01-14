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

## Travelling solution for the BBM

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

where 
- $A > 0$;
- $k = \displaystyle \sqrt{\frac{A}{12+4A}}$;
- $c = 1 + \displaystyle \frac{A}{3}$;

For approximating solutions, we use the [DeepXDE](https://github.com/lululxvi/deepxde) library, which is a kind of interface that links Deep Learning frameworks like TensorFlow and PyTorch to a way of easily modelling PDEs in Python.

## Results

During research, one goal appeared promissing: **finding the best Neural Network optimizer for the BBM equation**.

The DeepXDE library provides multiple options for optimizers for each backend (Tensorflow, PyTorch and others). We chose to stay only with the TensorFlow options: **L-BFGS, SGD, ADAM, NADAM.**

In a fixed setting we manage to obtain various results for each, as listed in the figure below:

![corrida_opt](https://github.com/user-attachments/assets/4d69534a-15e9-46c3-be93-61572027552f)

The main result is that the L-BFGS method is the most suited optimizer for the BBM equation problem proposed.

## References

- Benjamin, T. B., Bona, J. L., & Mahony, J. J. (1972). **Model equations for long waves in nonlinear dispersive systems**. *Philosophical Transactions of the Royal Society of London. Series A, Mathematical and Physical Sciences*, 272(1220), 47–78. The Royal Society London.

- Crighton, D. G. (1995). **Applications of KdV**. In *KdV’95: Proceedings of the International Symposium held in Amsterdam, The Netherlands, April 23–26, 1995, to commemorate the centennial of the publication of the equation by and named after Korteweg and de Vries* (pp. 39–67). Springer.

- Raissi, M., Perdikaris, P., & Karniadakis, G. E. (2017). **Physics informed deep learning (part I): Data-driven solutions of nonlinear partial differential equations**. *arXiv preprint arXiv:1711.10561*.

- Lu, L., Meng, X., Mao, Z., & Karniadakis, G. E. (2021). **DeepXDE: A deep learning library for solving differential equations**. *SIAM Review*, 63(1), 208–228. SIAM.

- Taylor, J., Wang, W., Bala, B., & Bednarz, T. (2022). **Optimizing the optimizer for data-driven deep neural networks and physics-informed neural networks**. *arXiv preprint arXiv:2205.07430*.
