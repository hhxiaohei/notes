...menustart

 - [Elgenvalues and Elgenvectors](#8358d3063f9f8db669067bc62cf5ea5e)
	 - [5.1 INTRODUCTION](#103445c268b50fae9bd814331a04faa4)

...menuend



<h2 id="8358d3063f9f8db669067bc62cf5ea5e"></h2>
# Elgenvalues and Elgenvectors


<h2 id="103445c268b50fae9bd814331a04faa4"></h2>
## 5.1 INTRODUCTION

This chapter begins the "second half" of linear algebra. 

The first half was about Ax = b. The new problem Ax = λx  will still be solved by simplifying a matrix -- making it diagonal if possible. 

*c step is no longer to subtract a multiple of one row from another*. Elimination changes the eigenvalues, which we don't want.

Determinants give a transition from Ax = b to Ax = λx. In both cases the determinant leads to a "formal solution": to Cramer's rule for x = A⁻¹b, and to the polynomial det (A - λI), whose roots will be the eigenvalues. (All matrices are now square; the eigenvalues of a rectangular matrix make no more sense than its determinant.) The determinant can actually be used if n = 2 or 3. For large n, computing λ, is more difficult than solving Ax = b.

The first step is to understand how eigenvalues can be useful. One of their applications is to ordinary differential equations. We shall not assume that the reader is an expert on differential equations ! If you can differentiate xⁿ, sin x, and eˣ, you know enough. As a specific example, consider the coupled pair of equations

```
dv/dt = 4v - 5w,  v = 8 at t=0,
dw/dt = 2v - 3w,  w = 5 at t=0.		(1)
```

This is an ***initial-value problem***. The unknown is specified at time t = 0 by the given initial values 8 and 5. The problem is to find v(t) and w(t) for later times t > 0. 

It is easy to write the system in matrix form. Let the unknown vector be u(t), with initial value u(0). The coefficient matrix is A:

```
Vector unknown :

u(t) = ⎡v(t)⎤, u(0) = ⎡8⎤,  A = ⎡4 -5⎤
	   ⎣w(t)⎦		  ⎣5⎦		⎣2 -3⎦
```

The two coupled equations become the vector equation we want:

```
Matrix form :

du/dt = Au    with u = u(0) at t=0  (2)
```

This is the basic statement of the problem. Note that it is a first-order equation -- no higher derivatives appear -- and it is *linear* in the unknowns. It also has *constant coefficients*; the matrix A is independent of time.

How do we find u(t)? If there were only one unknown instead of two, that question
would be easy to answer. We would have a scalar instead of a vector equation:

```
Single equation :

du/dt = au   with  u = u(0) at t=0	(3)
```

The solution to this equation is the one thing you need to know:

```
Pure exponential 	u(t) = eᵅᵗu(0)	(4)
```

At the initial time t = 0, u equals u(0) because e⁰ = 1. The derivative of eᵅᵗ has the required factor *a*, so that du/dt = au. Thus the initial condition and the equation are both satisfied.

We shall take a direct approach to systems, and look for solutions with the *same exponential dependence* on *t* just found in the scalar case:

 - v(t) = e<sup>λ</sup>ᵗy

 - w(t) = e<sup>λ</sup>ᵗz &nbsp;&nbsp;&nbsp;&nbsp;(5)

or in vector notation:

 - u(t) = e<sup>λ</sup>ᵗx. &nbsp;&nbsp;&nbsp;&nbsp;(6)

This is the whole key to differential equations du/dt = Au:  ***Look for pure exponential solutions***. Substituting v = e<sup>λ</sup>ᵗy and w = e<sup>λ</sup>ᵗz into the equation, we find

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_dif_equation.png)

he factor e<sup>λ</sup>ᵗ is common to every term, and can be removed. This cancellation is the reason for assuming the same exponent λ for both unknowns; it leaves

```
Eigenvalue problem :

4y - 5z = λy
2y - 3z = λz.	  (7)
```

That is the eigenvalue equation. 

In matrix form it is Ax = λx. You can see it again if we use u = e<sup>λ</sup>ᵗx -- a number e<sup>λ</sup>ᵗ that grows or decays times a fixed vector x. ***Substituting into du/dt = Au gives λe<sup>λ</sup>ᵗx = Ae<sup>λ</sup>ᵗx. The cancellation of eat produces***

```
Eigenvalue equation :

Ax = λx.	(8)
```

Now we have the fundamental equation of this chapter. It involves two unknowns λ and x. It is an algebra problem, and differential equations can be forgotten! The number λ (lambda) is an ***eigenvalue*** of the matrix A, and the vector x is the associated ***eigenvector***.
Our goal is to find the eigenvalues and eigenvectors, λ's and x's, and to use them.

---

**The Solutions of Ax = λx**

Notice that Ax = λx is a nonlinear equation; λ multiplies x. If we could discover λ., then the equation for x would be linear. In fact we could write λIx in place of λx, and bring this term over to the left side:

```
(A - λI)x = 0.		(9)
```

The identity matrix keeps matrices and vectors straight; the equation (A - λ)x = 0 is
shorter, but mixed up. This is the key to the problem:

 - ***The vector x is in the nullspace of A - λI***.
 - ***The number λ, is chosen so that A - λI has a nullspace***.

Of course every matrix has a nullspace. We want a *nonzero* eigenvector x.  The goal is to build u(t) out of exponentials e<sup>λ</sup>ᵗx , and *we are interested only in those particular values λ for which there is a nonzero eigenvector x.  To be of any use, the nullspace of A - λI must contain vectors other than zero. In short, A - λI ***must be singular***.

For this, the determinant gives a conclusive test.

**5A**: The number λ is an eigenvalue of A if and only if A - λI is singular:

```
det( A - λI ) = 0.		(10)
```

This is the characteristic equation. Each λ is associated with eigenvectors x:

```
(A - λI)x = 0	or 	 Ax = λx.	(11)
```

In our example, we shift A by λI to make it singular:

```
Subtract λI :

A - λI = ⎡4-λ   -5 ⎤.
		 ⎣ 2   -3-λ⎦
```

Note that λ is subtracted only from the main diagonal (because it multiplies I).


```
Determinant :

|A - λI| = (4 - λ)(-3 - λ) + 10   or   λ² - λ - 2.
```

This is the *characteristic polynomial*. Its roots, where the determinant is zero, are the eigenvalues. They come from the general formula for the roots of a quadratic, or from factoring into λ² - λ - 2 = (λ + 1) (λ - 2).  That is zero if λ = -1 or λ = 2, as the general formula confirms:

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple.png)

