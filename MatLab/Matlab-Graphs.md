# Matlab Graphs

Graphing and graphics with MatLab.

* [MatLab Documentation](https://uk.mathworks.com/help/)
* [MathWorks 2-D and 3-D Plots](https://uk.mathworks.com/help/matlab/learn_matlab/plots.html)

## 2D Plots

Simple line plots can be created with the `plot` function, examples:

```MatLab
% Plot a sine curve
x = 0:pi/100:2*pi % Generate a range of values
y = sin(x) % Get the sine of those values
plot(x,y) % Plot them

xlabel('x') % Label X axis
ylabel('y, sin(x)') % Label Y axis
title('Plot of the Sine Function') % Title graph
```

## 3D Plots

## Graphing and Drawing

* `gcf` returns a handle to the current figure, or creates one if no figures are active.