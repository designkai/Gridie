# SimplyGrid
Super lightweight LESS grid built with calc(), with fallback to IE7+.

## Using the mixin

By using a mixin .col can be called inside specific elements, making the grid flexible beyond the pre-defined classes. For example, to create a basic layout you might use it inside an id.

	#main-content {
		.col(3,5);
	}
	#side-bar {
		.col(2,5);
	}

This allows you to not use column classes in your HTML.

	<div class="row">
		<div id="main-content">Main content</div>
		<div id="side-bar">Side bar</div>
	</div>

This method also allows you to attach grid values directly to elements, without having to create columns. Take the following image list.

	<div class="row img-list">
		<img src="cool-image.jpg" style="width:100%;">
		<img src="cool-image.jpg" style="width:100%;">
		<img src="cool-image.jpg" style="width:100%;">
		<img src="cool-image.jpg" style="width:100%;">
		<img src="cool-image.jpg" style="width:100%;">
		<img src="cool-image.jpg" style="width:100%;">
	</div>

Using the mixin, we could turn these 6 images into 6 columns that break down to 3 columns using a media query.

	.img-list {
		img {
			.col(1,3);
			@media (min-width: 600px) {
				.col(1,6);
			}
		}
	}

## Limitations

* Currently you cannot place content or styles straight into a row. To do so you'd need to add your largest span inside the row. The only styling acceptable on row is padding.
* Using @gutters for .row margin-bottom means that mordern units (such as vw) won't work. Instead, an extra line can be added to .row setting the margin-bottom to 2% using the \9 hack.
