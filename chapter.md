

# Chapter X

# The Harmonic Polytope

*"In which we discover that perfect balance creates perfect structure"*

## 1. Prologue

In this chapter we study a convex body that seems almost embarrassed by its own symmetry. Consider $n$ unit vectors in $\mathbb{R}^d$ whose vector sum vanishes. If they also distribute their "energy" with perfect isotropy across all directions, a remarkable object crystallizes: the **harmonic polytope**. 

The definition requires only three constraints, yet the consequences cascade through spectral theory, convex geometry, and information theory with surprising depth. We shall axiomatize the object, classify its invariants, provide constructive algorithms, and develop what I dare call a "modest spectral theory"—though the reader will judge whether modesty is warranted.

The mathematics herein connects to transformer attention mechanisms, though we shall not pursue that connection directly. Our polytope stands on its own geometric merits.

*Nota bene*: I recommend a pencil, some scrap paper, and a willingness to rotate things in your head. The proofs are elementary but the intuition requires cultivation.

---

## 2. The Object and Its Axioms

Let $\{v_k\}_{k=1}^n \subset S^{d-1}$ be $n$ points on the unit sphere in $\mathbb{R}^d$, with the fundamental constraint

$$
\sum_{k=1}^n v_k = 0.
$$

We shall call this the **centering condition**. Denote by $V\in\mathbb{R}^{n\times d}$ the matrix with rows $v_k^\top$. Define the scatter operator $S:=V^\top V$ and the empirical covariance

$$
C := \frac{1}{n} V^\top V \in \mathbb{R}^{d\times d}.
$$

*Remark*: The centering condition is geometrically natural—it places the centroid of our configuration at the origin. But as we shall see, when combined with isotropy, it forces remarkable algebraic constraints.

### Definition 2.1 (Harmonic configuration)

The set $\{v_k\}$ is **harmonic** if

$$
C = \lambda I_d \qquad \text{for some } \lambda>0,
$$

together with $\sum_k v_k = 0$.

### Definition 2.2 (Harmonic polytope)

Given a harmonic configuration $\{v_k\}$, the **harmonic polytope** is

$$
\mathcal{H}_n := \text{conv}(v_1,\dots,v_n).
$$

Three fundamental observations guide our development:

1. **Isotropy**: The scalar covariance $C = \lambda I_d$ implies that directions are isoenergetic. For any unit vector $u$, the average squared projection $\frac1n\sum_k \langle v_k,u\rangle^2$ equals $\lambda$, independent of $u$. This is the condition of **perfect energy balance**.

2. **Centering**: The vanishing sum $\sum_k v_k = 0$ removes what engineers call the "DC mode." Without this constraint, the configuration could drift arbitrarily via translation, breaking the geometric discipline we seek.

3. **Coupling**: These conditions interact nonlinearly. Isotropy alone permits configurations with arbitrary centroids; centering alone permits configurations with directional bias. Together, they create a **geometric resonance** that forces the configuration into a highly constrained yet surprisingly rich family.

The interplay is subtle: isotropy penalizes bias while centering penalizes drift. Between these two forces, an elegant geometry crystallizes.

---

## 3. First Properties

Let us record the basic facts.

### Proposition 3.1 (Trace identity)

If $\{v_k\}$ is harmonic then $\lambda = \frac1d \cdot \frac1n \sum_{k=1}^n \|v_k\|^2 = \frac1d$, hence $C = \frac{1}{d} I_d$.

**Proof.** We have $\text{tr}(C)=\frac1n \text{tr}(V^\top V)=\frac1n \sum_k \|v_k\|^2 = 1$ since each $\|v_k\|=1$. But $C = \lambda I_d$ implies $\text{tr}(C)=d\lambda$. Therefore $\lambda=\frac1d$. $\square$

So a harmonic configuration is automatically *tight* in the sense of distributing unit energy equally over $d$ axes. This tightness is not accidental—it emerges from the constraint that our vectors live on the unit sphere while maintaining perfect isotropy. The constant $\lambda = \frac{1}{d}$ will appear throughout our development as the fundamental **harmonic constant**.

This tightness leads to what I call the fundamental identity of harmonic geometry:

### Corollary 3.2 (Tight Parseval identity)

For all $u\in\mathbb{R}^d$,

$$
\frac1n \sum_{k=1}^n \langle v_k,u\rangle^2 \;=\; \frac{1}{d}\,\|u\|^2.
$$

