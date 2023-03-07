<script>
	import Header from '../lib/components/Header.svelte';
	import { gsap } from 'gsap';
	import { onMount } from 'svelte';

	onMount(() => {
		window.addEventListener('mousemove', (e) => {
			gsap.to('.customCursor', {
				x: e.clientX - 50,
				y: e.clientY - 50,
				ease: 'power1.out',
				duration: 0.5
			});
		});

		const customMain = document.querySelector('.customMain');
		customMain?.addEventListener('mouseenter', (e) => {
			console.log(e);
			gsap.to('.customCursor', {
				scale: 8
			});
		});
		customMain?.addEventListener('mouseleave', () => {
			gsap.to('.customCursor', {
				scale: 1
			});
		});

		const customSpan = document.querySelector('.customSpan');
		customSpan?.addEventListener('mouseenter', () => {
			gsap.to('.customCursor', {
				scale: 12
			});
		});
		customSpan?.addEventListener('mouseleave', () => {
			gsap.to('.customCursor', {
				scale: 8
			});
		});
	});
</script>

<div class="h-[100vh] flex flex-col">
	<Header />
	<main class="flex justify-center px-[250px] flex-col grow customMain">
		<p>We make it happen</p>
		<h1>
			<span class="customSpan">Websites</span>
			<span class="customSpan">Apps</span>
			<span class="customSpan">Branding</span>
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
