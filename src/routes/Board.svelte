<script>
	import Score from './Score.svelte';
	import Timer from './Timer.svelte';
</script>

<section class="board">
	<div class="game-container">
		<Score playerId={1} --justify-position="flex-end" />
		<div class="game-boards">
			<figure class="game-board--white">
				<img src="/images/board-layer-white-large.svg" alt="White board for the connect 4 game" />
			</figure>
			<div class="hidden-board">
				{#each new Array(42) as index}
					<div class="ring" />
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
	}
	@media only screen and (min-width: 768px) {
		.game-boards {
			grid-row-start: 2;
			grid-column-start: 2;
		}
	}
</style>