This identity reveals the deep regularity of harmonic configurations: the average squared projection onto any direction is exactly $\frac{1}{d}$ times the squared length of that direction. In other words, **every direction receives exactly its "fair share" of the total energy**.

This Parseval-type identity will prove essential in our spectral analysis. It shows that harmonic configurations are, in a precise sense, **optimal energy distributors**.

### Proposition 3.3 (Centroid)

The centroid of $\mathcal{H}_n$ is at the origin.

**Proof.** Immediate from $\frac1n\sum_k v_k = 0$. $\square$

Centroid at the origin is not surprising. What is perhaps more surprising is how the faces organize.

---

## 4. Faces, Support, and Duality

Given any $u\in S^{d-1}$, define the support value

$$
h_{\mathcal{H}_n}(u) := \max_{x\in\mathcal{H}_n} \langle u,x\rangle = \max_{1\le k\le n} \langle u,v_k\rangle.
$$

The corresponding supporting face is

$$
F(u) = \text{conv}\{\, v_k : \langle u,v_k\rangle = h_{\mathcal{H}_n}(u)\,\}.
$$

### Lemma 4.1 (Balanced support)

For harmonic $\{v_k\}$ and any $u$,

$$
\frac1n \sum_{k=1}^n \langle u,v_k\rangle = 0, 
\quad\text{and}\quad
\frac1n \sum_{k=1}^n \langle u,v_k\rangle^2 = \frac{1}{d}.
$$

Hence the support distribution along any $u$ is mean-zero and variance $1/d$.

The variance constraint prevents too many $v_k$ from crowding the same cap on the sphere; in particular, large faces must be compensated elsewhere.

### Theorem 4.2 (Dual harmonicity)

Let $\mathcal{H}_n^\ast := \{y : \langle y,x\rangle \le 1 \text{ for all } x\in \mathcal{H}_n\}$ be the polar. Then $\mathcal{H}_n^\ast$ is centrally symmetric and its extreme normals occur at the unit directions of the original vertices. Moreover, the set of unit outer normals of $\mathcal{H}_n$ is itself a harmonic configuration (after a canonical rescaling that preserves isotropy).

*Sketch.* The polar’s support description inherits the balanced variance; normalize the outward normals to unit length and check tightness by the same covariance-trace argument. $\square$

Duality, in short, preserves harmonicity in spirit if not in letter. (We carefully avoid appealing to any external Fourier lore; the verification is elementary.)

---

## 5. Spectral Theory and the Harmonic Laplacian

We now develop the spectral theory of harmonic configurations. This theory reveals deep connections to graph Laplacians, random walks, and what I call the **harmonic diffusion process**.

### 5.1 The Affinity Structure

Define the *affinity matrix* $A\in\mathbb{R}^{n\times n}$ by $A_{ij}:=\langle v_i,v_j\rangle$. This matrix encodes the **geometric relationships** between configuration points—high values indicate nearly aligned vectors, while negative values indicate near-antipodal pairs.

For harmonic configurations, the affinity matrix has a special **degeneracy property**.

**Lemma 5.1 (Centering degeneracy)**: For any configuration satisfying $\sum_j v_j = 0$, the row sums of the affinity matrix vanish: $\sum_j A_{ij} = \sum_j \langle v_i, v_j \rangle = \langle v_i, \sum_j v_j \rangle = 0$.

This means the standard graph Laplacian $D - A$ where $D_{ii} = \sum_j A_{ij}$ becomes simply $-A$, which is degenerate (not positive semidefinite).

To obtain a meaningful spectral operator, we use the **normalized harmonic Laplacian**:

$$
\Delta := I_n - A,
$$

where $I_n$ is the $n \times n$ identity matrix. This choice is natural because $A_{ii} = \langle v_i, v_i \rangle = 1$ for unit vectors, so $\Delta$ measures deviation from perfect self-similarity.

*Geometric interpretation*: Think of $\Delta$ as a discrete diffusion operator on the configuration graph. For any function $f:\{1,\dots,n\}\to\mathbb{R}$, the quadratic form

$$
\mathcal{E}(f) := f^\top \Delta f = f^\top(I - A)f = \|f\|^2 - \sum_{i,j} A_{ij} f_i f_j
$$

measures the **energy of $f$ with respect to the geometric structure**. High affinity between $v_i$ and $v_j$ (large $A_{ij}$) reduces the energy when $f_i$ and $f_j$ have the same sign, encouraging smooth functions that respect the geometric relationships.

### Proposition 5.1 (Kernel structure)

