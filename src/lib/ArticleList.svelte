<script>
	const posts = import.meta.glob('/src/routes/blog/*.svx');
	const list = Object.keys(posts);

	const basename = (path, ext = '.svx') => {
		const name = path.split('/').pop();
		return name.slice(0, name.length - ext.length);
	};

	const formatDate = date => date.toLocaleDateString(undefined, {
		month: 'short',
		year: 'numeric',
		day: 'numeric',
	});

	const getPost = key => posts[key]();

	const topPost = list.shift();
	const thenPosts = list;
</script>

<div class='container'>
	<!-- Top post -->
	{#if topPost}
		{#await getPost(topPost)}
			<div class='top-spinner'>
				<div class='dots'></div>
			</div>
		{:then post}
			<div class='top-post'>
				<img src='{post.metadata.cover}'>
				<h2>{post.metadata.title}</h2>
				<p class='desc'>
					<strong class='tldr'>TLDR </strong> {post.metadata.description}
				</p>
				<p class='meta'>
					<strong>Siddharth Shyniben</strong> on <span class='light'>{formatDate(new Date(post.metadata.date))}</span>
				</p>
			</div>
		{/await}
	{/if}
	
	<div class='post-grid'>
		{#each thenPosts as post}
			{#await getPost(topPost)}
				<div class='top-spinner'>
					<div class='dots'></div>
				</div>
			{:then post}
				<div class='post'>
					<img src='{post.metadata.cover}'>
					<h2>{post.metadata.title}</h2>
					<p class='meta'>
						<strong>Siddharth Shyniben</strong> on <span class='light'>{formatDate(new Date(post.metadata.date))}</span>
					</p>
				</div>
			{/await}
		{/each}
	</div>
</div>

<style>
.container {
	width: 70vw;
	max-width: min(1200px, 70vw);
	margin: 0 auto;
}

.top-post {
	margin: 2em auto;
	height: 100%;
	max-width: min(1200px, 70vw);
	margin-bottom: 10em;
}

.top-spinner {
	margin: 2em auto;
	height: 60vh;
	max-width: min(1200px, 70vw);
}

.top-post img {
	width: 100%;
	object-fit: cover;
}

.top-post h2 {
	font-size: 2em;
	margin: 0.5em 0;
}

.tldr {
	color: #2563eb;
	font-weight: 700;
	font-family: 'Jost', sans-serif;
}

.top-post .desc {
	color: #66666E;
	font-family: 'Nunito', sans-serif;
}

.light {
	color: #66666E;
}

.dots {
	width: 50px;
	height: 24px;
	color: #2563eb;
	background: 
		radial-gradient(circle closest-side, currentColor 90%, #0000) 0% 50%,
		radial-gradient(circle closest-side, currentColor 90%, #0000) 50% 50%,
		radial-gradient(circle closest-side, currentColor 90%, #0000) 100% 50%;
	background-size: calc(100%/3) 12px;
	background-repeat: no-repeat;
	animation: dots 1s infinite linear;
}

@keyframes dots {
	20% {
		background-position: 0% 0%, 50% 50%, 100% 50%
	}

    40% {
		background-position: 0% 100%, 50% 0%, 100% 50%
	}
    
	60% {
		background-position: 0% 50%, 50% 100%, 100% 0%
	}

    80% {
		background-position: 0% 50%, 50% 50%, 100% 100%
	}
}

.post-grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
	grid-gap: 1em;
	margin: 2em auto;
	height: 100%;
	max-width: min(1200px, 70vw);
	padding-bottom: 2em;
	justify-content: center;
}

@media screen and (max-width: 500px) {
	.post-grid {
		grid-template-columns: repeat(auto-fill, 300px);
	}
}

@media screen and (max-width: 400px) {
	.post-grid {
		grid-template-columns: repeat(auto-fill, 200px);
	}
}

.post img {
	width: 100%;
	object-fit: cover;
}

/* ugh */
:global(body) {
	overflow-x: hidden;
}
</style>
