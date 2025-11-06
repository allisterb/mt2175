Solving Systems of Differential Equations with Matrix Diagonalization

Introduction: From Complex Systems to Simple Solutions

Welcome! This guide is designed to demystify the process of solving systems of linear differential equations for the MT2175 Further Linear Algebra exam. Think of this guide as your personal tutorial for this topic, focusing not just on the methods but on the strategies you'll need to succeed on your exam. We'll leverage powerful techniques from linear algebra to turn complex, interconnected problems into simple, solvable ones.

The Core Problem

We often encounter systems of first-order linear differential equations with constant coefficients, which can be written in a compact matrix form:

y′ = Ay

Here, y(t) is a vector of unknown functions (y1(t), y2(t), ..., yn(t))T, and A is a matrix of constant coefficients. The challenge lies in the fact that the rate of change of each function, y′i(t), depends on a combination of the other functions. This "coupling" makes it difficult to solve for any single function directly.

The Core Idea

The central strategy is to simplify the problem by changing our perspective. We will perform a change of variables to transform the complex, coupled system y' = Ay into a new system that is simple and "uncoupled." In this new system, each differential equation can be solved independently. This powerful transformation is achieved through matrix diagonalization.

The key insight is to think of the substitution y = Pz not just as a change of variables, but as a change of basis. The matrix P is a change of basis matrix that transforms the problem from the standard basis (where the components of y are coupled) into a new, more convenient basis composed of eigenvectors. In this special basis, the system's behavior simplifies to simple scaling along the eigenvector directions, which is what the diagonal matrix D represents.

To appreciate why this is our goal, let's first look at the ideal scenario we're trying to create.


--------------------------------------------------------------------------------


1. The Simple Case: Why Diagonal Systems are Easy

Imagine a system y′ = Ay where the matrix A is already a diagonal matrix.

The Diagonal System

If A is diagonal, say A = diag(λ1, λ2, . . . , λn), the system of equations looks like this:

y′1 = λ1y1
y′2 = λ2y2
  ⋮
y′n = λnyn


The Simplicity of Decoupling

Notice that each equation now involves only one unknown function. The rate of change of y1 depends only on y1, the rate of change of y2 depends only on y2, and so on. They are completely independent of each other, or decoupled.

The Solution

Each of these equations is a standard, elementary differential equation. The solution for each is well-known:

yi(t) = yi(0)e^(λit)

This straightforward exponential solution is precisely what we want to achieve. The goal of diagonalization is to transform any suitable system into this simple, solvable form.


--------------------------------------------------------------------------------


2. The Main Technique: Solving Diagonalizable Systems

If a matrix A is diagonalizable, we can systematically transform the system, solve it in the simpler eigenvector basis, and then transform it back.

2.1. The Method: A Step-by-Step Guide

The key is the change of basis y = Pz, where P is an invertible matrix whose columns are the eigenvectors of A. As we saw, this substitution effectively reframes our problem in a basis where the system's structure becomes diagonal.

Starting with our system y' = Ay, we substitute y = Pz:

1. (Pz)' = A(Pz)
2. Pz' = APz (since P is a matrix of constants)
3. z' = (P⁻¹AP)z

Since P is the matrix of eigenvectors, P⁻¹AP is the diagonal matrix D of corresponding eigenvalues. The transformed system is simply:

z' = Dz

This is the easy, decoupled system we examined in the previous section.

The Complete Process

Here is the full workflow for solving a diagonalizable system:

1. Find Eigenvalues and Eigenvectors: For the given matrix A, calculate its eigenvalues (λi) and find a complete set of n linearly independent eigenvectors (vi).
2. Form P and D:
  * Construct the matrix P by placing the eigenvectors vi as its columns.
  * Construct the diagonal matrix D by placing the corresponding eigenvalues λi on the diagonal, in the same order as their eigenvectors in P.
3. Solve the Transformed System: State the simple diagonal system z' = Dz. Its general solution is a vector z(t) where each component is:
  * zi(t) = c_i * e^(λit)
  * The c_i are arbitrary constants.
4. Transform Back: Use the original change of variables, y(t) = Pz(t), to find the general solution for the original system. If initial conditions are provided, use them to find the specific values of the constants c_i.

2.2. Worked Example: General and Particular Solutions