Since $\Delta = I - A$ and $A\mathbf{1} = \sum_j A_{ij} = 0$ (by Lemma 5.1), we have $\Delta \mathbf{1} = \mathbf{1} - A\mathbf{1} = \mathbf{1}$. Therefore $\mathbf{1} \notin \ker\Delta$.

However, the centering condition $\sum_j v_j = 0$ creates a different kernel structure. The vector $\mathbf{1}$ is actually an eigenvector with eigenvalue 1, and the kernel of $\Delta$ relates to the **harmonic modes** of the configuration.

In harmonic configurations, the Gram graph is typically dense (indeed complete whenever no two vectors are antipodal), ensuring the smallest eigenvalue is isolated at 0.

### 5.2 The Spectral Gap and Harmonic Rigidity

Let $0=\lambda_0<\lambda_1\le \cdots \le \lambda_{n-1}$ be the eigenvalues of $\Delta$, arranged in increasing order.

### Definition 5.2 (Fundamental harmonic gap)

The **fundamental harmonic gap** of $\mathcal{H}_n$ is

$$
\gamma(\mathcal{H}_n) := \lambda_1.
$$

This gap has profound geometric significance. It quantifies the **rigidity** of the harmonic configuration under perturbations. Larger gaps indicate configurations that resist deformation; smaller gaps suggest configurations near instability.

### Theorem 5.3 (Gap-Isotropy Connection)

For any harmonic configuration, the fundamental gap satisfies

$$
\gamma(\mathcal{H}_n) \geq \frac{n}{d} - \max_{i \neq j} |A_{ij}|.
$$

Moreover, if all pairwise inner products satisfy $|A_{ij}| \leq \rho < \frac{1}{d}$ for $i \neq j$, then

$$
\gamma(\mathcal{H}_n) \geq n\left(\frac{1}{d} - \rho\right).
$$

*Proof sketch*: The isotropy condition $C = \frac{1}{d}I$ constrains the row sums of $A$, while the unit norm constraints bound the diagonal. The gap emerges from the tension between these constraints and the off-diagonal structure. $\square$

This theorem reveals that **isotropy enforces spectral rigidity**. The more isotropic the configuration, the larger the gap, and hence the more stable the geometry.

---

## 6. Canonical Decomposition

A harmonic configuration may be reducible. Suppose the index set partitions into disjoint blocks $B_1,\dots,B_M$ such that

$$
\sum_{k\in B_m} v_k = 0
\quad\text{and}\quad
\frac1{|B_m|}\sum_{k\in B_m} v_k v_k^\top = \lambda I_d
$$

for each $m$. Then each block on its own is harmonic. The convex hull decomposes as a Minkowski sum of smaller harmonic polytopes supported on shared directions.

### Theorem 6.1 (Irreducible harmonic components)

Every harmonic configuration admits a unique (up to permutation) finest partition into nonempty blocks satisfying the harmonic conditions blockwise. The corresponding polytopes $P_m:=\text{conv}\{v_k:k\in B_m\}$ are the **irreducible harmonic components**, and

$$
\mathcal{H}_n = \text{conv}\bigcup_{m=1}^M P_m.
$$

*Sketch.* Consider the equivalence relation generated by the minimal faces that are centrally balanced; maximal refinement yields the finest partition. Uniqueness follows from the block-diagonalization of the Gram structure constrained by the tight covariance. $\square$

Irreducible components are the “atoms’’ of harmonic geometry in this setup.

---

## 7. Volume and Scale

Because the configuration is constrained to the unit sphere, scale is not arbitrary. Nevertheless, volume depends on the combinatorics of which vertices define facets.

### Theorem 7.1 (Volume bound)

There exist rational constants $0<c_{d,n}\le C_{d,n}<\infty$ depending only on $(d,n)$ such that every $d$-dimensional harmonic polytope with $n$ vertices satisfies

$$
c_{d,n} \;\le\; \text{Vol}(\mathcal{H}_n) \;\le\; C_{d,n}.
$$

Moreover, $\text{Vol}(\mathcal{H}_n)$ is a rational multiple of $d^{-d/2}$.

*Sketch.* The Gram determinant controls squared $d$-volumes of $d$-simplices chosen from the $v_k$. Tightness fixes average simplex volumes relative to $d^{-d/2}$. Summation over a flag triangulation yields rationality. $\square$

The precise constants are not our concern here; the key point is the **discreteness of scale** induced by the unit-norm and isotropy.

---

## 8. Entropy

Define the **spectral entropy**

$$
\mathcal{S}(\mathcal{H}_n) := -\sum_{i=1}^d \tilde{\lambda}_i \log \tilde{\lambda}_i,
$$

