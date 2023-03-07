<script>
	import Header from '../lib/components/Header.svelte';
	import { gsap } from 'gsap';
</script>

<svelte:window
	on:mousemove={(e) => {
		gsap.to('.customCursor', {
			x: e.clientX - 50,
			y: e.clientY - 50,
			ease: 'power1.out',
			duration: 0.5
		});
	}}
/>

<div class="h-[100vh] flex flex-col">
	<Header />
	<main
		class="flex justify-center px-[250px] flex-col grow"
		on:mouseenter={() => {
			gsap.to('.customCursor', {
				scale: 5
			});
		}}
		on:mouseleave={() => {
			gsap.to('.customCursor', {
				scale: 1
			});
		}}
	>
		<p>We make it happen</p>
		<h1>
			<span>Websites</span> <span>Apps</span> <span>Branding</span>
		</h1>
	</main>

	<div class="h-8 w-8 rounded-full bg-black absolute customCursor -z-20" />
</div>

<style>
	h1 {
		@apply text-[5.8vw] font-bold;
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
