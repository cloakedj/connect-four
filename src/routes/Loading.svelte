<div class="loader-container">
	<div class="loader" />
</div>

<style>
	.loader-container {
		block-size: 100%;
		inline-size: 100%;
		position: fixed;
		inset-block-start: 0;
		inset-inline-start: 0;
		background: var(--purple, #7945ff);
		display: grid;
		place-items: center;
		z-index: 99999999;
	}

	.loader {
		block-size: 3dvw;
		inline-size: 3dvw;
		border-radius: 50%;
		background: transparent;
		border: 0.4rem solid var(--red, #fd6687);
		border-block-start-color: transparent;
		animation-name: rotate;
		animation-timing-function: ease-in;
		animation-iteration-count: infinite;
		animation-duration: 0.4s;
	}

	@keyframes rotate {
		from {
			transform: rotate(0deg);
		}

		to {
			transform: rotate(360deg);
		}
	}
</style>