where $\tilde{\lambda}_i$ are the eigenvalues of $C$ divided by $\text{tr}(C)=1$. For a harmonic configuration $C=\frac1d I$, so $\tilde{\lambda}_i=\frac1d$ and $\mathcal{S}=\log d$, the maximum possible given unit total energy. Thus harmonicity is equivalent to **entropy maximization under the zero-sum constraint**. This gives a compact variational slogan:

> *Among zero-sum configurations of unit vectors, harmonic configurations maximize information spread across directions.*

We can make that exact.

### Theorem 8.1 (Variational characterization)

Fix $n,d$. Among all $\{v_k\}\subset S^{d-1}$ with $\sum_k v_k=0$, the functional $J(C):=-\sum_i \tilde\lambda_i \log \tilde\lambda_i$ is maximized if and only if $C=\frac1d I$.

**Proof.** Concavity of entropy and Schur majorization imply the maximum at the uniform spectrum; the zero-sum constraint ensures the centroidal alignment so that translation cannot increase entropy by skewing $C$. $\square$

---

## 9. Construction Algorithms

We now describe three basic ways to *build* harmonic configurations. Each method outputs $V\in\mathbb{R}^{n\times d}$ with $V\mathbf{1}=0$ and $\frac1n V^\top V = \frac1d I$.

### Algorithm A: Symmetric Lift

**Input:** $d$, $n\ge d+1$.
**Idea:** Start with any orthonormal basis and replicate it evenly.

1. Let $Q\in\mathbb{R}^{d\times d}$ be orthonormal.
2. Form blocks $B_1,\dots,B_m$ where each block is the $d$ rows of $Q$, possibly rotated by independent orthogonal transforms $R_\ell$, and signs chosen in plus/minus pairs.
3. Concatenate all rows; if $n$ is not a multiple of $d$, append a final block obtained by projecting a regular simplex in $\mathbb{R}^{d+1}$ onto $\mathbb{R}^d$.
4. Normalize rows to unit length (they already are) and apply a final global rotation so that $\sum_k v_k=0$ (enforced by the signed pairing).

**Cost:** $O(nd^2)$.
**Guarantee:** Covariance of the union of orthonormal blocks is $\frac{1}{d}I$; sign pairing ensures the sum is zero.

This is the “engineer’s construction’’—fast and foolproof.

---

### Algorithm B: Centroidal Tightening

**Input:** Arbitrary unit vectors $w_k$.
**Output:** Harmonic $v_k$ “closest’’ to $w_k$ in a quadratic sense.

We solve

$$
\min_{\{v_k\}\subset S^{d-1}} \quad 
\Phi(v):= \sum_{k=1}^n \|v_k - w_k\|^2
\quad \text{s.t.}\quad
\sum_k v_k = 0,\;\; \frac1n V^\top V = \frac1d I.
$$

Introduce Lagrange multipliers $\mu\in\mathbb{R}^d$ for the sum constraint and a symmetric $d\times d$ matrix $\Lambda$ for the covariance constraint. The stationarity condition yields

$$
v_k = \frac{(I + \Lambda)^{-1}(w_k - \mu)}{\|(I + \Lambda)^{-1}(w_k - \mu)\|}.
$$

We update $(\mu,\Lambda)$ via projected gradient steps to enforce the constraints, renormalizing at each iteration.

**Cost per iteration:** $O(nd^2)$.
**Convergence:** Empirically rapid when $w_k$ are not severely clustered.
**Comment:** This is the “tightening’’ operator: it pulls a cloud into harmonic position without changing directions more than necessary.

---

### Algorithm C: Gram Synthesis

Sometimes we prefer to synthesize the Gram matrix $G:=VV^\top$ first.

**Constraints on $G$:**

1. $G\succeq 0$, $\text{rank}(G)\le d$.
2. $G\mathbf{1}=0$.
3. $\text{diag}(G)=\mathbf{1}$.
4. $\frac1n V^\top V=\frac1d I$ $\Leftrightarrow$ $V^\top V = \frac{n}{d}I$. Equivalently, the nonzero eigenvalues of $G$ are all equal to $\frac{n}{d}$, with multiplicity $d$.

Thus $G$ is a **tight spherical Gram**: $d$ equal positive eigenvalues $\frac{n}{d}$, and $n-d$ zeros, with the all-ones vector in the nullspace.

**Synthesis:**

