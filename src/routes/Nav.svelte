<script lang="ts">
	import type { GameState } from '$lib';
	import { getContext } from 'svelte';

	const { set }: GameState = getContext('gameState');
</script>

<nav>
	<button class="board-btn--menu button-pill heading--xs" on:click={() => set('pause')}>
		Menu
	</button>
	<figure>
		<img src="/images/logo.svg" alt="Connect four board game logo consisting of 4 discs" />
	</figure>
	<button class="board-btn--menu button-pill heading--xs"> Restart </button>
</nav>

<style>
	nav {
		padding: 1dvw 3dvw;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 8dvw;
	}
	.button-pill {
		border-radius: 20px;
		background: var(--dark-purple, #5c2dd5);
		color: var(--white, #fff);
		border: none;
		padding: 0.5dvw 1.4dvw;
		text-transform: uppercase;
		cursor: pointer;
		transition: 0.1s all ease-in-out;

		&:hover {
			background: var(--red, #fd6687);
		}
	}
</style>
