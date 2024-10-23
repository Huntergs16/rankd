<script>
	import RankRow from '$lib/RankRow.svelte';
</script>

<div class="w-screen h-screen bg-orange-100">
	<header></header>
	<div class="flex flex-col items-center justify-between">
		<h1 class="text-7xl font-black">Rankd</h1>
		<div>Current Item</div>
		<ul class="w-full px-10 flex flex-col gap-3">
			{#each { length: 10 } as _, i}
				<RankRow id={i} />
			{/each}
		</ul>
	</div>
	<footer>© 2024 Hunter Samoy</footer>
</div>
