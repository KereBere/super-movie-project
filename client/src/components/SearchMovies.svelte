<script>
	import { goto } from '$app/navigation';
	import {fly} from 'svelte/transition';
	let inputValue = '';
	let active = false;

	const cancelInactive = () => (inputValue ? (active = true) : (active = false));
	const submitSearch = () => goto('/search/' + inputValue);
</script>

<form on:submit|preventDefault={submitSearch} action="POST" class="search">
	{#if !active}
		<label in:fly={{ y: -10, duration: 500 }} out:fly={{ y: -10, duration: 500 }} for="search_movie"
			>Search Movie</label
		>
	{/if}
	<input
		on:blur={cancelInactive}
		on:focus={() => (active = true)}
		name="search_movie"
		type="text"
		bind:value={inputValue}
		class={active ? 'selecte' : ''}
	/>
	{#if inputValue}
		<button in:fly={{ x: 20, duration: 500 }} out:fly={{ x: 0, duration: 500 }}>Search</button>
	{/if}
</form>

<style>
	.search {
		position: relative;
		width: 30%;
		margin: 1rem;
	}
	button {
		font-size: 0.7rem;
		padding: 0rem 1rem;
		background-color: rgb(96, 110, 201);
		color: white;
		font-weight: bold;
		position: absolute;
		bottom: 50%;
		right: 0;
		transform: translate(0, 50%);
		height: 100%;
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
		cursor: pointer;
	}
	input {
		width: 100%;
		border: none;
		font-size: 1rem;
		font-family: 'Poppins' sans-serif;
		outline: none;
		color: rgb(255, 255, 255);
		padding: 0.5rem, 0.1rem;
		transition: background 0.75s ease-out;
		font-weight: bold;
		background: rgb(63, 63, 63);
		border-radius: 10px;
		padding: 1rem;
	}
	label {
		position: absolute;
		font-size: 0.8rem;
		top: 50%;
		left: 0;
		transform: translate(0, -50%);
		color: #fff;
		padding: 0rem 1rem;
		background: none;
	}
	.input.selected {
		background: rgb(50, 50, 50);
	}
</style>
