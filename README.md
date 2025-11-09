# Vector & Matrix Visualizer — A Research Notebook–Style Walkthrough

> A compact, reproducible study of 2D vectors, linear transformations, and geometric intuition using NumPy and Matplotlib.

## Abstract
This notebook explores core concepts from linear algebra in 2D: vectors, vector operations, projections, and matrix-induced linear transformations. We pair concise mathematical definitions with visual demonstrations to build geometric intuition. The primary artifact is the Jupyter notebook `playground.ipynb`, which renders vector fields, basis transformations, and the effect of a 2×2 matrix on a grid.

Keywords: linear algebra, vectors, projections, matrices, linear transformations, visualization, NumPy, Matplotlib.

## Repository contents
- `playground.ipynb` — The research-style notebook with code, plots, and explanations.
- `requirements.txt` — Minimal Python dependencies for reproducible runs.
- `README.md` — You are here.

## Reproducibility and environment
- Python: 3.9+ (3.10 recommended)
- OS: Linux, macOS, Windows

Install dependencies in an isolated environment:

```bash
# create and activate a virtual environment (Linux/macOS)
python3 -m venv .venv
source .venv/bin/activate

# install packages
pip install -r requirements.txt
```

Open the notebook in your preferred tool:

```bash
# Option A: Jupyter Lab
jupyter lab playground.ipynb

# Option B: VS Code (with the Jupyter extension)
code playground.ipynb
```

## How to use
1. Open `playground.ipynb` and run cells top-to-bottom.
2. Modify the example vectors `v1`, `v2`, or the 2×2 matrix `A` in the later sections to experiment.
3. Re-run the relevant cells to see how the geometry changes.

## Mathematical background (concise)
- Vectors in $\mathbb{R}^2$: $\mathbf{v} = [x, y]$.
- Vector addition: $\mathbf{a} + \mathbf{b} = [a_x + b_x,\ a_y + b_y]$.
- Scalar multiplication: $c\,\mathbf{v} = [c x,\ c y]$.
- Dot product and angle:
  $$\mathbf{a}\cdot\mathbf{b} = a_x b_x + a_y b_y,\quad \cos\theta = \frac{\mathbf{a}\cdot\mathbf{b}}{\lVert\mathbf{a}\rVert\,\lVert\mathbf{b}\rVert}$$
- Projection of $\mathbf{a}$ onto $\mathbf{b}$:
  $$\mathrm{proj}_{\mathbf{b}}(\mathbf{a}) = \frac{\mathbf{a}\cdot\mathbf{b}}{\mathbf{b}\cdot\mathbf{b}}\,\mathbf{b}$$
- Linear transformation by a 2×2 matrix $A$:
  $$\mathbf{v}' = A\,\mathbf{v},\quad A = [\,A\,\mathbf{e}_1\mid A\,\mathbf{e}_2\,]$$
  where $\mathbf{e}_1=[1,0]^\top,\ \mathbf{e}_2=[0,1]^\top$ are the standard basis.
- Determinant (area scale in 2D): $|\det(A)|$ scales areas; negative sign indicates orientation flip.

## Notebook roadmap (what each section demonstrates)
1. Import and styling — Configure NumPy, Matplotlib, and a clean plotting style.
2. Visualizing 2D vectors — `plot_vectors(...)` draws arrows from the origin with labels and grid.
3. Vector operations — Functions for addition, subtraction, scalar multiplication, and dot product.
4. Projection — `plot_projection(a, b)` shows $\mathrm{proj}_b(a)$ and the perpendicular residual $\mathbf{a}-\mathrm{proj}_b(\mathbf{a})$.
5. Matrix transformation — `visualize_matrix(A)` illustrates how a 2×2 matrix acts on the plane by:
   - Drawing the original grid and standard basis $\{\mathbf{e}_1, \mathbf{e}_2\}$.
   - Applying $A$ to every grid point and to the basis, plotting $A\mathbf{e}_1$ and $A\mathbf{e}_2$.
   - Optionally showing a sample vector $\mathbf{v} = 2\mathbf{e}_1 + 3\mathbf{e}_2$ and its image $A\mathbf{v}$.
6. Determinant — Computes $\det(A)$ and interprets it as area scaling.

## The core visual: `visualize_matrix(A)`
This function is the geometric heart of the notebook.

- Input: `A` (2×2 NumPy array)
- Output: A side-by-side figure with the original space and the transformed space.
- Method:
  - Build a lattice on $[-2,2]\times[-2,2]$ and apply $A$ to all points.
  - Plot original basis $\mathbf{e}_1,\mathbf{e}_2$ and their images $A\mathbf{e}_1, A\mathbf{e}_2$.
  - Show how squares become parallelograms (shear), grow/shrink (scales), or rotate.
- What you learn:
  - The columns of $A$ are the images of the basis vectors.
  - $\det(A)$ shows area change; sign shows orientation.

Try changing `A` to see different behaviors:

```python
# Pure scaling
A = np.array([[2, 0],
              [0, 2]])

# Shear
A = np.array([[1, 1],
              [0, 1]])

# Rotation by ~45° (approx.)
A = np.array([[ 0.7071, -0.7071],
              [ 0.7071,  0.7071]])
```

## Example session (quick start)
Inside the notebook, you’ll find examples like:

```python
v1 = np.array([2, 1])
v2 = np.array([1, 3])
plot_vectors([v1, v2], colors=["r", "g"])  # visualize two vectors

# Vector operations
dot_product(v1, v2)
vector_addition(v1, v2)
vector_subtraction(v1, v2)
scalar_multiplication(v1)

# Projection
plot_projection(v1, v2)

# Matrix transform
A = np.array([[1, 2],
              [2, 1]])
visualize_matrix(A)
```

## Interpretation guide
- Parallel grid lines after transformation indicate linearity (no bending/curvature).
- If $\det(A)=0$, the grid collapses to a line — the transformation is singular (non-invertible).
- Very large entries in `A` may require adjusting the axis limits for visibility.

## Troubleshooting
- Shapes must match: `A` must be 2×2; vectors must be length-2.
- If plots don’t show, ensure your environment supports graphical backends (Jupyter in browser or VS Code).
- If labels overlap, tweak figure size or axis limits.

## Extending the notebook
- Add eigenvectors/eigenvalues and overlay invariant directions when they exist.
- Animate interpolation from the identity to `A` to see the transformation “unfold.”
- Color-code grid cells to show orientation flips (positive vs. negative determinant).
- Return `fig, axes` from plotting functions to enable composition and saving.

## Attribution
- Built with NumPy and Matplotlib.
- Educational framing inspired by classic linear algebra pedagogy on geometric interpretations of matrices.

---
If you use or adapt this notebook for teaching or demos, a link back to this repository is appreciated.