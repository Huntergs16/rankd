<script lang="ts">
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';
	import { writable } from 'svelte/store';
	import type { Writable } from 'svelte/store';
	import { createEventDispatcher } from 'svelte';

	// create the dispatcher
	const dispatch = createEventDispatcher();

	function sendIsRanked() {
		dispatch('isRanked', { state: true });
	}

	type RankItem = {
		id: number;
		name: string;
		src: string;
	};

	export let list: RankItem[] = [];

	let rankedList: RankItem[] = Array.from({ length: 10 }, (_, index) => ({
		id: index + 1,
		name: '',
		src: ''
	}));

	const flipDurationMs = 0;

	// Create a writable store for the list
	let listStore: Writable<RankItem[]> = writable(list);
	let rankedListStore: Writable<RankItem[]> = writable(rankedList);

	// Update the writable store whenever the items prop changes
	$: listStore.set(list);
	$: rankedListStore.set(rankedList);

	// Handle the reordering logic
	function handleDnDConsider(e: CustomEvent) {
		listStore.set(e.detail.items);
	}
	// Handle the reordering logic
	function handleDndFinalize(e: CustomEvent) {
		if (e.detail.items[e.detail.items.length - 1] != list[list.length - 1]) {
			list = list.slice(0, list.length - 1);
		}
		listStore.set(list);
		if (list.length == 0) sendIsRanked();
	}
	// Handle the reordering logic
	function handleRankedDndConsider(e: CustomEvent) {
		if (e.detail.items) {
			rankedListStore.set(e.detail.items);
		}
	}

	// Handle the reordering logic
	function handleRankedDndFinalize(e: CustomEvent) {
		if (e.detail.items) {
			rankedListStore.set(e.detail.items);
		}
	}
</script>

<div class=" w-9/12 flex flex-col items-center">
	{#if list.length}
		<h2 class="select-none">&#9432; Drag item to place in ranking</h2>
		<ul
			use:dndzone={{ items: $listStore, flipDurationMs, dropFromOthersDisabled: true }}
			on:consider={handleDnDConsider}
			on:finalize={handleDndFinalize}
			class="w-full flex flex-col items-center gap-3 list-none mb-8 border-b-[.2rem] border-dashed border-black pb-8"
		>
			{#each $listStore as item, i (item.id)}
				<li
					animate:flip={{ duration: flipDurationMs }}
					class="flex items-center justify-center w-full rounded-md border-2 border-solid border-black h-10 sm:h-14 cursor-grab select-none {i ==
					$listStore.length - 1
						? ''
						: 'hidden'}"
				>
					{#if item.src}
						<div class="hidden sm:block overflow-hidden aspect-square h-full p-[2px]">
							<img class="object-cover h-full w-full" src={item.src} alt={item.name} />
						</div>
					{/if}
					<div class="text-xl font-bold">{item.name}</div>
				</li>
			{/each}
		</ul>
	{/if}

	<ul
		use:dndzone={{ items: $rankedListStore, flipDurationMs }}
		on:consider={handleRankedDndConsider}
		on:finalize={handleRankedDndFinalize}
		class="w-full flex flex-col items-center gap-3 list-none"
	>
		{#each $rankedListStore as item, i (item.id)}
			<li
				animate:flip={{ duration: flipDurationMs }}
				class="flex items-center w-full rounded-md border-2 border-solid border-black h-10 sm:h-14 cursor-grab select-none"
			>
				<div class="w-10 text-xl font-bold text-right mr-6 sm:mr-0">{i + 1}:</div>
				{#if item.src}
					<div class="hidden sm:block overflow-hidden aspect-square h-full p-[2px]">
						<img class="object-cover h-full w-full" src={item.src} alt={item.name} />
					</div>
				{/if}
				<div class="text-xl font-bold">{item.name}</div>
			</li>
		{/each}
	</ul>
</div>
