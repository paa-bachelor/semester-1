# Python for Scientists - Scipy

```py
import numpy as np

from scipy import linalg, optimize, interpolate, fft, integrate, stats
from scipy import signal
from scipy.sparse import diags
```

## 2. Linear System

General linear system.

```py
x = linalg.solve(a, b)
```

LU factorization.

```py
P, L, U = linalg.lu(a, permute_l=False)
L, U = linalg.lu(a, permute_l=True)
# If permute_l=True, L is no longer lower triangular.
```

LU factorization in practice.

```py
lu, piv = linalg.lu_factor(a)
x = linalg.lu_solve((lu, piv), b)
```

Cholesky factorization for positive definite hermitian matrices.

```py
L = linalg.cholesky(a, lower=True)
U = linalg.cholesky(a, lower=False)
```

Cholesky factorization in practice.

```py
cho, lower = linalg.cho_factor(a, lower=lower)
x = linalg.cho_solve((cho, lower), b)
```

Inverse.

```py
inv = linalg.inv(a)
```

Special types of matrices.

```py
x = linalg.solve_banded(a, b)
x = linalg.solveh_banded(a, b)

cho = linalg.cholesky_banded(a, lower=lower)
x = linalg.cho_solve_banded((cho, lower), b)
```

## 3. Linear Least Squares

General LLS.

```py
x, res2, rank, s = linalg.lstsq(a, b)
# res2 is the norm squared of the residual. 
```

QR factorization.

```py
Q, R = linalg.qr(a)
```

SVD decomposition.

```py
U, s, Vh = linalg.svd(a, full_matrices=True)        # full SVD
Up, sp, Vph = linalg.svd(a, full_matrices=False)    # compact SVD
```

Singular values.

```py
s = linalg.svdvals(a)
```

Moore-Penrose Pseudoinverse.

```py
pinv = linalg.pinv(a)
```

Special types of matrices.

```py
pinv = linalg.pinvh(a)
```

## 4. Eigenvalue Problems

General eigenvalue problem.

```py
eigvals, eigvecs = linalg.eig(a)
```

Only eigenvalues.

```py
eigvals = linalg.eigvals(a)
```

Special types of matrices.

```py
eigvals, eigvecs = linalg.eigh(a)
eigvals = linalg.eigvalsh(a)

eigvals, eigvecs = linalg.eig_banded(a)
eigvals = linalg.eigvals_banded(a)

eigvals, eigvecs = linalg.eigh_tridiagonal(a)
eigvals = linalg.eigvals_tridiagonal(a)
```

## 5. Nonlinear Equations

General 1D equation.

```py
x = optimize.brentq(f, [a, b])
```

General ND equation.

```py
res = optimize.root(f, x0)
```

Bisection method.

```py
x = optimize.bisect(f, [a, b])
```

Newton's method & secant method.

```py
x = optimize.newton(f, x0, fp)      # Newton method
x = optimize.newton(f, x0)          # secant method
```

Polynomial roots.

```py
x = np.polynomial.polynomial.polyroots(p)
```

## 6. Optimization Problems

General unconstrained ND problem.

```py
res = optimize.minimize(f, x0, method='Nelder-Mead')
```

General constrained ND problem.

```py
# ----- { NONLINEAR CONSTRAINT FUNCTION } -----
def cons_c(x):
    c = [x[0]**2 + x[1], x[0]**2 - x[1]]
    return c


def cons_J(x):              # optional
    jacobian = [
        [2*x[0], 1], 
        [2*x[0], -1]
    ]
    return jacobian


def cons_H(x, v):           # optional
    hessian_1 = np.array([
        [2, 0], 
        [0, 0]
    ])
    hessian_2 = np.array([
        [2, 0], 
        [0, 0]
    ])
    return v[0] * hessian_1 + v[1] * hessian_2      # return linear combination

# ----- { CONSTRAINT OBJECTS } -----
bounds = optimize.Bounds(
    [0, -0.5],              # lower bounds 
    [1.0, 2.0]              # upper bounds
)
linear_constraint = optimize.LinearConstraint(
    [[1, 2], [2, 1]],       # function matrix 
    [-np.inf, 1],           # lower bounds
    [1, 1]                  # upper bounds
)
nonlinear_constraint = optimize.NonlinearConstraint(
    cons_c,                 # contraint function
    -np.inf,                # lower bounds
    1,                      # upper bounds
    jac=cons_J,             # jacobian matrix
    hess=cons_H             # hessian matrix
)

# ----- { MINIMIZE } -----
res = optimize.minimize(
    f, x0, method='trust-constr', 
    constraints=[linear_constraint, nonlinear_constraint], 
    bounds=bounds
)
```

