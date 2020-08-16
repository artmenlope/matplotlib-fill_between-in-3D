# Matplotlib's _fill_between_ in 3D

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/LICENSE.md)
![Last Commit](https://img.shields.io/github/last-commit/artmenlope/matplotlib-fill_between-in-3D)

The purpose of this repository is to show an example of a way of bringing the Python 3 _matplotlib.pyplot.fill_between_ function to 3D plots.

The main _fill_between_3d_ function can be found in the _FillBetween3d.py_ file of this repository.

## Examples of use:

The needed imports for these examples will be
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from mpl_toolkits.mplot3d.art3d import Poly3DCollection
```


### Example 1

This first example shows how the _fill_between_3d_ function fills the area between two lines laying in the 3d space.

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
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/example1.svg" width="50%">
</p>

### Example 2

This function can also be used to fill the area between two lines like the matplotlib's _fill_between_ function does in 2D plots but with 3D lines.

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
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/example2.svg" width="50%">
</p>

Adding 

```python
X, Y = np.meshgrid(x, y)
Z = 0.5*np.exp(-(X**2+Y**2))

ax.plot_surface(X, Y, Z, color='darkorange', alpha=0.8)
```
to the code of this example results in: 

<p align="center">
<img src="https://github.com/artmenlope/matplotlib-fill_between-in-3D/blob/master/example2b.svg" width="50%">
</p>
