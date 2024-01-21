<script lang="ts">
	import { NavLink } from '$lib';
	import { onNavigate } from '$app/navigation';

	onNavigate((navigation) => {
		if ('startViewTransition' in document && !document.startViewTransition) return;

		return new Promise((resolve) => {
			if ('startViewTransition' in document && typeof document.startViewTransition === 'function') {
				document.startViewTransition(async () => {
					resolve();
					await navigation.complete;
				});
			}
		});
	});
</script>

<header>
	<nav>
		<NavLink href="/">Home</NavLink>
		<NavLink href="/snippets">Snippets</NavLink>
	</nav>
</header>
<main>
	<slot />
</main>

<style>
	header {
		background: var(--primary);
		color: var(--dark);
		padding: 10px 20px;
	}

	main {
		padding: 10px 20px;
	}

	nav {
		display: flex;
		column-gap: 20px;
	}
</style>
