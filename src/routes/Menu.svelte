<script lang="ts">
	import type { GameState } from '$lib';
	import { getContext } from 'svelte';
	const { get, set }: GameState = getContext('gameState');
</script>

{#if get() === 'load'}
	<section class="menu-container menu-container--start">
		<form class="menu menu--start" on:submit|preventDefault>
			<figure>
				<img src="/images/logo.svg" alt="Connect four board game logo consisting of 4 discs" />
			</figure>
			<a class="menu-button--play menu-button--action" href="/game">
				<h2 class="heading--medium">Play vs player</h2>
				<figure>
					<img src="/images/player-vs-player.svg" alt="2 smile emojis overlapping each other." />
				</figure>
			</a>
			<button class="menu-button--rules heading--medium"> Game Rules </button>
		</form>
	</section>
{:else if get() === 'pause'}
	<section class="menu-container menu-container--pause">
		<form class="menu menu--pause" on:submit|preventDefault>
			<h1 class="heading--large">PAUSE</h1>
			<button
				class="menu-button--continue menu-button--action heading--medium"
				on:click={() => set('play')}
			>
				Continue Game
			</button>
			<button class="menu-button--restart heading--medium"> Restart </button>
			<a class="menu-button--quit menu-button--action heading--medium" href="/"> Quit Game </a>
		</form>
	</section>
{/if}

<style>
	.menu-container {
		position: fixed;
		inset-block-start: 0;
		inset-inline-start: 0;
		block-size: 100%;
		inline-size: 100%;
		display: grid;
		align-items: center;
		justify-content: center;
		z-index: 10;
	}

	.menu-container--pause {
		background: rgba(var(--block, 0, 0, 0), 0.5);
	}

	.menu-container--start {
		background: var(--dark-purple, #5c2dd5);
	}

	.menu {
		padding: 2dvw 2dvw 4dvw 2dvw;
		min-inline-size: 120%;
		border-radius: 40px;
		border: 3px solid rgb(var(--block, 0, 0, 0));
		background: var(--purple, #7945ff);
		box-shadow: 0px 10px 0px 0px rgb(var(--block, 0, 0, 0));
		display: flex;
		flex-flow: column;
		gap: 2dvw;

		& .menu-button--action:hover,
		& .menu-button--action:focus {
			border: 3px solid var(--dark-purple, #5c2dd5);
			box-shadow: 0px 10px 0px 0px #5c2dd5;
		}
	}

	.menu a {
		text-decoration: none;
		color: unset;
	}

	.menu button,
	.menu a {
		border-radius: 20px;
		border: 3px solid rgb(var(--block, 0, 0, 0));
		box-shadow: 0px 10px 0px 0px rgb(var(--block, 0, 0, 0));
		padding: 1dvw;
		text-transform: uppercase;
		cursor: pointer;
		text-align: center;
	}

	figure {
		margin: 0;
	}

	.menu--start {
		& .menu-button--play {
			background: var(--yellow, #ffce67);
			display: flex;
			justify-content: space-between;
			flex-shrink: 0;
			align-items: center;
			gap: 2dvw;
			transition: all 0.1s ease;
		}

		& > figure {
			padding: 3dvw;
			display: flex;
			align-items: center;
			justify-content: center;
		}

		& .menu-button--play figure img {
			inline-size: 5dvw;
		}

		& .menu-button--rules {
			background: (--white, #fff);
			text-align-last: left;
		}
	}

	.menu--pause {
		min-inline-size: 150%;
		justify-self: center;

		& h1 {
			color: var(--white, #fff);
			text-align: center;
			padding: 2.5dvw;
		}

		& .menu-button--quit {
			background: var(--red, #fd6687);
			color: var(--white, #fff);
		}
	}
</style>
