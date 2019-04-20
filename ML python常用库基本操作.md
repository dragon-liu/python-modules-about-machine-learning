## NumPy

**What do you need to know to get started?**

- Know how to create arrays : `array`, `arange`, `ones`, `zeros`.

- Know the shape of the array with `array.shape`, then use slicing to obtain different views of the array: `array[::2]`, etc. Adjust the shape of the array using `reshape` or flatten it with `ravel`.

- Obtain a subset of the elements of an array and/or modify their values with masks

  ```python
  a[a < 0] = 0
  ```

- Know miscellaneous operations on arrays, such as finding the mean or max (`array.max()`, `array.mean()`). No need to retain everything, but have the reflex to search in the documentation (online docs, `help()`, `lookfor()`)!!

- For advanced use: master the indexing with arrays of integers, as well as broadcasting. Know more NumPy functions to handle various array operations.

## Matplotlib: plotting

```python
首先，在代码的开始加上%matplotlib inline(针对jupyter notebook)会即时显示图像而不用每次都plt.show()
```

```python
#这一小块代码可以在一个图中同时画出sin和cos
import numpy as np
import matplotlib.pyplot as plt

X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
C, S = np.cos(X), np.sin(X)

plt.plot(X, C)
plt.plot(X, S)

plt.show()
```

