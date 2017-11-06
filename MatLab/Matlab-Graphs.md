# Matlab Graphs

Graphing and graphics with MatLab.

* [MatLab Documentation](https://uk.mathworks.com/help/)
* [MathWorks 2-D and 3-D Plots](https://uk.mathworks.com/help/matlab/learn_matlab/plots.html)

## 2D Plots

Simple line plots can be created with the `plot` function, examples:

```MatLab
% Plot a sine curve
x = 0:pi/100:2*pi; % Generate a range of values
y = sin(x); % Get the sine of those values
plot(x,y) % Plot them

xlabel('x') % Label X axis
ylabel('y, sin(x)') % Label Y axis
title('Plot of the Sine Function') % Title graph
```

The look of the graph can be changed with a third paramater, LineSpec, e.g. `plot(x, y, 'r--')` would graph a red dashed line, `r` red, `--` dashed. Those make up a *line specification*, which can include characters to set color, style, and marker (symbol at each plotted data point). E.g. `'g:*'` requests a green dotted line with `*` markers.

* [2-D line plot documentation](https://uk.mathworks.com/help/matlab/ref/plot.html?searchHighlight=plot&s_tid=doc_srchtitle)

By default MatLab clears the figure each time a plotting function is used in the same context. To add multiple plots to a figure use `hold`:

```MatLab
x = 0:pi/100:2*pi;
y = sin(x);
plot(x, y)

hold on

y2 = cos(x);
plot(x, y2, ':')
legend('sin', 'cos')
```

When used, `hold on` will ensure all plots appear in the current figure window until `hold off`, `close`, or another figure is used (probably).

## 3D Plots

## Graphing and Drawing

* `gcf` returns a handle to the current figure, or creates one if no figures are active.