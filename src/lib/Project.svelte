<script>
	import { onMount } from 'svelte';
	import clsx from 'clsx';
	export let src = '';
	export let isMobile = false;
	export let title = '';
	title = title === '' ? src : title;
	const uniqueId = title.split(' ').join('').toLowerCase();

	$: deviceWidth = 0;
	$: deviceHeight = 0;
	$: cssVars = `--preview-scale: scale(1)`;

	// Update the scale factor initially and whenever the window is resized
	onMount(() => {
		updateScaleFactor();

		window.addEventListener('resize', updateScaleFactor);
	});

	// Function to dynamically set the scale factor
	function updateScaleFactor() {
		// Get the window dimensions
		deviceWidth = window.innerWidth;
		deviceHeight = window.innerHeight;

		// Get the device image dimensions
		const image = document.querySelector(`#${uniqueId}`);
		const imageWidth = image?.clientWidth;
		const imageHeight = image?.clientHeight;

		if (imageWidth && imageHeight) {
			// Get the preview windows dimensions
			const previewRatio = 0.65;
			const previewWidth = imageWidth * 0.76;
			const previewHeight = previewWidth * previewRatio;

			// adjust device width to match preview width aspect ratio
			deviceHeight = deviceWidth * previewRatio;

			// Adjust the scale factor based on your criteria
			const scaleFactor = Math.min(previewHeight / previewHeight, previewWidth / deviceWidth);
			cssVars = `--project-scale: scale(${scaleFactor});`;
		}
	}
</script>

<div class={clsx('project', isMobile && 'mobile')} style={cssVars}>
	<div class="project-display">
		{#if isMobile}
			<img id={uniqueId} class="device-image phone" src="" alt="" />
		{:else}
			<img id={uniqueId} class="device-image macbook" src="/macbook.png" alt="" />
		{/if}
		<iframe class="project-iframe" {title} {src} width={deviceWidth} height={deviceHeight}>
		</iframe>
	</div>
</div>

<style>
	.project-display {
		position: relative;
		width: 100%;
		flex: 1;
	}

	.project-details {
		flex: 1;
	}

	img.device-image {
		width: 100%;
	}

	.project-iframe {
		position: absolute;
		top: 5%;
		left: 12%;
		border: none;
		transform-origin: 0 0;
		transform: var(--project-scale);
	}

	.project-title {
		padding: 0 20px;
	}
</style>