**There are two eigenvalues, because a quadratic has two roots.** Every 2 by 2 matrix A - λI has λ² (and no higher power of λ²) in its determinant.

The values λ = -1 and λ = 2 lead to a solution of Ax = λx or (A - λI )x = 0. A matrix with zero determinant is singular, so there must be nonzero vectors x in its nullspace. In fact the nullspace contains a whole line of eigenvectors; it is a subspace!

```
λ₁ = -1: (A - λ₁I)x = ⎡5  -5⎤⎡y⎤ = ⎡0⎤.
					  ⎣2  -2⎦⎣z⎦   ⎣0⎦
```

The solution (the first eigenvector) is any nonzero multiple of x₁:

```
Eigenvector for λ₁ :

x₁ = ⎡1⎤.
	 ⎣1⎦
```

The computation for λ₂ is done separately:

```
λ₂ = 2: (A - λ₂I)x = ⎡2  -5⎤⎡y⎤ = ⎡0⎤.
					 ⎣2  -5⎦⎣z⎦   ⎣0⎦
```

The second eigenvector is any nonzero multiple of x₂:

```
Eigenvector for λ₂ :

x₂ = ⎡5⎤.
	 ⎣2⎦
```

You might notice that the columns of A - λ₁I give x₂, and the columns of A - λ₂I are multiples of x₁. *This is special (and useful) for 2 by 2 matrices*.

In the 3 by 3 case, I often set a component of x equal to 1 and solve (A - λI)x = 0 for the other components(因为满足条件的x很多). Of course if x is an eigenvector then so is 7x and so is -x. All vectors in the nullspace of A - λI (which we call the *eigenspace*) will satisfy Ax = λx. In our example the eigenspaces are the lines through x₁ = (1, 1) and x₂ = (5, 2).

Before going back to the application (the differential equation), we emphasize the steps in solving Ax = λx:

 1. ***Compute the determinant of A - λI***. 
 	- With λ, subtracted along the diagonal, this determinant is a polynomial of degree n. It starts with (-λ)ⁿ.
 2. ***Find the roots of this polynomial***. 
 	- The n roots are the eigenvalues of A.
 3. ***For each eigenvalue solve the equation (A - λI)x = 0***. 
 	- Since the determinant is zero, there are solutions other than x = 0. Those are the eigenvectors.


In the differential equation, this produces the special solutions u = e<sup>λ</sup>ᵗx . They are the *pure exponential solutions* to du/dt = Au. Notice e⁻ᵗ and e²ᵗ:

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple_001.png)

There two special solutions give the complete solution. They can be multiplied by any numbers c₁ and c₂, and they can be added together. When u₁ and u₂ satisfy the linear equation du/dt = Au, so does their sum u₁ + u₂.

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple_012.png)

