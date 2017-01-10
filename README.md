# Gridie
Super lightweight grid built with calc(), with fallback to IE7+. The examples below are written in LESS, but there is also an SCSS file with the same methods.

## Using the mixin

Gridie has been designed in a way that removes the need for a whole bloated grid system, instead allowing you to build grid features into classes as they need them.

Using `.col(x,y,breakpoint);` allows you to define grid widths inside specific elements, making the grid flexible beyond the pre-defined classes. For example, to create a basic layout you might simply add grid functionality to IDs.

```html
<div class="row">
	<div id="main-content">Main content</div>
	<div id="side-bar">Side bar</div>
</div>
```

```less
#main-content {
	// This calculates to 3/5 = 60%
	.col(3,5);
}
#side-bar {
	// This calculates to 2/5 = 40%
	.col(2,5);
}
```

This method also allows you to attach grid values directly to elements, without having to create columns. Take the following image list.

```html
<div class="row img-list">
	<img src="image.jpg">
	<img src="image.jpg">
	<img src="image.jpg">
	<img src="image.jpg">
	<img src="image.jpg">
	<img src="image.jpg">
</div>
```

Using the mixin, we could turn these 6 images into 6 columns.

```less
.img-list {
	img {
		width: 100%;
		.col(1,6);
	}
}
```

### Mixin breakpoints

The mixin can also be used to define the breakpoints of an element. For example, we could make those 6 columns break into 3 columns at 740px, then 2 columns at 520px.

```less
.img-list {
	img {
		.col(3,6,520px);
		.col(1,6,740px);
	}
}
```

## Creating a grid stylesheet

Gridie can also be used to create a regular grid syste, defined with classes of your choosing.

To add or remove the grid stylesheet functionality, redifine `@create-classes` as `true` or `false`. This can be done after import into another less file.

At the top of the Gridie code are some basic setting.

```less
// Grid settings
@create-classes:    true; // Change to true to build grid
@grid-gutters:      2vmax; // Sets the space between rows and columns
@grid-columns:      12; // Sets the number of columns
@grid-rowclass:     row; // Sets the class name used for rows
@grid-colclass:     col; // Sets the class name used for columns
```

These allow you to define your gutter width and column count, as well as rename your row and column classes. This is useful, particularly in systems where the class name may conflict with other grids.

Beneath the settings is an array of breakpoints, and their names.

```less
// Create a column sepparated array of all your breakpoints
// in the format of 'name [width]px'
@breakpoints:
	sm 568px,
	md 768px,
	lg 1024px,
	xl 1280px;
```

There is no limit to how many or few breakpoints can be defined in this array. These breakpoints will all then be compiled into the grid as useable classes.

The format of the classes is defines as `.[grid-colclass][number]-[breakpoint]` The code below will produce six columns that breaks into three columns, then two columns, and finally one column, based on the array above.

```html
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
<div class="col12 col6-sm col4-md col2-lg">&nbsp;</div>
```

Specifying a column without a class size will make sure that it keeps it's width at any size, unless specified by another class.

```html
<!-- This will always be four columns -->
<div class="col3">&nbsp;</div>
<div class="col3">&nbsp;</div>
<div class="col3">&nbsp;</div>
<div class="col3">&nbsp;</div>

<!-- This will be two columns on desktop, and four columns anytime below -->
<div class="span3 span6-lg">&nbsp;</div>
<div class="span3 span6-lg">&nbsp;</div>
<div class="span3 span6-lg">&nbsp;</div>
<div class="span3 span6-lg">&nbsp;</div>
```

## Limitations

* Currently you cannot place content or styles straight into a row. To do so you'd need to add your largest span inside the row. The only styling acceptable on row is padding.
* Rows directly inside rows will also cause issues.
* Using @gutters for .row margin-bottom means that mordern units (such as vw) won't work. Instead, an extra line can be added to .row setting the margin-bottom to 2% using the \9 hack.
