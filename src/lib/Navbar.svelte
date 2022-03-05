<nav>
	<div class='brand'>
		<img src='/logo.png' alt='logo' class='brand-logo'/>
		<span>blog</span>
	</div>
	<div>
		<svg xmlns="http://www.w3.org/2000/svg" class="search" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
			<path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
		</svg>
	</div>
</nav>

<style>
nav {
	border-bottom: 3px solid rgba(102, 102, 110, 0.38);
	width: 100%;
	height: 90px;

	display: flex;
	justify-content: space-around;
	align-items: center;
}

.brand {
	display: flex;

	font-size: 50px;
}

.brand-logo {
	height: 70px;
}

.search {
	height: 20px;
}
</style>
