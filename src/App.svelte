<script>
	export let name;

	let m = { x: 0, y: 0 };
	let mouseIsDown = false;
	let blockGrid = [];
	let width = 100;
	let height = 100;
	let blockWidth = window.innerWidth / width;
	let blockHeight = window.innerHeight / height;

	// Reset the Block grid
	const resetBlockGrid = () => {
		for ( let x = 0; x < height; x++ ) {
			blockGrid[ x ] = [];
			for ( let y = 0; y < width; y++ ) {
				blockGrid[ x ][ y ] = '.';
			}
		}
	}
	resetBlockGrid();

	function handleMousemove(event) {
		if ( ! mouseIsDown ) {
			return;
		}
		m.x = event.clientX;
		m.y = event.clientY;
		let blockY = Math.floor( m.x / blockWidth );
		let blockX = Math.floor( m.y / blockHeight );
		console.log( blockX, blockY );
		blockGrid[ blockX ] = blockGrid[ blockX ] || [];
		blockGrid[ blockX ][ blockY ] = 'X';
	}

	function handleMouseDown() {
		console.log( 'handleMouseDown' );
		mouseIsDown = true;
	}

	function handleMouseUp() {
		console.log( 'handleMouseUp' );
		mouseIsDown = false;
	}


	function styles(props) { getStyles(props); }


	const getStyles = () => (
	`		background-color: #eee;
			width: ${ Math.floor( window.innerWidth / document.getElementsByClass('blockgrid').clientWidth ) }px;
			height: ${ Math.floor( window.innerHeight /  document.getElementsByClass('blockgrid').clientHeight ) }px;
	`
	);
</script>
<style>
	div {
		width: 100%;
		height:100%;
	}
	td {
		list-style-type: none;
		font-family: "Lucida Console", Monaco, monospace;
	}
	::selection {
		background-color: transparent;
	}
</style>

<div
	on:mousemove={ handleMousemove }
	on:mousedown={ handleMouseDown }
	on:mouseup={ handleMouseUp }
	class="blockgrid"
>
	<table >
	{ #each blockGrid as gridrow }
		<tr >
			{ #each gridrow as item }
				<td style={getStyles()}>
					{ item }
				</td>
			{ /each }

 		</tr>
	{ /each }
	</table>
<button on:click={ resetBlockGrid }>
	Clear
</button>

</div>