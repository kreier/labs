# Bifurcations

While trying Mathematica on the Raspberry Pi 4 I noticed the performance improvements. Since a calculation of a bifurcation was the screenshot for the wikipedia page I tried to replicate the output. I was looking for this:



But the 40 seconds didn't compute for my little ARM CPU. I tried Anaconda as well These are the results by language:

## Mathematica


## Jupyter notebook

``` py
import numpy as np
import matplotlib.pyplot as plt

# Logistic function implementation
def logistic_eq(r,x):
    return r*x*(1-x)

# Create the bifurcation diagram
def bifurcation_diagram(seed, n_skip, n_iter, step=0.0001, r_min=0):
    print("Starting with x0 seed {0}, skip plotting first {1} iterations, then plot next {2} iterations.".format(seed, n_skip, n_iter));
    # Array of r values, the x axis of the bifurcation plot
    R = []
    # Array of x_t values, the y axis of the bifurcation plot
    X = []
    
    # Create the r values to loop. For each r value we will plot n_iter points
    r_range = np.linspace(r_min, 4, int(1/step))

    for r in r_range:
        x = seed;
        # For each r, iterate the logistic function and collect datapoint if n_skip iterations have occurred
        for i in range(n_iter+n_skip+1):
            if i >= n_skip:
                R.append(r)
                X.append(x)
                
            x = logistic_eq(r,x);
    # Plot the data    
    plt.plot(R, X, ls='', marker=',')
    plt.ylim(0, 1)
    plt.xlim(r_min, 4)
    plt.xlabel('r')
    plt.ylabel('X')
    plt.show()

bifurcation_diagram(0.2, 100, 10, r_min=3.55)
```
![bifurcation](pic/bifurcation.png)
