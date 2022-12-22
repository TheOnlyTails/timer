<script lang="ts">
	import { onMount } from "svelte"

	let time = 60 * 4

	let stop = false

	$: minutes = Math.floor(time / 60)
	onMount(() => {
		setInterval(() => {
			if (!stop) time--
		}, 1000)
	})
</script>

<h1>{minutes.toString().padStart(2, "0")}:{(time - minutes * 60).toString().padStart(2, "0")}</h1>

<div class="buttons">
	<button on:click={() => (stop = !stop)}>
		{#if stop}
			Start
		{:else}
			Stop
		{/if}
	</button>
	<button on:click={() => (time = 60 * 4)}>Reset</button>
</div>

<style lang="scss">
	h1 {
		font-size: calc(4 * var(--font-size-fluid-3));
	}

	.buttons {
		display: flex;
		gap: 1rem;

		button {
			inline-size: var(--size-fluid-7);
			aspect-ratio: var(--ratio-golden);
			background-color: var(--yellow-4);
			border-radius: var(--radius-3);
			color: var(--gray-10);
			font-size: var(--font-size-fluid-1);
		}
	}
</style>
