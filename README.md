# Matplotlib's _fill_between_ in 3D

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/LICENSE.md)
![Last Commit](https://img.shields.io/github/last-commit/artmenlope/matplotlib-fill_between-in-3D)

The purpose of this repository is to show an example of a way of bringing the Python 3 `matplotlib.pyplot.fill_between` function to 3D plots.

The main `fill_between_3d` function can be found in the [_FillBetween3d.py_](https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/FillBetween3d.py) file of this repository.

## Examples of use:

The needed imports for these three examples will be
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from mpl_toolkits.mplot3d.art3d import Poly3DCollection
```

### Example 1

This example shows how to plot three lines with `fill_between_3d` applied to them in three different equidistant layers. The code is the following:

```python
# x axis 1D space.
x = np.linspace(-10,10,100)

# Define the three functions to plot.
f1 = np.sin(0.25*x)**2 * np.exp(-0.1*(x+0.7)**2) 
f2 = np.sin( 0.5*x)**2 * np.exp(-0.1*(x+0.7)**2)
f3 = np.sin(     x)**2 * np.exp(-0.1*(x+0.7)**2)

# Sets of [x, y, 0] lines (with constant y) for defining the bases of the polygons.
set01 = [x, -7*np.ones(len(x)), np.zeros(len(x))]
set02 = [x,  0*np.ones(len(x)), np.zeros(len(x))]
set03 = [x,  7*np.ones(len(x)), np.zeros(len(x))]

# Sets of the form [x, y, fi] (with constant y) representing each function 3D line.
set1  = [x, -7*np.ones(len(x)), f1]
set2  = [x,  0*np.ones(len(x)), f2]
set3  = [x,  7*np.ones(len(x)), f3]

# Plotting part. Figure and axes creation.
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d', xlim=(-10,10), ylim=(-10,10))

# Plot the f1 line and its fill_between_3d.
ax.plot(*set1, lw=2, zorder=20, c="C0")
fill_between_3d(ax, *set01, *set1, mode = 1, c="C0")

# Plot the f2 line and its fill_between_3d.
ax.plot(*set2, lw=2, zorder=15, c="C1")
fill_between_3d(ax, *set02, *set2, mode = 1, c="C1")

# Plot the f3 line and its fill_between_3d.
ax.plot(*set3, lw=2, zorder=10, c="C2")
fill_between_3d(ax, *set03, *set3, mode = 1, c="C2")

# Correct the z limit of the plot.
ax.set_zlim((0,np.max([f1,f2,f3])))

# Show the plot.
plt.show()
```

The result is

<p align="center">
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/images/example1.svg" width="60%">
</p>


### Example 2

This second example shows how the `fill_between_3d` function fills the area between two arbitrary lines laying in the 3d space.

```python
x = np.linspace(-1,1,100)
y = np.linspace(-1,1,100)

set1 = [x, np.cos(2*np.pi*y), np.sin(2*np.pi*y)]     # x, y, z coordinates of the first line (x1, y1, z1)
set2 = [x, 2*np.cos(2*np.pi*y), 2*np.sin(2*np.pi*y)] # x, y, z coordinates of the second line (x2, y2, z2)

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

ax.plot(*set1, lw=4)
ax.plot(*set2, lw=4)
fill_between_3d(ax, *set1, *set2, mode = 1)

plt.show()
``` 

<p align="center">
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/images/example2.svg" width="60%">
</p>

### Example 3

This function can also be used to fill the area between two lines like the matplotlib's `fill_between` function does in 2D plots but with 3D lines.

```python
x = np.linspace(-2,2,100)
y = np.linspace(-2,2,100)

set1 = [x, np.zeros(len(x)), np.exp(-(x-0.5)**2)]
set2 = [x, np.zeros(len(x)), 0.5*np.exp(-(x)**2)]

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

ax.plot(*set1, lw=4)
ax.plot(*set2, lw=4)
fill_between_3d(ax, *set1, *set2, mode = 1)

plt.show()
```

<p align="center">
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/images/example3.svg" width="60%">
</p>

Adding 

```python
X, Y = np.meshgrid(x, y)
Z = 0.5*np.exp(-(X**2+Y**2))

ax.plot_surface(X, Y, Z, color='darkorange', alpha=0.8)
```
to the code of this example results in: 

<p align="center">
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/images/example3b.svg" width="60%">
</p>
