---
title: FoldingText Extensions
date: 2018-11-15 17:53:27
menu: "Projects"
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


[**FoldingText**](http://www.foldingtext.com/) has become my [**Markdown**](http://daringfireball.net/projects/markdown/) editor of choise. I use it along side of [**Marked 2**](http://marked2app.com/). I use my [**FoldingText Alfred workflow**](/#/projects/alfred) to control things. While working with FoldingText, I have created some extensions as well. Give them a try and let me know what you think! If you have ideas you would like to see in FoldingText, let me know and maybe I will write it. I love extending applications.

##### Extensions

**[imath](https://github.com/raguay/math.ftplugin)**

This extension adds the ability to run calculations in FoldingText. Just add the `.imath` to the end of a line. If it is a header, then just write math expressions after it. If it is not on a header, then indent math expressions after it. A line ending in `=>` will start evaluating every line up to the extension line, then search for previous `.imath` section that are not folded, and then evaluates the math. You define variables normally with the `=` sign.

Since previous `.imath` sections that are not folded are evaluated, you can keep cases for variables in folded sections. Remember, the last variable definition will be the one used in function evaluation. Therefore, fold the sections that you do not want to evaluate and they will be hidden from the evaluator. This gives a way to do case studies with the math.

I finally have funtion definitions working. You define a function and use it in other areas. See the example below.

```markdown
Normal Example Math.imath
	
	z = 9
	
	y = 8
	
	p = 5
	
	x = 1.5
	
	f = x^z + x^y + p
	
	f => 69.072265625

### Header Example Math.imath

(2 * 2)/7 => 0.5714285714285714

4 + 8 => 12

sin(50 deg) => 0.766044443118978

log(5) => 1.6094379124341003

10^log(5) => 40.68533651197375

10^1.61 => 40.73802778041128

a = 1

b = 2

c = 1

result = (b + sqrt(b^2-4*a*c))/2*a

result => 1

g = [ 1, 2, 3]

h = [ 5, 5, 5 ]

g-h=> [-4, -3, -2]

g = [ 1, 2, 3]

h = [ 5, 5, 5 ]

g+h=> [6, 7, 8]

### Function definitions.imath
a = 3

b = 4

c = 5

f(x) = a*x^2 + b*x + c

f(10) => 345
```

Since I am using **FoldingText** to write this page, the examples above are live from the extension. The extension uses the [**Math.js**](http://mathjs.org) JavaScript library for doing all the calculations.

I'm thinking about doing graphs....

##### Other FoldingText Solutions

If you have not checked it out, you should visit the [Alfred Workflow for FoldingText](/#/projects/alfred) that I wrote. It gives many great features that I use everyday: bookmarking, adding notes to tags, site mapping, etc. It is very useful.

I also have most of it translated to a [LaunchBar 6 FoldingText Action](/#/projects/LaunchBar). 

##### FoldingText Tutorials

I have also written an article on writing FoldingText extensions for Computer Tuts+. It is called:

- [**Customizing FoldingText**](http://goo.gl/M8MBWX)

{{> 'donate.html'}}