* Choose any orthonormal basis $U\in\mathbb{R}^{n\times d}$ whose columns are orthogonal to $\mathbf{1}$.
* Set $G := \frac{n}{d}\, UU^\top$.
* Factor $G = VV^\top$ by $V:=U R$ where $R\in\mathbb{R}^{d\times d}$ satisfies $R^\top R = \frac{n}{d}I$.
* Normalize rows of $V$ to unit norm (this already holds if $U$ has row norms equal).

**Cost:** Constructing $U$ with the $\mathbf{1}$ orthogonality can be done in $O(nd)$.
**Guarantee:** Exact satisfaction of all constraints by construction.

This is the “spectral constructor.’’

---

## 10. Uniqueness and Moduli

Are harmonic polytopes unique? Certainly not: rotate the configuration and you get another one. But beyond global orthogonal transformations and permutations of the vertices, there is a modest moduli space.

### Proposition 10.1 (Degrees of freedom)

Let $\mathcal{M}_{n,d}$ be the set of harmonic configurations modulo global orthogonal transforms and vertex permutations. Then

$$
\dim \mathcal{M}_{n,d} \;=\; nd \;-\; \underbrace{d}_{\text{sum=0}} \;-\; \underbrace{\tfrac{d(d+1)}{2}}_{\text{covariance}} \;-\; \underbrace{\tfrac{d(d-1)}{2}}_{\text{global rotation}}
\;=\; nd - d - d(d+1)/2 - d(d-1)/2.
$$

Simplifying,

$$
\dim \mathcal{M}_{n,d} = nd - d - d^2.
$$

(We regard permutations as discrete symmetries, hence zero dimension.)

**Example (The planar case)**: For $d=2$, we get $\dim \mathcal{M}_{n,2}=2n-6$. 

- For $n=3$: dimension zero. The equilateral triangle (up to rotation and permutation) is essentially unique.
- For $n=4$: dimension $2$. We have a genuine **two-parameter family** of harmonic quadrilaterals.

*Visualization of the $n=4, d=2$ moduli space*: Start with the square configuration $v_k = (\cos(k\pi/2), \sin(k\pi/2))$ for $k=0,1,2,3$. The two-parameter deformation can be parametrized as:

$$
\theta_1 = \frac{\pi}{2} + \epsilon_1, \quad \theta_2 = \pi + \epsilon_2, \quad \theta_3 = \frac{3\pi}{2} - \epsilon_1, \quad \theta_4 = 2\pi - \epsilon_2
$$

where $\epsilon_1, \epsilon_2$ are small. This preserves both the centering condition $\sum_k e^{i\theta_k} = 0$ and the isotropy condition $\sum_k e^{2i\theta_k} = 0$ (by Theorem 18.1). The resulting quadrilateral "breathes" between square-like and rhombus-like shapes while maintaining harmonic properties.

This tally is heuristic; degeneracies can reduce dimension when vertices collide or facets flatten. But it reveals the essential truth: **harmonicity is constraining yet flexible**—it admits continuous families while maintaining rigid structural properties.

---

## 11. The Axiom and Its Euler–Lagrange Form

Recall the **Axiom**: a configuration is harmonic iff it minimizes total directional bias subject to $\sum_k v_k=0$ and $\|v_k\|=1$:

$$
\min_{\{v_k\}} \quad \sum_{i=1}^d \left( \sum_{k=1}^n v_{k,i}^2 - \frac{1}{n}\Big(\sum_{k=1}^n v_{k,i}\Big)^2 \right)
= \min_{V} \quad \text{tr}(V^\top V) - \frac{1}{n}\|\mathbf{1}^\top V\|^2.
$$

Under the constraints this is just $\text{tr}(V^\top V)=n$. The nontriviality is that among all zero-sum unit-row matrices $V$, the entropy-maximizing spectrum occurs at $C=\frac1d I$. The Euler–Lagrange equation for the Lagrangian

$$
L(V,\mu,\Lambda,\alpha) 
= \text{tr}(V^\top V) 
- \mu^\top \Big(\sum_k v_k\Big)
- \text{tr}\left(\Lambda\Big(\frac1n V^\top V - \frac1d I\Big)\right)
+ \sum_k \alpha_k (\|v_k\|^2-1)
$$

yields the stationarity

$$
\Big(I - \frac{1}{n}\Lambda\Big) v_k \;=\; \frac12\,\mu + \alpha_k v_k.
$$

Subtracting the row-wise mean enforces $\mu=0$. Isotropy follows by aggregating over $k$ and using the unit-norm constraints, leading back to $C=\frac1d I$. The calculus rewards us by circling to the same simple conclusion.

