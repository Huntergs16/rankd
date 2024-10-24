<script lang="ts">
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';
	import { writable } from 'svelte/store';
	import type { Writable } from 'svelte/store';

	type RankItem = {
		id: number;
		name: string;
		src: string;
	};

	export let list: RankItem[] = [];

	const flipDurationMs = 150;

	// Create a writable store for the list
	let listStore: Writable<RankItem[]> = writable(list);

	// Update the writable store whenever the items prop changes
	$: listStore.set(list);

	// Handle the reordering logic
	function handleDndConsider(e: CustomEvent) {
		if (e.detail.items) {
			listStore.set(e.detail.items);
		}
	}

	// Handle the reordering logic
	function handleDndFinalize(e: CustomEvent) {
		if (e.detail.items) {
			listStore.set(e.detail.items);
		}
	}
</script>

<ul
	use:dndzone={{ items: $listStore, flipDurationMs }}
	on:consider={handleDndConsider}
	on:finalize={handleDndFinalize}
	class="w-full px-10 flex flex-col items-center gap-3 list-none"
>
	{#each $listStore as item, i (item.id)}
		<li
			animate:flip={{ duration: flipDurationMs }}
			class="flex items-center w-full max-w-2xl rounded-md border-2 border-solid border-black h-14 md:h-20 cursor-grab px-4 select-none"
		>
			<div class="w-6 text-xl font-bold text-right">{i + 1}:</div>
			<div class="overflow-hidden w-18 h-18 md:w-18 md:h-18 p-[4px]">
				<img class="rounded-xl" src={item.src} alt={item.name} width="100" height="100" />
			</div>
			<div class="text-xl font-bold">{item.name}</div>
		</li>
	{/each}
</ul>
