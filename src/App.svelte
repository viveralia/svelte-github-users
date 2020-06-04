<script>
	import { onMount } from 'svelte'

	let users

	onMount(() => {
		getUsers()
	})

	const getUsers = async () => {
		const url = 'https://api.github.com/users'
		const res = await fetch(url)
		const data = await res.json()
		users = data
	}
</script>

<main>
	<h1>Github Users</h1>
	{#if users}
		<ul>
			{#each users as user}
				<li>
					<img src={user.avatar_url} alt={user.login} />
					<p>@{user.login}</p>
				</li>
			{/each}
		</ul>
	{:else}
		<p>Loading users...</p>
	{/if}
</main>

<style>
	ul {
		list-style: none;
		padding: 0;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-gap: 0.5rem;
	}


	img {
		width: 100%;
	}

	@media (min-width: 700px) {
		ul {
			grid-template-columns: repeat(6, 1fr);
		}
	}
</style>