Let's solve the system y' = Ay with the following matrix and initial conditions:

* A = [[6, 13, -8], [2, 5, -2], [7, 17, -9]]
* y(0) = (2, 1, 1)T

Step 1: Diagonalize A

The eigenvalues and corresponding matrices P and P⁻¹ are found to be:

* Eigenvalues: λ1 = -2, λ2 = 1, λ3 = 3
* Eigenvector Matrix (P): P = [[1, -1, 1], [0, 1, 1], [1, 1, 2]]
* Inverse Matrix (P⁻¹): P⁻¹ = [[-1, -3, 2], [-1, -1, 1], [1, 2, -1]]

Step 2: Solve for z(t)

The transformed system is z' = Dz, where D = diag(-2, 1, 3). The general solution for z(t) is:

* z1(t) = αe^(-2t)
* z2(t) = βe^(t)
* z3(t) = γe^(3t) (We use α, β, γ as arbitrary constants for the general solution.)

Step 3: Find the General Solution for y(t)

We transform back using y = Pz:

y(t) = [[1, -1, 1], [0, 1, 1], [1, 1, 2]] * [[αe^(-2t)], [βe^(t)], [γe^(3t)]]

This matrix multiplication gives the general solution:

* y1(t) = αe^(-2t) - βe^(t) + γe^(3t)
* y2(t) = βe^(t) + γe^(3t)
* y3(t) = αe^(-2t) + βe^(t) + 2γe^(3t)

Step 4: Find the Particular Solution

To find the specific constants α, β, γ, we use the initial conditions y(0) = (2, 1, 1)T. The key relationship is z(0) = P⁻¹y(0):

z(0) = [[-1, -3, 2], [-1, -1, 1], [1, 2, -1]] * [[2], [1], [1]] = [[-3], [-2], [3]]

This tells us that z1(0) = α = -3, z2(0) = β = -2, and z3(0) = γ = 3. Substituting these values into our general solution for y(t) gives the final particular solution:

* y1(t) = -3e^(-2t) + 2e^(t) + 3e^(3t)
* y2(t) = -2e^(t) + 3e^(3t)
* y3(t) = -3e^(-2t) - 2e^(t) + 6e^(3t)

This method works beautifully for diagonalizable matrices. But what happens when a matrix cannot be diagonalized?


--------------------------------------------------------------------------------


3. The Complication: Non-Diagonalizable Systems

3.1. Introducing the Jordan Normal Form

The Problem

A matrix is not diagonalizable if it does not have a full set of n linearly independent eigenvectors. This happens when an eigenvalue's geometric multiplicity (the dimension of its eigenspace) is less than its algebraic multiplicity (the number of times it appears as a root of the characteristic polynomial).

The Solution: Jordan Normal Form

When a matrix isn't diagonalizable, the Jordan Normal Form (J) is the next best thing. It's the "simplest" matrix that A can be transformed into. A Jordan matrix is an upper triangular matrix composed of Jordan blocks on its diagonal.

A k x k Jordan block Jk(λ) is a matrix with a single eigenvalue λ on the main diagonal, ones on the superdiagonal (the diagonal directly above the main one), and zeros everywhere else.

* 2x2 Jordan Block: J2(λ) = [[λ, 1], [0, λ]]
* 3x3 Jordan Block: J3(λ) = [[λ, 1, 0], [0, λ, 1], [0, 0, λ]]

A key theorem states that for any square matrix A, there exists an invertible matrix P such that P⁻¹AP = J, where J is a Jordan matrix.

3.2. Solving Systems with Jordan Normal Form

The Transformed System

We use the same change of variables, y = Pz, as before. This transforms the system y' = Ay into z' = Jz. While not as simple as a diagonal system, this is still solvable.

Solving a Jordan Block System

The system z' = Jz is not fully decoupled, but it can be solved from the bottom up. For a single k x k Jordan block, the general solution is known.

For a system w' = Jw, where J is a single k x k Jordan block with eigenvalue λ (and where wj is the j-th function in the transformed system, corresponding to the j-th row of the Jordan block), the general solution is:

wj = c_j*e^(λt) + c_(j+1)*t*e^(λt) + c_(j+2)*(t²/2)*e^(λt) + ··· + c_k*(t^(k-j)/(k-j)!)*e^(λt) for j = 1, ..., k.