Golden section search.

```py
x = optimize.golden(f, brack=(a, b))
```

Fixed point iteration.

```py
x = optimize.fixed_point(g, x0, method='iteration')
```

## 7. Interpolation

Lagrange interpolation.

```py
f = interpolate.lagrange(t, y)
```

1D interpolation.

```py
f = interpolate.interp1d(t, y, kind='linear')
f = interpolate.interp1d(t, y, kind='cubic')
```

Cubic spline interpolation.

```py
f = interpolate.CubicSpline(t, y, bc_type='not-a-knot')
f = interpolate.CubicSpline(t, y, bc_type='clamped')
f = interpolate.CubicSpline(t, y, bc_type='natural')
f = interpolate.CubicSpline(t, y, bc_type='periodic')
```

ND interpolation.

```py
Z = interpolate.griddata(points, z, mgrid, method='cubic')
```

## 8. Fast Fourier Transform

DFT.

```py
y = fft.fft(x, n=n)
z = fft.ifft(y, n=n)    # inverse
```

DFT sample frequencies. Nyquist < 0.

```py
freqs = fft.fftfreq(n, d=1/fs)
```

DFT of a real sequence (only half is stored).

```py
y = fft.rfft(x, n=n)
z = fft.irfft(y, n=n)   # inverse
```

DFT sample frequencies (for usage with `rfft`, `irfft`). Nyquist > 0.

```py
freqs = fft.rfftfreq(n, d=1/fs)
```

Compute fast length for FFT.

```py
fast_n = fft.next_fast_len(n, real=real)
```

Convolution.

```py
z = signal.convolve(x, y)                       # uses FFT
z = signal.convolve(x, y, method='direct')      # explicit calculation
```

## 9. Integration

General 1D integration (Clenshaw-Curtis quadrature).

```py
quad, err = integrate.quad(f, a, b)
```

General 2D & 3D integration.

```py
quad2, err = integrate.dblquad(f, ymin, ymax, xmin, xmax)       # xmin, xmax : can be functions of y
quad3, err = integrate.tplquad(f, zmin, zmax, ymin, ymax, xmin, xmax)

# OR, MANUALLY
quad2 = integrate.quad(lambda y: integrate.quad(f, xmin, xmax, args=y)[0], ymin, ymax)
```

Newton-Cotes quadrature.

```py
x = np.linspace(a, b, rn + 1)                   # rn : interpolant degree
                                                # >> effective degree is rn + 1
weights, _ = integrate.newton_cotes(rn, 1)
quad = (b - a)/rn * np.sum(weights * f(x))
```

Gaussian quadrature.

```py
quad, err = integrate.quadrature(f, a, b, maxiter=max_degree)
```

Composite trapezoidal rule.

```py
quad = np.trapz(y, x)
```

Composite Simpson's rule.

```py
quad = integrate.simpson(y, x)      # len(y) odd
```

Romberg integration.

```py
quad = integrate.romberg(f, a, b)
```

## 10. Monte Carlo

Numpy PRNG (PCG).

```py
rng = np.random.default_rng(seed=seed)
```

> Distributions at https://numpy.org/doc/stable/reference/random/index.html.

## 11. ODE

IVP.

```py
# Bogacki-Shampine
sol = integrate.solve_ivp(ODE, [t0, tf], [y0], max_step=h, method="RK23", t_eval)
# Dormand-Prince
sol = integrate.solve_ivp(ODE, [t0, tf], [y0], max_step=h, method="RK45", t_eval)

# stiff ODEs
sol = integrate.solve_ivp(ODE, [t0, tf], [y0], max_step=h, method="LSODA", t_eval)
```

IVP (older API).

```py
sol = integrate.odeint(ODE, y0, t)  
```

BVP.

```py
sol = integrate.solve_bvp(ODE, bc_res, x, y)
# y : initial guess
```