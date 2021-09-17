<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	let files;
	let grid;
	let drop;

	function onsheet(json, sheetnames, select_sheet_cb) {
		console.log(json);
		const cdg = canvasDatagrid({
			parentNode:  grid
		});
	
		/* load data */
		cdg.data = json;
	};

	function uploadFile(files) {
		console.log(files[0]);

		DropSheet({
		file: files[0],
		drop,
		on: {
			sheet: onsheet,
		}
		})
	}

$: {
    if (files && files[0]) {
        uploadFile(files);
    }
}
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<section>
	<h1>Upload file...</h1>

	<p>Nothing gets uploaded to a server, all processing is done client side.</p>

	<div>
		<input type="file" id="file" bind:files />
	</div>

	{#if files && files[0]}
		<p>
			{files[0].name}
		</p>
	{/if}

	<div id="drop" bind:this={drop}>Drop a file here</div>
	<div id="grid" bind:this={grid}></div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
