<script lang="ts">
	import { onMount } from "svelte"

	let time = 60 * 4

	let stop = true

	const colors = [
		{
			name: "Red",
			color: "--red-8",
			textColor: "",
		},
		{
			name: "Blue",
			color: "--blue-7",
			textColor: "",
		},
	] as const

	let currentColorIndex = 0
	$: currentColor = colors[currentColorIndex]

	$: minutes = Math.floor(time / 60)
	onMount(() => {
		setInterval(() => {
			if (!stop) time--
		}, 1000)
	})
</script>

<main style:background="var({currentColor.color})">
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
	<div class="buttons">
		{#each colors as color, i}
			<input
				type="radio"
				bind:group={currentColorIndex}
				value={i}
				class="color-input"
				style:background="var({color.color})"
				aria-label={color.name}
			/>
		{/each}
	</div>
</main>

<style lang="scss">
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 1rem;
		block-size: 100vh;
		block-size: 100dvh;
	}

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

	.color-input {
		appearance: none;
		outline: var(--border-size-2) solid var(--gray-1);
		border-radius: var(--radius-round);
		inline-size: var(--size-fluid-2);
		aspect-ratio: var(--ratio-square);
		padding: var(--size-fluid-1);
	}
</style>
