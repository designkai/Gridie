# SimplyGrid
Super lightweight CSS grid

## Using the mixin

By using a mixin .col can be called inside specific elements, making the grid flexible beyond the pre-defined classes. For example, to create a basic layout you might use it inside an id.

	#main-content {
		.col(3,5);
	}
	#side-bar {
		.col(2,5);
	}

	<div class="row">
		<div id="main-content">Main content</div>
		<div id="side-bar">Side bar</div>
	</div>

## Limitations

Currently you cannot place content or styles straight into a row. To do so you'd need to add your largest span inside the row and style that. The only styling acceptable on row is padding.
