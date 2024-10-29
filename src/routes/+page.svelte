<script lang="ts">
	import Ranking from '$lib/Ranking.svelte';

	let isRanked = false;

	function handleIsRanked(event: CustomEvent) {
		// extract and use the data from the event
		isRanked = event.detail.state;
	}
	let list = {
		name: 'Best NBA Players',
		items: [
			{
				id: 1,
				name: 'Kobe Bryant',
				src: 'https://cdn.nba.com/headshots/nba/latest/1040x760/977.png'
			},
			{
				id: 2,
				name: 'LeBron James',
				src: 'https://cdn.nba.com/headshots/nba/latest/1040x760/2544.png'
			},
			{
				id: 3,
				name: 'Tim Duncan',
				src: 'https://cdn.nba.com/headshots/nba/latest/1040x760/1495.png'
			},
			{
				id: 4,
				name: "Shaquille O'Neal",
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/406.png'
			},
			{
				id: 5,
				name: 'Magic Johnson',
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/77142.png'
			},
			{
				id: 6,
				name: 'Kareem Abdul-Jabbar',
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/76003.png'
			},
			{
				id: 7,
				name: 'Bill Russell',
				src: 'https://cdn.nba.com/headshots/nba/latest/1040x760/78049.png'
			},
			{
				id: 8,
				name: 'Wilt Chamberlain',
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/76375.png'
			},
			{
				id: 9,
				name: 'Michael Jordan',
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/893.png'
			},
			{
				id: 10,
				name: 'Larry Bird',
				src: 'https://cdn.nba.com/headshots/nba/latest/260x190/1449.png'
			}
		]
	};
</script>

<div class="w-screen h-screen flex flex-col items-center bg-orange-100 overflow-hidden">
	<div class="w-full max-w-2xl flex flex-col items-center">
		<header class="w-full flex border-b-2 border-b-black mb-6 p-2">
			<h1 class="text-4xl sm:text-6xl font-black">Rankd</h1>
		</header>
		<div class="w-full flex flex-col items-center justify-between">
			<h2 class="text-2xl sm:text-3xl font-black mb-5">{list.name}</h2>
			<Ranking list={list.items} on:isRanked={handleIsRanked} />
			{#if isRanked}
				<button
					class="mt-4 bg-green-500 text-white py-3 px-6 text-lg font-medium rounded-md shadow-[0px_4px_10px_rgba(0,0,0,0.6)] transform transition-all duration-100 ease-in-out active:shadow-[0px_2px_5px_rgba(0,0,0,0.7)] active:translate-y-1"
					>Submit</button
				>
			{/if}
		</div>
		<footer class="mt-4">© 2024 Hunter Samoy</footer>
	</div>
</div>
