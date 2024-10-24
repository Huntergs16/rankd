<script>
	import List from '$lib/List.svelte';

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

<div class="w-screen h-screen flex flex-col items-center bg-orange-100">
	<header></header>
	<div class="w-full flex flex-col items-center justify-between">
		<h1 class="text-7xl font-black mb-5">Rankd</h1>
		<h2 class="text-3xl font-black mb-5">{list.name}</h2>
		<div class="text-3xl font-black mb-5">Current Item</div>
		<List list={list.items} />
		<button>Submit</button>
	</div>
	<footer>© 2024 Hunter Samoy</footer>
</div>
