<script lang="ts">
	import Board from './Board.svelte';
	import Menu from './Menu.svelte';
	import '$styles/global.css';
	import Nav from './Nav.svelte';
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';

	const gameState = writable('start');
	setContext('gameState', {
		set: (state: string) => ($gameState = state),
		get: () => $gameState
	});
</script>

<main>
	<slot />
	<Nav />
	{#if $gameState === 'start' || $gameState === 'pause'}
		<Menu />
	{/if}
	<Board />
</main>

<style>
	main {
		inline-size: 100%;
		block-size: 100%;
		background: var(--puple, #7945ff);
	}
</style>
