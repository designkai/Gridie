# SimplyGrid
Super lightweight LESS grid built with calc(), with fallback to IE7+.

## Using the mixin

By using a mixin .col can be called inside specific elements, making the grid flexible beyond the pre-defined classes. For example, to create a basic layout you might use it inside an ID.

```css
#main-content {
	.col(3,5);
}
#side-bar {
	.col(2,5);
}
```

This allows you to not use column classes in your HTML.

```html
<div class="row">
	<div id="main-content">Main content</div>
	<div id="side-bar">Side bar</div>
</div>
```

This method also allows you to attach grid values directly to elements, without having to create columns. Take the following image list.

```html
<div class="row img-list">
	<img src="cool-image.jpg" style="width:100%;">
	<img src="cool-image.jpg" style="width:100%;">
	<img src="cool-image.jpg" style="width:100%;">
	<img src="cool-image.jpg" style="width:100%;">
	<img src="cool-image.jpg" style="width:100%;">
	<img src="cool-image.jpg" style="width:100%;">
</div>
```

Using the mixin, we could turn these 6 images into 6 columns.

```less
.img-list {
	img {
		.col(1,3);
	}
}
```

The mixin can also be expanded on to define the breakpoints of an element. For example, if we wanted those 6 images to break into 6 rows at 740px we can add it at the end.

```less
.img-list {
	img {
		.col(1,3,740px);
	}
}
```

## Creating a grid stylesheet

If you'd like to create a stylesheet like normal that uses classes, this can be included by changing `@create-classes` to `true`.

This will output the styles for a grid based on the variables at the top of the doc.

```
@columns: 12;
@rowclass: row; // Sets the class used for rows
@colclass: span; // Sets the class used for columns
@small: 510px;
@medium: 600px;
@large: 768px;
```

These classes can then be used as expected. The code below will produce six columns that breaks into three columns, then two columns, and finally one column.

```html
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
<div class="span6-sm span4-md span2-lg">&nbsp;</div>
```

Specifying a column without a class size will make sure that it keeps it's width at any size, unless specified by another class.

```html
<!-- This will always be four columns -->
<div class="span3">&nbsp;</div>
<div class="span3">&nbsp;</div>
<div class="span3">&nbsp;</div>
<div class="span3">&nbsp;</div>

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