- 接下来看一下各种图像参数的设定

  ```python
  import numpy as np
  import matplotlib.pyplot as plt
  
  # Create a figure of size 8x6 inches, 80 dots per inch
  plt.figure(figsize=(8, 6), dpi=80)
  
  # Create a new subplot from a grid of 1x1
  plt.subplot(1, 1, 1)
  
  X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
  C, S = np.cos(X), np.sin(X)
  
  # Plot cosine with a blue continuous line of width 1 (pixels)
  plt.plot(X, C, color="blue", linewidth=1.0, linestyle="-")
  
  # Plot sine with a green continuous line of width 1 (pixels)
  plt.plot(X, S, color="green", linewidth=1.0, linestyle="-")
  
  # Set x limits
  plt.xlim(-4.0, 4.0)
  
  # Set x ticks
  plt.xticks(np.linspace(-4, 4, 9, endpoint=True))
  
  # Set y limits
  plt.ylim(-1.0, 1.0)
  
  # Set y ticks
  plt.yticks(np.linspace(-1, 1, 5, endpoint=True))
  
  # Save figure using 72 dots per inch
  # plt.savefig("exercise_2.png", dpi=72)
  
  # Show result on screen
  plt.show()
  ```

  ## [Figures, Subplots, Axes and Ticks](http://scipy-lectures.org/intro/matplotlib/index.html#id67)

  - A **“figure”** in matplotlib means the whole window in the user interface. Within this figure there can be **“subplots”**.

  - So far we have used implicit figure and axes creation. This is handy for fast plots. We can have more control over the display using figure, subplot, and axes explicitly. While subplot positions the plots in a regular grid, axes allows free placement within the figure. Both can be useful depending on your intention. We’ve already worked with figures and subplots without explicitly calling them. When we call plot, matplotlib calls [`gca()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.gca.html#matplotlib.pyplot.gca) to get the current axes and gca in turn calls [`gcf()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.gcf.html#matplotlib.pyplot.gcf) to get the current figure. If there is none it calls [`figure()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html#matplotlib.pyplot.figure) to make one, strictly speaking, to make a `subplot(111)`. Let’s look at the details.

- ### 1.Figures

  A figure is the windows in the GUI that has “Figure #” as title. Figures are numbered starting from 1 as opposed to the normal Python way starting from 0. This is clearly MATLAB-style. There are several parameters that determine what the figure looks like:

  | Argument    | Default            | Description                                 |
  | ----------- | ------------------ | ------------------------------------------- |
  | `num`       | `1`                | number of figure                            |
  | `figsize`   | `figure.figsize`   | figure size in inches (width, height)       |
  | `dpi`       | `figure.dpi`       | resolution in dots per inch                 |
  | `facecolor` | `figure.facecolor` | color of the drawing background             |
  | `edgecolor` | `figure.edgecolor` | color of edge around the drawing background |
  | `frameon`   | `True`             | draw figure frame or not                    |

  The defaults can be specified in the resource file and will be used most of the time. Only the number of the figure is frequently changed.

  As with other objects, you can set figure properties also setp or with the set_something methods.

  When you work with the GUI you can close a figure by clicking on the x in the upper right corner. But you can close a figure programmatically by calling close. Depending on the argument it closes (1) the current figure (no argument), (2) a specific figure (figure number or figure instance as argument), or (3) all figures (`"all"` as argument).

  ```python
  plt.close(1)     # Closes figure 1
  ```

    

- ### 2.Subplots

  With subplot you can arrange plots in a regular grid. You need to specify the number of rows and columns and the number of the plot. Note that the [gridspec](http://matplotlib.org/users/gridspec.html) command is a more powerful alternative.

  ![../../_images/sphx_glr_plot_subplot-horizontal_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_subplot-horizontal_001.png)

   

  ![../../_images/sphx_glr_plot_subplot-vertical_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_subplot-vertical_001.png)

   

  ![../../_images/sphx_glr_plot_subplot-grid_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_subplot-grid_001.png)

   

  ![../../_images/sphx_glr_plot_gridspec_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_gridspec_001.png)

  ### 3.Axes

  Axes are very similar to subplots but allow placement of plots at any location in the figure. So if we want to put a smaller plot inside a bigger one we do so with axes.

  [![../../_images/sphx_glr_plot_axes_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_axes_001.png)](http://scipy-lectures.org/intro/matplotlib/auto_examples/plot_axes.html) [![../../_images/sphx_glr_plot_axes-2_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_axes-2_001.png)](http://scipy-lectures.org/intro/matplotlib/auto_examples/plot_axes-2.html)

  ### 4.Ticks

  Well formatted ticks are an important part of publishing-ready figures. Matplotlib provides a totally configurable system for ticks. There are tick locators to specify where ticks should appear and tick formatters to give ticks the appearance you want. Major and minor ticks can be located and formatted independently from each other. Per default minor ticks are not shown, i.e. there is only an empty list for them because it is as `NullLocator` (see below).

  #### Tick Locators

  Tick locators control the positions of the ticks. They are set as follows:

  ```python
  ax = plt.gca()
  ax.xaxis.set_major_locator(eval(locator))
  ```

  There are several locators for different kind of requirements:

  ![../../_images/sphx_glr_plot_ticks_001.png](http://scipy-lectures.org/_images/sphx_glr_plot_ticks_001.png)

  All of these locators derive from the base class [`matplotlib.ticker.Locator`](https://matplotlib.org/api/ticker_api.html#matplotlib.ticker.Locator). You can make your own locator deriving from it. Handling dates as ticks can be especially tricky. Therefore, matplotlib provides special locators in matplotlib.dates.

  

  ## Pandas

  - ### Series

    [`Series`](http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html#pandas.Series) is a one-dimensional labeled array capable of holding any data type (integers, strings, floating point numbers, Python objects, etc.). The axis labels are collectively referred to as the **index**. The basic method to create a Series is to call:

    ```python
    s = pd.Series(data, index=index)
    ```

    Here, `data` can be many different things:

    - a Python dict
    - an ndarray
    - a scalar value (like 5)

    The passed **index** is a list of axis labels. Thus, this separates into a few cases depending on what **data is**:

    **From ndarray**

    If `data` is an ndarray, **index** must be the same length as **data**. If no index is passed, one will be created having values `[0, ..., len(data) - 1]`.

  ```python
  In [3]: s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
  
  In [4]: s
  Out[4]: 
  a    0.469112
  b   -0.282863
  c   -1.509059
  d   -1.135632
  e    1.212112
  dtype: float64
  
  In [5]: s.index
  Out[5]: Index(['a', 'b', 'c', 'd', 'e'], dtype='object')
  
  In [6]: pd.Series(np.random.randn(5))
  Out[6]: 
  0   -0.173215
  1    0.119209
  2   -1.044236
  3   -0.861849
  4   -2.104569
  dtype: float64
  ```

  **From dict**

  Series can be instantiated from dicts:

```python
In [7]: d = {'b': 1, 'a': 0, 'c': 2}

In [8]: pd.Series(d)
Out[8]: 
b    1
a    0
c    2
dtype: int64
```

**Note**

When the data is a dict, and an index is not passed, the `Series`index will be ordered by the dict’s insertion order, if you’re using Python version >= 3.6 and Pandas version >= 0.23.

If you’re using Python < 3.6 or Pandas < 0.23, and an index is not passed, the `Series` index will be the lexically ordered list of dict keys.

In the example above, if you were on a Python version lower than 3.6 or a Pandas version lower than 0.23, the `Series` would be ordered by the lexical order of the dict keys (i.e. `['a', 'b', 'c']` rather than `['b', 'a', 'c']`).

If an index is passed, the values in data corresponding to the labels in the index will be pulled out.

```python
In [9]: d = {'a': 0., 'b': 1., 'c': 2.}

In [10]: pd.Series(d)
Out[10]: 
a    0.0
b    1.0
c    2.0
dtype: float64

In [11]: pd.Series(d, index=['b', 'c', 'd', 'a'])
Out[11]: 
b    1.0
c    2.0
d    NaN
a    0.0
dtype: float64
```

**Note:**

NaN (not a number) is the standard missing data marker used in pandas.

**From scalar value**

If `data` is a scalar value, an index must be provided. The value will be repeated to match the length of **index**.

```python
In [12]: pd.Series(5., index=['a', 'b', 'c', 'd', 'e'])
Out[12]: 
a    5.0
b    5.0
c    5.0
d    5.0
e    5.0
dtype: float64
```

