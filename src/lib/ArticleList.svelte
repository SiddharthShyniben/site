<script>
	const posts = import.meta.glob('/src/routes/blog/*.svx');
	const list = Object.keys(posts);

	const basename = (path, ext = '.svx') => {
		const name = path.split('/').pop();
		return name.slice(0, name.length - ext.length);
	};
</script>

{#each list as post}
	<div class="post">
		<div class="content">
			{#await posts[post]()}
				<p>loading...</p>
			{:then res}
				<h2>{res.metadata.title}</h2>
				On: {new Date(res.metadata.date).toDateString()}
				<p>Description: {res.metadata.description}</p>
			{/await}
		</div>
	</div>
	<a href="/blog/{basename(post)}">Read on >></a>
{/each}
