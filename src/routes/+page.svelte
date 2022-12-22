<script lang="ts">
  import { onMount } from "svelte"

  let time = 60 * 4

  $: minutes = Math.floor(time / 60)
	onMount(() => {
		setInterval(() => {
			time--
		}, 1000)
	})
</script>

{minutes} : {time - minutes * 60}
<button on:click={() => time = 60 * 4}>Reset</button>