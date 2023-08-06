<script lang="ts">
	export let playerId: number;
</script>

<div class="timer">
	{#if playerId === 1}
		<img
			src="/images/turn-background-red.svg"
			alt="Red background clock showing the time left for player one."
		/>
	{:else}
		<img
			src="/images/turn-background-yellow.svg"
			alt="Yellow background clock showing the time left for player two."
		/>
	{/if}
	<h2
		class="heading--xs"
		style:color={playerId === 1 ? 'var(--white, #fff)' : 'rgb(var(--black, #000))'}
	>
		Player {playerId}'s Turn
	</h2>
	<h3
		class="heading--large"
		style:color={playerId === 1 ? 'var(--white, #fff)' : 'rgb(var(--black, #000))'}
	>
		3s
	</h3>
</div>

<style>
	.timer {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-flow: column;
		grid-column-start: 2;
		z-index: 3;
		margin-block-start: -3%;
	}
	img {
		position: absolute;
	}
	h2,
	h3 {
		position: relative;
	}
	h2 {
		text-transform: uppercase;
	}
	@media only screen and (min-width: 768px) {
		.timer {
			grid-column-start: 2;
			grid-row-start: 3;
		}
	}
</style>
