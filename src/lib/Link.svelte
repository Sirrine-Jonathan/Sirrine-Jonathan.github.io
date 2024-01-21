<script>
	import { page } from '$app/stores';
	export let href = '';
</script>

<a class:active={$page.url.pathname === href} {href}><slot /></a>

<style>
	a {
		text-decoration: none;
		color: var(--light);
		transition: color 0.3s;
		border-bottom: 2px solid transparent;
	}

	a.active {
		border-color: var(--accent);
	}

	a:hover {
		color: var(--dark);
		/* text-shadow:
			1px 1px black,
			-1px 1px black,
			-1px -1px black,
			1px -1px black; */
	}
</style>
