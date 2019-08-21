# matplotlib
从宏观上理解matplotlib的框架、机制十分重要。虽然它不能直接找到鱼，但它能引导你找到渔，进而找到鱼。否则，就会沦陷到每次使用都得去查google或者去查之前的示例的境地，永远也掌握不了matplotlib的关键脉络！


# matplotlib有两套接口
matplotlib有两套接口，第一套基于MATLAB，基于状态；第二套是面向对象的接口（OO）。
## 第一套接口：pyplot模块。
这一套接口模仿MATLAB，基于状态来使用。 matplotlib.pyplot模块是一系列的函数命令集合，每一个函数对图形（figure）进行一些变更操作：如创建figure，在figure中创建一个画图区域，在画图区域中画线、装饰画图区域等。这个figure的状态随着pyplot中函数的调用而改变，但这些改变的状态会被跨函数保存。 所以，可以跟踪当前图形及绘图区域等。
pyplot API相对于面向对象的API来说缺少灵活性。 pyplot中的大部分函数都可由Axes的方法来替代。
The first is based on MATLAB and uses a state-based interface. This is encapsulated in the pyplot module.
matplotlib.pyplot is a collection of command style functions that make matplotlib work like MATLAB. Each pyplot function makes some change to a figure: e.g., creates a figure, creates a plotting area in a figure, plots some lines in a plotting area, decorates the plot with labels, etc.

In matplotlib.pyplot various states are preserved across function calls, so that it keeps track of things like the current figure and plotting area, and the plotting functions are directed to the current axes (please note that "axes" here and in most places in the documentation refers to the axes part of a figure and not the strict mathematical term for more than one axis).

the pyplot API is generally less-flexible than the object-oriented API. Most of the function calls you see here can also be called as methods from an Axes object. 

## 第二套接口： 面向对象的接口 object-oriented interface
在面向对象的接口中，整个过程就是使用axes.Axes的实例来渲染一个figure.Figure的实例。
Matplotlib has two interfaces. The first is an object-oriented (OO) interface. In this case, we utilize an instance of axes.Axes in order to render visualizations on an instance of figure.Figure.

## 

# Reference
1. [effective-matplotlib](https://pbpython.com/effective-matplotlib.html)
2. [The Lifecycle of a Plot](https://matplotlib.org/tutorials/introductory/lifecycle.html#sphx-glr-tutorials-introductory-lifecycle-py)
3. [Pyplot tutorial](https://matplotlib.org/tutorials/introductory/pyplot.html)
