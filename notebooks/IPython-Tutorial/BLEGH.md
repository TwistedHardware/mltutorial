
# Tutorial Brief

IPython notebook provides a variaty of web widgets that can interact with python code running the the background kernel.

Finding Help:

- http://nbviewer.ipython.org/github/ipython/ipython/blob/2.x/examples/Interactive%20Widgets/Index.ipynb

<table>
<tr>
    <td><img src="http://www.scipy.org/_static/images/numpylogo_med.png"  style="width:50px;height:50px;" /></td>
    <td><h4>NumPy</h4> Base N-dimensional array package </td>
    <td><img src="http://www.scipy.org/_static/images/scipy_med.png" style="width:50px;height:50px;" /></td>
    <td><h4>SciPy</h4> Fundamental library for scientific computing </td>
    <td><img src="http://www.scipy.org/_static/images/matplotlib_med.png" style="width:50px;height:50px;" /></td>
    <td><h4>Matplotlib</h4> Comprehensive 2D Plotting </td>
</tr>
<tr>
    <td style="background:Lavender;"><img src="http://www.scipy.org/_static/images/ipython.png" style="width:50px;height:50px;" /></td>
    <td style="background:Lavender;"><h4>IPython</h4> Enhanced Interactive Console </td>
    <td><img src="http://www.scipy.org/_static/images/sympy_logo.png" style="width:50px;height:50px;" /></td>
    <td><h4>SymPy</h4> Symbolic mathematics </td>
    <td><img src="http://www.scipy.org/_static/images/pandas_badge2.jpg" style="width:50px;height:50px;" /></td>
    <td><h4>Pandas</h4> Data structures & analysis </td>
</tr>
</table>

# Why do we use widgets?

> ##IPython includes an architecture for interactive widgets that tie together Python code running in the kernel and JavaScript/HTML/CSS running in the browser. These widgets enable users to explore their code and data interactively.
> *http://nbviewer.ipython.org/github/ipython/ipython/blob/2.x/examples/Interactive%20Widgets/Index.ipynb*

# Import libraries


```python
import numpy as np
import matplotlib.pyplot as plt
```


```python
from __future__ import print_function
from ipywidgets import interact, interactive, fixed, interact_manual
import ipywidgets as widgets
from IPython.display import display
```

## Build-it Widgets


```python
# had to rename the modules from the widget library e.g. widgets.ButtonWidget is now widgegts.Button
# also had to conda install ipython-notebook to get the widgets package (for those of you who still get errors and aren't sure you've installed it.)
```


```python
    tab1_children = [widgets.Button(description="ButtonWidget"),
                 widgets.Checkbox(description="CheckboxWidget"),
                 widgets.Dropdown (values=[1, 2], description="DropdownWidget"),
                 widgets.RadioButtons(values=[1, 2], description="RadioButtonsWidget"),
                 widgets.Select(values=[1, 2], description="SelectWidget"),
                 widgets.Text(description="TextWidget"),
                 widgets.Textarea(description="TextareaWidget"),
                 widgets.ToggleButton(description="ToggleButtonWidget"),
                 widgets.ToggleButtons (values=["Value 1", "Value2"], description="ToggleButtonsWidget"),
                 ]

    tab2_children = [widgets.BoundedFloatText(description="BoundedFloatTextWidget"),
                 widgets.BoundedIntText(description="BoundedIntTextWidget"),
                 widgets.FloatSlider(description="FloatSliderWidget"),
                 widgets.FloatText(description="FloatTextWidget"),
                 widgets.IntSlider(description="IntSliderWidget"),
                 widgets.IntText(description="IntTextWidget"),
                 ]

    tab1 = widgets.Box(children=tab1_children)
    tab2 = widgets.Box(children=tab2_children)


    i = widgets.Accordion (children=[tab1, tab2])

    i.set_title(0,"Basic Widgets")
    i.set_title(1,"Numbers Input")

display(i)
```

# Simple Example

We will define a function that print the factorial.

$f(x) = x!$

$f(x) = x \times (x-1) \times ... 1$

$f(3) = 3! = 3 \times 2 \times 1 = 6$


```python
#new version of Python changes Print from statement to function. () needed now.
def factorial(x):
    print ("%s! = %s" % (x,np.math.factorial(x)));

def factorial2(x):
    if type(x) == int:
        if x >= 0:
            print (np.prod(np.arange(1,x+1)))
        else:
            print ("ERROR: Number must be positive")
    else:
        print ("ERROR: Only interger is allowed")
```

Now we will test it using a code cell


```python
factorial(3)
```

    3! = 6



```python
factorial2(3)
```

    6


# Using interact function

We will link that to a slider to make the x a variable that we can control.


```python
i = interact(factorial, x=(0,100))
```

    50! = 30414093201713378043612608166064768844377641568960512000000000000


## Controlling a Chart


```python
#This function plot x, y and adds a title
def plt_arrays(x, y, title="", color="red", linestyle="dashed", linewidth=2):
    fig = plt.figure()
    axes = fig.add_subplot(111)
    axes.plot(x,y, color=color, linestyle=linestyle, linewidth=linewidth)
    axes.set_title(title)
    axes.grid()
    plt.show()
```

We will define a function that return the following:

$f(x) = ax^3 + bx^2 + cx + d$

where a,b,c and d are are constants.


```python
def f(a, b, c, d, **kwargs):
    x=np.linspace(-10, 10, 20)
    y = a*(x**3) + b*(x**2) + c*x + d 
    
    title="$f(x) = (%s)x^{3} + (%s)x^{2} + (%s)x + (%s)$" % (a,b,c,d)
    
    plt_arrays(x,y, title=title, **kwargs)
```


```python
#Define Constants
a=0.25
b=2
c=-4
d=0


f(a, b, c, d,)
```


![png](output_24_0.png)



```python
i = interact(f,
             a=(-10.,10),
             b=(-10.,10),
             c=(-10.,10),
             d=(-10.,10),
             color = ["red", "blue", "green"],
             linestyle=["solid", "dashed"],
             linewidth=(1,5)
             )
```


![png](output_25_0.png)


## Displaying a widget from interact function


```python
i.widget
```


![png](output_27_0.png)