Notice the emergence of terms like t*e^(λt) and (t²/2)*e^(λt), which are characteristic of systems with repeated eigenvalues and insufficient eigenvectors.

Worked Example: A Non-Diagonalizable System

Consider the system y' = Ay where A is not diagonalizable:

* A = [[1, 0, 1], [1, 1, -3], [0, 1, 4]]

The Jordan Normal Form J and the transition matrix P are given as:

* J = [[2, 1, 0], [0, 2, 1], [0, 0, 2]]
* P = [[1, 1, 0], [-2, -3, 0], [1, 2, 1]]

Step 1: Solve the Transformed System z' = Jz

Since J is a single 3x3 Jordan block with λ=2, we apply the formula from the theorem for k=3 to find the general solution for z(t):

* z3(t) = c3 * e^(2t)
* z2(t) = c2 * e^(2t) + c3 * t * e^(2t)
* z1(t) = c1 * e^(2t) + c2 * t * e^(2t) + c3 * (t²/2) * e^(2t)

Step 2: Find the General Solution for y(t)

Finally, we transform back using y = Pz. The relationships are y1 = z1 + z2, y2 = -2z1 - 3z2, and y3 = z1 + 2z2 + z3. We substitute the expressions for z(t) and collect terms:

* y1(t) = [c1e^(2t) + c2te^(2t) + c3(t²/2)e^(2t)] + [c2e^(2t) + c3te^(2t)] y1(t) = (c1 + c2)e^(2t) + (c2 + c3)t*e^(2t) + (c3/2)t²*e^(2t)
* y2(t) = -2[c1e^(2t) + c2te^(2t) + c3(t²/2)e^(2t)] - 3[c2e^(2t) + c3te^(2t)] y2(t) = (-2c1 - 3c2)e^(2t) + (-2c2 - 3c3)t*e^(2t) - c3*t²*e^(2t)
* y3(t) = [c1e^(2t) + c2te^(2t) + c3(t²/2)e^(2t)] + 2[c2e^(2t) + c3te^(2t)] + [c3e^(2t)] y3(t) = (c1 + 2c2 + c3)e^(2t) + (c2 + 2c3)t*e^(2t) + (c3/2)t²*e^(2t)

This gives the complete general solution for the original system in terms of the arbitrary constants c1, c2, c3.


--------------------------------------------------------------------------------


4. Summary and Exam Strategy

The method for solving y' = Ay depends entirely on the nature of the matrix A. Here is a direct comparison of the two pathways.

Feature	Diagonalizable Case (A = PDP⁻¹)	Non-Diagonalizable Case (A = PJP⁻¹)
Transformation	y = Pz leads to a decoupled system z' = Dz.	y = Pz leads to a coupled system z' = Jz.
z(t) Solution	Purely exponential solutions: zi = c_i * e^(λit).	Polynomial-exponential solutions involving terms like t*e^(λt) and t²*e^(λt).
Final Solution y(t)	y = Pz, a linear combination of the pure exponential solutions.	y = Pz, a linear combination of the more complex polynomial-exponential solutions.

Key Exam Takeaways

1. Analyze the Matrix A. Your first task is always to find the eigenvalues of A and determine if it is diagonalizable by comparing the algebraic and geometric multiplicities of each eigenvalue. This critical first step dictates your entire solution path.
2. Solve the Transformed System.
  * Diagonalizable: The solution for z' = Dz is zi(t) = c_i * e^(λit).
  * Non-Diagonalizable: Memorize the pattern for z' = Jz based on the size of the Jordan blocks, which introduces terms with t, t²/2!, etc.
3. Transform Back. Always remember the final step, y = Pz, to express the solution in terms of the original functions. Forgetting this is a common mistake.
4. Use Initial Conditions.
  * If initial conditions y(0) are given, you must find the specific constants. The crucial step is z(0) = P⁻¹y(0).
  * If only a general solution is required, leave the constants as arbitrary (α, β, γ or c1, c2, c3). Read the question carefully to know which is required.
  * Final Check: Once you have your particular solution y(t), quickly calculate y(0) by setting t=0. Does it match the given initial conditions? This simple check can catch algebraic errors made during the final substitution.
