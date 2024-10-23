<script>
	export let id;
	$: dispid = id + 1;
	export let value = '';
	export let src = '';
</script>

<li
	class="flex items-center w-full rounded-md border-2 border-solid border-black h-14 duration-100 ease-in hover:h-16 cursor-pointer"
>
	<div class="w-6 text-xl text-right">{dispid}:</div>
	<div>{value}</div>
	<img {src} alt={value} />
</li>
