SVG Reference Sheet
=================

> **Note:** Based on video course [Using SVG Sprites](http://webdesign.tutsplus.com/courses/using-svg-sprites) from Tuts+

Defining Symbols
---------------------
In the body of our page, we define SVG symbols individually:
```
<svg style="display:none">
	<symbol id="sym-mygraphic1">
		<path ...>
	</symbol>
	<symbol id="sym-mygraphic2">			
		<path ...>
	</symbol>
</svg>
```

Where `<path ...>` refers to what we copy from Illustrator or SVG code generator.

Using symbols
-----------------
Now we are ready to use our declared symbols.

Let's assume we have a 500x300px svg graph in illustrator and want to show a smaller version of it:
```
<svg class="sym-mygraphic2" height="100" viewbox="0 0 500 300">
	<use xlink:href="#sym-mygraphic1"></use>
</svg>

```
Here `viewbox` says: "dont crop/clip it, show the whole svg without offset (0 0).

> **Note:**
The four values in `viewbox` are ( startX , startY , endX, endY )

The `width` and `height` attributes are optional and define how big / small to display our symbol. In this case we are scaling down our symbol to 200 pixels high and missing width is assumed to be auto.
If we don't specify `width` and `height` attributes, the SVG element takes up the whole space of its container.

Applying CSS
----------------

####Globally:
```
<svg class="sym-mygraphic1" width="200" height="100" viewbox="0 0 400 200">
	<style>
		use { fill: #00f; } /* Make all blue */
	</style>
	<use xlink:href="#sym-mygraphic1"></use>
</svg>
```


####Individually:
```
<svg class="sym-mygraphic1" width="200" height="100" viewbox="0 0 400 200">
	<style>
		use.bluegraphic1 { fill: #00f; }
	</style>
	<use class="bluegraphic1" xlink:href="#sym-mygraphic1"></use>
</svg>
```

Loading Sprites
------------------
Let's say we have a 300x300 sprite containing four squared symbols, each 150x150 pixels max.
```
<img src="images/mysprite.svg#svgView(viewBox(0,0,150,150))" width="50">
```
The code above loads the entire sprite but only displays the symbol in the first quadrant (top left), and we scale the symbol using `width` and / or `height` as needed.

Good thing it loads entire sprite once, so we make only one HTTP request. Next, to load the second symbol (top right) somewhere else in the page:
```
<img src="images/mysprite.svg#svgView(viewBox(150,0,150,150))" width="20">
```

We can also add classes as needed:
```
<img class="someclass" src="images/mysprite.svg#svgView(viewBox(150,150,150,150))" width="100">
