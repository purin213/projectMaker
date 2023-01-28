<script>
// @ts-nocheck

	import Project from './Project.svelte'
	import Comment from './Comment.svelte'
	
	let pid = 1;
	let cid = 1;
	
	let username = "";
	
	let projectList = [
		{id: pid++, done:false, title:"Add TypeScript support", tasksCompleted: 25, totalTasks:57},
	];
	let commentList = [
		{id: cid++, project:1, name:"Ecma Script", postedAt:new Date(), commentText:"Those interface tests are now passing"},
	];
	
	// @ts-ignore
	function addProject(input) {
		const project = {
			id: pid++,
			done: false,
			title: input.value,
			tasksCompleted: 0,
			totalTasks:50
		};

		projectList = [project, ...projectList];
		input.value = '';
	}
	
	// @ts-ignore
	function addComment(input) {
		
	}

	function remove(project) {
		projectList = projectList.filter(t => t !== project);
	}

</script>

<h2>
	Projects for 2023
</h2>

<div style="display:flex; padding: 1rem 1rem; justify-content:start; align-items:start;">
	<p>comment name</p>
	<input bind:value={username} style="width:30%; margin:0 1rem;" placeholder="name"/>
</div>

<div class="board">
	<input placeholder="add a project" on:keydown={e => e.key === 'Enter' && addProject(e.target)}/>
</div>

<ul>
	{#each projectList as project}
	<li>
		<Project
			title={project.title}
			tasksCompleted={project.tasksCompleted}
			totalTasks={project.totalTasks}
		>
			<div slot="comments">
				{#each commentList.filter(item => item.project === project.id) as comment}
				<Comment name={comment.name} postedAt={comment.postedAt}>
					<p>{comment.commentText}</p>
				</Comment>
				{/each}
			</div>
		</Project>
	</li>
	{/each}
</ul>

<style>
	.board {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1em;
		max-width: 36em;
		margin: 0 auto;
	}

	.board > input {
		font-size: 1.4em;
		grid-column: 1/3;
		margin: 1em;
	}
	
	h2 {
		font-weight: 300;
		margin: 0 1rem;
	}

	ul {
		display:flex;
		justify-content:center;
		flex-direction:column;
		list-style: none;
		padding: 0;
		margin: 0.5rem;
		display: flex;
	}

	@media (max-width: 600px) {
		ul {
			flex-direction: column;
		}
	}

	li {
		padding: 0.5rem;
		flex: 1 1 50%;
		min-width: 200px;
	}
</style>