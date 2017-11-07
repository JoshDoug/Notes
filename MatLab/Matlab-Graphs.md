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

When used, `hold on` will ensure all plots appear in the current figure window until `hold off`, `close`, or another figure is used (probably). If there are multiple figures open then `close all` can be used to close all of them in one go.

## Subplots

Multiple plots can be made in the same window using the subplot function. Each plot is preceded by a call to `subplot` which specifies the size of the subplot grid (they're set in a grid layout with rows and columns) and the place within the grid of the plot. E.g. `subplot(2, 2, 3)` would specify a 2x2 grid with the plot in the 3rd portion, which would place it in column 1, row 2.

```MatLab
% Sample 2x2 Subplot
t = 0:pi/10:2*pi;
[X,Y,Z] = cylinder(4*cos(t));
subplot(2,2,1); mesh(X); title('X');
subplot(2,2,2); mesh(Y); title('Y');
subplot(2,2,3); mesh(Z); title('Z');
subplot(2,2,4); mesh(X,Y,Z); title('X,Y,Z');
```

## 3D Plots

## Graphing and Drawing

* `gcf` returns a handle to the current figure, or creates one if no figures are active.