This is ***superposition***, and it applies to differential equations (homogeneous and linear) just as it applied to matrix equations Ax = 0. The nullspace is always a subspace, and combinations of solutions are still solutions.

Now we have two free parameters c₁ and c₂, and it is reasonable to hope that they can be chosen to satisfy the initial condition u = u(0) at t = 0:

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple_013.png)

The constants are c₁ = 3 and c₂ = 1, and the solution to the original equation is

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple_014.png)

Writing the two components separately, we have v (0) = 8 and w (0) = 5:

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/LA_eigen_eigenvalues_4_exmaple_014.1.png)

The key was in the eigenvalues λ and eigenvectors x. Eigenvalues are important in themselves, and not just part of a trick for finding *u*. 

Probably the homeliest example is that of soldiers going over a bridge.  Traditionally, they stop marching and just walk across. If they happen to march at a frequency equal to one of the eigenvalues of the bridge, it would begin to oscillate. (Just as a child's swing does; you soon notice the natural frequency of a swing, and by matching it you make the swing go higher.) An engineer tries to keep the natural frequencies of his bridge or rocket away from those of the wind or the sloshing of fuel. And at the other extreme, a stockbroker spends his life trying to get in line with the natural frequencies of the market. The eigenvalues are the most important feature of practically any dynamical system.


**Summary and Examples**

To summarize, this introduction has shown how λ and x appear naturally and automatically when solving du/dt = Au. Such an equation has pure exponential solutions u = e<sup>λ</sup>ᵗx ; the eigenvalue gives the rate of growth or decay, and the eigenvector x develops at this rate. The other solutions will be mixtures of these pure solutions, and the mixture is adjusted to fit the initial conditions.

The key equation was Ax = λx. Most vectors x will not satisfy such an equation. They change direction when multiplied by A, so that Ax is not a multiple of x. This means that ***only certain special numbers λ are eigenvalues, and only certain special vectors x are eigenvectors***. We can watch the behavior of each eigenvector, and then combine these "normal modes" to find the solution. To say the same thing in another way, the underlying matrix can be diagonalized.

The diagonalization in Section 5.2 will be applied to difference equations, Fibonacci numbers, and Markov processes, and also to differential equations. In every example, we start by computing the eigenvalues and eigenvectors; there is no shortcut to avoid that. Symmetric matrices are especially easy. "Defective matrices" lack a full set of eigenvectors, so they are not diagonalizable. Certainly they have to be discussed, but we will not allow them to take over the book. We start with examples of particularly good matrices.

Example 1: Everything is clear when A is a ***diagonal matrix***:

```
A = ⎡3 0⎤ has λ₁ = 3 with x₁ = ⎡1⎤,  λ₂ = 2 with x₂ = ⎡0⎤.
	⎣0 2⎦  					   ⎣0⎦					  ⎣1⎦
```

On each eigenvector A acts like a multiple of the identity: Ax₁ = 3x₁ and Ax₂ = 2x₂. Other vectors like x = (1, 5) are mixtures x₁ + 5x₂ of the two eigenvectors, and when A multiplies x₁ and x₂ it produces the eigenvalues  λ₁ = 3 and x₂ = 2:

```
A  times  x₁+5x₂  is 3x₁+10x₂ = ⎡ 3⎤.  
								⎣10⎦
```

This is Ax for a typical vector x -- not an eigenvector. But the action of A is determined by its eigenvectors and eigenvalues.



Example 2: The eigenvalues of a ***projection matrix*** are 1 or 0!

```
P = ⎡1/2 1/2⎤ has λ₁ = 1 with x₁ = ⎡1⎤,  λ₂ = 0 with x₂ = ⎡ 1⎤.
	⎣1/2 1/2⎦  					   ⎣1⎦					  ⎣-1⎦
```

We have λ = 1 when x projects to itself, and λ = 0 when x projects to the zero vector. The column space of P is filled with eigenvectors, and so is the nullspace. If those spaces have dimension r and n - r, then k = 1 is repeated r times and A = 0 is repeated n - r times (always n λ's):

```
Four eigenvalues allowing repeats:

	⎡1 0 0 0⎤
P = ⎢0 0 0 0⎥ 	has λ = 1,1,0,0
 	⎢0 0 0 0⎥   
	⎣0 0 0 1⎦ 
```

***There is nothing exceptional about λ = 0***. Like every other number, zero might be an eigenvalue and it might not. If it is, then its eigenvectors satisfy Ax = Ox. Thus x is in the nullspace of A. A zero eigenvalue signals that A is singular (not invertible); its determinant is zero. Invertible matrices have all λ ≠ 0.

Example 3: The eigenvalues are on the main diagonal when A is ***triangular***:






