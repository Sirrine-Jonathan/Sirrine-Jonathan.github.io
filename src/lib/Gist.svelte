<script lang="ts">
	export let src = '';
	export let title = '';
	src = src.slice(src.length - 3) === '.js' ? src : src + '.js';
	title = title === '' ? src : title;

	import { onMount } from 'svelte';

	let frame: HTMLIFrameElement;
	let height = '30px';

	const barGistHeight = 30;

	onMount(() => {
		frame.srcdoc = `<script src='${src}'><${''}/script>`;
	});

	function getInnerHeight() {
		const body = frame?.contentWindow?.document?.body;
		if (body) {
			height = body.scrollHeight + barGistHeight + 'px';
		}
	}
</script>

<div>
	<div class="gist-title">{title}</div>
	<iframe src="about:blank" bind:this={frame} {title} {height} on:load={getInnerHeight} />
</div>

<style>
	iframe {
		border: 0;
		width: 100%;
	}

	.gist-title {
		padding: 0 20px;
	}
</style>
