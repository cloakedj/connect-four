<script lang="ts">
	import Menu from './Menu.svelte';
	import '$styles/global.css';
	import Nav from './Nav.svelte';
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	import { navigating, page } from '$app/stores';
	import Loading from './Loading.svelte';
	import { afterNavigate } from '$app/navigation';

	const gameState = writable('load');
	setContext('gameState', {
		set: (state: string) => ($gameState = state),
		get: () => $gameState
	});

	afterNavigate(() => {
		$gameState = $page.url.pathname === '/game' ? 'play' : 'load';
	});
</script>

{#if $navigating}
	<Loading />
{/if}

{#if $gameState === 'load' || $gameState === 'pause'}
	<Menu />
{/if}

<main>
	<Nav />
	<slot />
</main>

<style>
	main {
		inline-size: 100%;
		block-size: 100%;
		background: var(--puple, #7945ff);
	}
</style>
