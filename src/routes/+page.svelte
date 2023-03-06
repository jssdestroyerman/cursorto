<script>
	import Header from '../lib/components/Header.svelte';
	import { spring } from 'svelte/motion';

	let coords = spring(
		{ x: 50, y: 50 },
		{
			stiffness: 0.05,
			damping: 0.5
		}
	);
</script>

<div
	class="h-[100vh] flex flex-col"
	on:mousemove={(e) => coords.set({ x: e.clientX - 20, y: e.clientY - 20 })}
>
	<Header />
	<main class="flex justify-center px-[250px] flex-col grow">
		<p>We make it happen</p>
		<h1><span>Websites</span> <span>Apps</span> <span>Branding</span></h1>
	</main>

	<div
		class="h-5 w-5 rounded-full bg-black absolute"
		style={`transform: translate(${$coords.x}px, ${$coords.y}px);
		`}
	/>
</div>

<style>
	h1 {
		@apply text-[110px] font-bold;
		-webkit-text-fill-color: transparent;
		-webkit-text-stroke: 1px;
	}
	span {
		@apply transition-all duration-300;
	}
	span:hover {
		@apply cursor-pointer;
		-webkit-text-fill-color: black;
	}
</style>
