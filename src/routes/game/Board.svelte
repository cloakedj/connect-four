<script lang="ts">
	import { scale } from 'svelte/transition';
	import Score from './Score.svelte';
	import Timer from './Timer.svelte';
	import { quintInOut } from 'svelte/easing';

	const setActiveColumn = (column: number) => {
		document.documentElement.style.setProperty('--active-column', `${column}`);
	};
</script>

<section class="board" transition:scale={{ start: 0.7, easing: quintInOut }}>
	<div class="game-container">
		<Score playerId={1} --justify-position="flex-end" />
		<div class="game-boards">
			<figure class="game-board game-board--white">
				<img src="/images/board-layer-white-large.svg" alt="White board for the connect 4 game" />
			</figure>
			<div class="hidden-board">
				{#each new Array(6) as index}
					{#each Array.from({ length: 7 }, (_, i) => i) as column}
						<button class="ring {column}" on:mouseenter={(e) => setActiveColumn(column)} />
					{/each}
				{/each}
			</div>
			<figure class="game-board game-board--black">
				<img src="/images/board-layer-black-large.svg" alt="White board for the connect 4 game" />
			</figure>
		</div>
		<Score playerId={2} --justify-position="flex-start" />
		<Timer playerId={1} />
	</div>
	<div class="board-base" aria-hidden="true" />
</section>

<style>
	figure {
		margin: 0;
	}
	.board {
		block-size: 100%;
		inline-size: 100%;
		position: relative;
	}
	.board-base {
		border-radius: 60px 60px 0px 0px;
		background: var(--dark-purple, #5c2dd5);
		inline-size: 100%;
		flex-shrink: 0;
		min-block-size: 27%;
		position: absolute;
		inset-block-end: 0;
	}
	.game-boards {
		position: relative;
		block-size: 100%;
		z-index: 1;
	}
	.game-container {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		justify-items: center;
		column-gap: 2dvw;
	}
	.game-board--white {
		position: relative;
		z-index: 2;
		pointer-events: none;
	}
	.game-board--black {
		position: absolute;
		inset-block-start: 0;
	}
	.hidden-board {
		block-size: 100%;
		inline-size: 100%;
		position: absolute;
		inset-block-start: 0;
		inset-inline-start: 0;
		border-radius: 40px;
		z-index: 1;
		display: inline-flex;
		flex-wrap: wrap;
		column-gap: var(--board-ring-column-gap, 24px);
		row-gap: var(--board-ring-row-gap, 20px);
		padding-block-start: var(--board-padding-uniform, 20px);
		padding-inline-start: var(--board-padding-uniform, 20px);
		padding-inline-end: var(--board-padding-uniform, 20px);
		padding-block-end: var(--board-padding-bottom, 60px);
		--turn-player-indicator: url('/images/marker-red.svg');

		&::before {
			content: '';
			visibility: hidden;
			background: var(--turn-player-indicator);
			background-repeat: no-repeat;
			background-size: contain;
			position: absolute;
			block-size: var(--player-indicator-height, 26px);
			inline-size: var(--player-indicator-width, 32px);
			position: absolute;
			inset-block-start: -5%;
			inset-inline-start: calc(
				var(--board-padding-uniform, 20px) + (var(--board-ring-size, 32px) / 2) +
					(
						var(--active-column) *
							(var(--board-ring-size, 64px) + var(--board-ring-row-gap, 24px) + 4px)
					)
			);
			transform: translateX(-50%);
			transition: 0.13s all ease;
		}

		& .ring {
			all: unset;
			block-size: var(--board-ring-size, 64px);
			inline-size: var(--board-ring-size, 64px);
			border-radius: 50%;
			cursor: pointer;

			&:hover {
				background: rgb(255, 255, 255, 0.2);
			}
		}
	}

	.hidden-board:has(.ring:hover)::before {
		visibility: visible;
	}
	@media only screen and (min-width: 768px) {
		.game-boards {
			grid-row-start: 2;
			grid-column-start: 2;
		}
	}
</style>
