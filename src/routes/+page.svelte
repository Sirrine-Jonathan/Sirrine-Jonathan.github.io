<script>
	import { Project } from '$lib';
	const projects = [
		{
			title: 'Chess Layers',
			src: 'https://chess-layers.vercel.app'
		}
	];
</script>

<h1>Jonathan Sirrine</h1>
<div class="projects-list">
	<h2>Projects</h2>
	{#each projects as project}
		<div class="project">
			<div class="project-preview">
				<Project src={project.src} title={project.title} />
			</div>
			<div class="project-details">
				<div class="project-title">{project.title}</div>
			</div>
		</div>
	{/each}
	<div class="project">
		<div class="project-preview">
			<Project src="https://forest-phaser-game.vercel.app" title="лес" />
		</div>
		<div class="project-details">
			<div class="project-title">лес</div>
		</div>
	</div>
	<div class="project">
		<div class="project-preview">
			<Project src="https://jonathansirrine.com" title="Personal Website" />
		</div>
		<div class="project-details">
			<div class="project-title">Personal Website</div>
		</div>
	</div>
</div>

<style>
	.projects-list {
		display: flex;
		flex-direction: column;
		row-gap: 100px;
		margin-top: 20px;
	}
	.project {
		display: flex;
	}

	.project-preview,
	.project-details {
		flex: 1;
	}
</style>
