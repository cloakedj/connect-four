<script lang="ts">
	export let playerId: number;
</script>

<div class="scorecard" data-player-id={playerId}>
	<figure class="player-icon">
		{#if playerId === 1}
			<img src="/images/player-one.svg" alt="Red colored smiling emoji representing player one." />
		{:else}
			<img
				src="/images/player-two.svg"
				alt="Yellow colored smiling emoji representing player two."
			/>
		{/if}
	</figure>
	<h2 class="heading--small">Player {playerId}</h2>
	<h3 class="heading--large">12</h3>
</div>

<style>
	.scorecard {
		border-radius: 20px;
		border: 3px solid var(--black, #000);
		background: var(--white, #fff);
		box-shadow: 0px 10px 0px 0px #000;
		flex-shrink: 0;
		position: relative;
		padding: 3dvw 2dvw 2dvw 2dvw;
		inline-size: fit-content;
		display: flex;
		gap: 0.3dvw;
		flex-flow: column;
		align-items: center;
		align-self: center;
		justify-self: var(--justify-position, 'center');
	}
	.player-icon {
		position: absolute;
		inset-block-start: 0;
		transform: translateY(-75%);
	}
	h2 {
		text-transform: uppercase;
	}

	@media only screen and (min-width: 768px) {
		.scorecard {
			grid-column-start: 2;
			grid-row-start: 1;
			inline-size: 40%;
			margin-block-end: 2dvw;
			margin-inline-start: 6%;
			margin-inline-end: 6%;
			flex-flow: row;
			justify-content: center;
			padding: 1dvw 2dvw 1dvw 2dvw;
			gap: 2dvw;
		}
		[data-player-id='1'] {
			--justify-position: flex-start;
		}
		[data-player-id='2'] {
			--justify-position: flex-end;
			flex-flow: row-reverse;
		}
		[data-player-id='1'] .player-icon {
			inset-inline-start: 0;
			transform: translate(-125%, 6%);
		}
		[data-player-id='2'] .player-icon {
			inset-inline-end: 0;
			transform: translate(125%, 6%);
		}
	}
</style>
