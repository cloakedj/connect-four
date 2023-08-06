<script lang="ts">
	import { afterNavigate } from '$app/navigation';
	import Board from './Board.svelte';
	import type { GameState } from '$lib';
	import { getContext } from 'svelte';
	const { set }: GameState = getContext('gameState');

	afterNavigate(() => {
		set('play');
	});
</script>

<Board />