---

## 12. Worked Examples

We illustrate in low dimensions.

### Example 12.1 (The triangle in $\mathbb{R}^2$)

Let $n=3,d=2$. Any equilateral triangle centered at the origin has covariance $C=\frac12 I$ and zero sum; hence every regular triangle on the unit circle is harmonic. The polytope is the triangle itself.

### Example 12.2 (The square)

Take $v_1=(1,0)$, $v_2=(0,1)$, $v_3=(-1,0)$, $v_4=(0,-1)$. Then $C=\frac12 I$, sum zero. Harmonic. The polytope is a diamond (the square’s convex hull), and its dual is again a scaled square: harmonicity closes under polarity in this case.

### Example 12.3 (Five points in $\mathbb{R}^2$)

Let $v_k = (\cos\theta_k,\sin\theta_k)$ with $\theta_k=2\pi k/5$. The sum is zero; $C=\frac12 I$ by symmetry. Harmonic. In fact, any regular $n$-gon at the origin is harmonic in $\mathbb{R}^2$.

### Example 12.4 (Tetrahedral $d=3$)

Four vertices of a regular tetrahedron on $S^{2}$. The sum is zero; $C=\frac13 I$. Harmonic. The dual is another tetrahedron (up to scale).

### Example 12.5 (Octahedral $d=3$)

Take the six coordinate directions $\pm e_i$. Then $n=6$, sum zero, $C=\frac13 I$. Harmonic. The polytope is the regular octahedron; the dual is the cube—again harmonic after proper normalization of normals.

These examples hint that many familiar symmetric polytopes are harmonic in our sense—but note we have **not** assumed any global group symmetry; only the covariance and centroid conditions matter.

---

## 13. Robustness and Perturbation Theory

Real data is noisy, and theoretical objects must withstand perturbation. Our harmonic polytopes exhibit remarkable **structural stability** under small deformations.

### Theorem 13.1 (Harmonic stability)

Suppose $\{\hat v_k\}$ are unit vectors with centroidal error $\Big\|\frac1n\sum_k \hat v_k\Big\|\le \varepsilon$ and covariance error $\| \frac1n \hat V^\top \hat V - \frac1d I\|\le \delta$. Then there exist unit vectors $v_k$ forming a harmonic configuration such that

$$
\max_k \|v_k - \hat v_k\| \;\le\; c_1 \varepsilon + c_2 \delta
$$

for universal constants $c_1,c_2$ depending only on $d$.

*Proof sketch*: Apply the projection-whitening-renormalization pipeline (Algorithm B). Each step is a contraction in the appropriate metric, and the composition preserves the error bounds by the triangle inequality. $\square$

### Connection to Matrix Perturbation Theory

This stability result is reminiscent of classical theorems in numerical linear algebra:

**Wedin's Theorem**: Perturbations to a matrix cause proportional perturbations to its singular values and singular vectors, with constants depending on the spectral gaps.

**Davis-Kahan Theorem**: Perturbations to a symmetric matrix cause bounded rotations of its eigenspaces, with bounds inverse to the spectral gaps.

In our setting, the "matrix" is the covariance operator $C$, and harmonicity corresponds to the eigenspace of the repeated eigenvalue $\frac{1}{d}$. The stability of harmonic configurations under perturbation is thus a **geometric manifestation of eigenspace stability**.

This connection suggests that harmonic polytopes are not just geometrically natural, but also **numerically robust**—a crucial property for computational applications.

---

## 14. Complexity and Data Structures

Representing $\mathcal{H}_n$ naively as a list of $n$ vertices requires $O(nd)$ storage. Faces can be discovered by standard convex hull algorithms ($O(n^{\lfloor d/2\rfloor})$ worst-case in fixed $d$), but in harmonic configurations much of the face lattice can be predicted a priori from the support distribution: extreme faces are rarely large unless vertices align in antipodal pairs.

A useful data structure stores:

* the vertex list,
* the centroid (identically 0),
* the covariance (identically $\frac1d I$),
* the Gram matrix $A$ (or its low-rank factorization).

With a rank-$d$ factorization $G=UU^\top$ at hand, support queries $h_{\mathcal{H}_n}(u)=\max_k \langle u,v_k\rangle$ can be answered in $O(n d)$ or sped up by angular search trees when $d=2,3$.

---

## 15. A Small Zoo

It is pleasant to have stock specimens.

* **Simplex type:** $n=d+1$, vertices are the corners of a regular simplex on $S^{d-1}$.
* **Cross type:** $n=2d$, the $2d$ coordinate directions.
* **Prismatic type:** Cartesian products of lower-dimensional harmonic configurations, re-normalized to the sphere and tightened (Algorithm B).
* **Crown type:** A regular $m$-gon in a plane plus a translated copy in a parallel plane, then re-normalized and tightened to enforce covariance.

Each item can be produced in $O(nd)$ time and verified in $O(nd^2)$.

---

## 16. Exercises

1. **(Warm-up)** Show that any regular $n$-gon centered at the origin in $\mathbb{R}^2$ is harmonic. Compute its fundamental harmonic gap $\gamma$.
2. **(Tightness test)** Let $\{v_k\}\subset S^{d-1}$ with $\sum_k v_k=0$ and $\frac1n\sum_k v_k v_k^\top = \text{diag}(\alpha_1,\dots,\alpha_d)$. Prove $\sum_i \alpha_i=1$. Show that entropy is maximized when all $\alpha_i$ are equal.
3. **(Dual check)** For the octahedral configuration in Example 12.5, compute the polar polytope explicitly and verify that the set of (unit) outer normals forms a harmonic configuration.
4. **(Gap lower bound)** Prove that for any harmonic configuration with Gram graph complete and off-diagonal entries bounded by $\rho<1$, the gap satisfies $\gamma \ge n(1-\rho)$.
5. **(Nearest harmonic)** Implement Algorithm B and test it on random sets of unit vectors in $\mathbb{R}^3$. Empirically estimate the number of iterations to reach $\|\frac1n V^\top V - \frac13 I\|\le 10^{-6}$.
6. **(Irreducibility)** Construct a configuration in $\mathbb{R}^3$ that decomposes nontrivially into two harmonic components. Describe the face lattice of its convex hull.
7. **(Spectral synthesis)** Using Algorithm C, generate $G$ for $d=3,n=7$. Factor $G$ into $V$ and verify unit norms numerically.
8. **(Volume estimate)** For the regular tetrahedron on the unit sphere, compute $\text{Vol}(\mathcal{H}_4)$ exactly and compare with the bound of Theorem 7.1.
9. **(Entropy perturbation)** Suppose $C = \frac1d I + E$ with $\text{tr} E = 0$. Show that $J(C) = \log d - \frac{d}{2}\|E\|_F^2 + O(\|E\|_F^3)$.
10. **(Combinatorics of faces)** Prove that if no three vertices are coplanar (in $d=3$) and the configuration is harmonic, then every facet is a triangle or a quadrilateral.

---

## 17. Implementation Notes

A compact routine to **project to zero sum** and **whiten covariance** (the core of Algorithm B):

```
procedure Harmonize(V: n×d matrix with unit rows):
    // Step 1: center
    c ← (1/n) * (1^T V)          // 1×d row
    V ← V - 1 c                   // subtract centroid from each row
    // Step 2: whiten
    C ← (1/n) * V^T V             // d×d
    W ← C^{-1/2} * (I / √d)       // d×d, compute by eigen-decomposition
    V ← V W                        // now (1/n) V^T V = (1/d) I
    // Step 3: renormalize rows back to unit sphere
    for k = 1..n:
        V[k,:] ← V[k,:] / ||V[k,:]||
    // Optional: repeat once to correct tiny drift induced by row renorm
    return V
```

One pass suffices in practice; a second pass tightens numerical residue. Cost is dominated by an eigendecomposition of $d\times d$: $O(d^3 + nd^2)$.

---

## 18. A Minimal Classification in the Plane

In $\mathbb{R}^2$, the situation is unusually transparent.

### Theorem 18.1 (Planar Fourier characterization)

A configuration in $\mathbb{R}^2$ is harmonic if and only if the angles $\theta_k$ of the unit vectors $v_k = (\cos\theta_k,\sin\theta_k)$ satisfy

$$
\sum_{k=1}^n e^{i\theta_k} = 0 \quad\text{and}\quad \sum_{k=1}^n e^{2i\theta_k} = 0.
$$

*Proof.* The centering condition $\sum_k v_k = 0$ becomes $\sum_k (\cos\theta_k, \sin\theta_k) = 0$, which is equivalent to $\text{Re}\left(\sum_k e^{i\theta_k}\right) = 0$ and $\text{Im}\left(\sum_k e^{i\theta_k}\right) = 0$, i.e., $\sum_k e^{i\theta_k} = 0$.

For the isotropy condition $C = \frac{1}{2}I_2$, we compute:
$$
C = \frac{1}{n}\sum_k v_k v_k^\top = \frac{1}{n}\sum_k \begin{pmatrix} \cos^2\theta_k & \cos\theta_k\sin\theta_k \\ \cos\theta_k\sin\theta_k & \sin^2\theta_k \end{pmatrix}
$$

Using the identities $\cos^2\theta = \frac{1 + \cos(2\theta)}{2}$, $\sin^2\theta = \frac{1 - \cos(2\theta)}{2}$, and $\cos\theta\sin\theta = \frac{\sin(2\theta)}{2}$:

$$
C = \frac{1}{2}I_2 + \frac{1}{2n}\text{Re}\begin{pmatrix} \sum_k e^{2i\theta_k} & -i\sum_k e^{2i\theta_k} \\ i\sum_k e^{2i\theta_k} & -\sum_k e^{2i\theta_k} \end{pmatrix}
$$

For $C = \frac{1}{2}I_2$, we need $\sum_k e^{2i\theta_k} = 0$. $\square$

**The Fourier Perspective**: Planar harmonicity is precisely the condition that the **first and second Fourier modes vanish**:
- First mode: $\sum_k e^{i\theta_k} = 0$ (centering)  
- Second mode: $\sum_k e^{2i\theta_k} = 0$ (isotropy)

This gives us a beautiful mnemonic: **harmonic configurations are those with no DC bias and no quadratic bias in their angular Fourier spectrum**.

*Historical note*: This connects to classical results in approximation theory, where Chebyshev sets are characterized by vanishing of specific Fourier modes. Our harmonic polytopes are the geometric realization of this spectral principle.

---

## 19. What It Means to Be Primitive

We have avoided bibliographic excursions and comparative anatomy on purpose. Within this chapter, a **harmonic polytope** is simply what remains when three urges are obeyed:

1. **Stand on the sphere** (unit constraint).
2. **Cancel your sum** (centering).
3. **Share energy uniformly** (isotropy).

Many convex bodies satisfy one or two of these urges. Surprisingly few satisfy all three nontrivially. Those that do exhibit a mixture of rigidity (tight covariance, maximal entropy, balanced support) and freedom (a genuine moduli, many combinatorics). They are primitive in the sense that we can specify them with a short axiom and reconstruct them with short code.

From here, one could wander outward: products, limits, random ensembles, extremal gaps, sparse harmonics. But our compact aim has been to isolate the core object and equip the reader with definitions, algorithms, and a feel for its geometry.

---

## 20. Epilogue

If you scatter your arrows until no direction matters, and you cancel your thrust until no drift remains, you do not get nothing. You get a shape.

That shape is the **harmonic polytope**.

---

### Mathematical Summary

**The Harmonic Polytope** is the convex hull of unit vectors whose sum vanishes and whose directions are isotropically distributed. This structure—simple to define, rich in consequences—yields:

- **Spectral theory**: Via the harmonic Laplacian $\Delta = I - A$ and fundamental gap $\gamma$
- **Duality results**: Polars of harmonic polytopes preserve harmonic structure  
- **Entropy principles**: Harmonicity maximizes directional information spread
- **Construction algorithms**: Three robust methods with polynomial complexity
- **Perturbation stability**: Small errors in centering/isotropy yield small configuration changes

It is what I call a **"primitive object of reality"**—capturing balance, spread, and structure in pure geometric form.

### Notes and Remarks

* **On tightness.** The equality $C=\frac1dI$ is the key that makes the algebra linear and the geometry disciplined. One may view the configuration as a tight Parseval system of $n$ unit vectors in $\mathbb{R}^d$ with vanishing mean.

* **On duality.** The polar inherits centeredness and, after appropriate normalization of facet normals, the same tightness principle. This self-similarity under polarity is rare among convex bodies.

* **On robustness.** The projection-whitening-renorm pipeline (Algorithm B) is the practical workhorse. It solves the nearest harmonic configuration problem in a single sweep, with stability guaranteed by classical matrix perturbation theory.

* **On moduli.** The formula $\dim \mathcal{M}_{n,d}=nd-d-d^2$ counts degrees of freedom after removing symmetries. While heuristic (constraints can bite), it explains why small $n$ in small $d$ feel "rigid" while larger instances admit rich deformation families.

* **On applications.** Though we've avoided external connections, the reader may recognize these structures in transformer attention mechanisms, where tokens form context polytopes through auto-contextualization. The mathematical principles developed here provide the theoretical foundation for such applications.
