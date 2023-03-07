<script>
	import Header from '../lib/components/Header.svelte';
	import { gsap } from 'gsap';
	import { onMount } from 'svelte';

	let hoveringMain = false;
	let index = 0;
	const videos = ['websites.mp4', 'apps.mp4', 'branding.mp4'];

	onMount(() => {
		window.addEventListener('mousemove', (e) => {
			gsap.to('.customCursor', {
				opacity: 1,
				x: e.clientX - 50,
				y: e.clientY - 50
			});
		});

		const customMain = document.querySelector('.customMain');
		customMain?.addEventListener('mouseenter', (e) => {
			gsap.to('.customCursor', {
				scale: 8,
				duration: 0.5
			});
		});
		customMain?.addEventListener('mouseleave', () => {
			gsap.to('.customCursor', {
				scale: 1,
				duration: 0.5
			});
		});

		const customSpan = document.querySelectorAll('.customSpan');
		customSpan.forEach((span) => {
			span?.addEventListener('mouseenter', () => {
				gsap.to('.customCursor', {
					scale: 15
				});
			});
			span?.addEventListener('mouseleave', () => {
				gsap.to('.customCursor', {
					scale: 8
				});
			});
		});
		const customVideo = document.querySelectorAll('.customVideo');
		customVideo.forEach((video) => {
			if (index === 0) {
				gsap.to('.customVideo', {
					delay: 1,
					scale: 1
				});
			}
		});
	});
</script>

<div class="h-[100vh] flex flex-col">
	<Header />
	<main
		class="flex justify-center px-[250px] flex-col grow customMain"
		on:mouseenter={() => (hoveringMain = true)}
		on:mouseleave={() => (hoveringMain = false)}
	>
		<p>We make it happen</p>
		<h1>
			<span
				class="customSpan"
				on:mouseenter={() => {
					index = 0;
				}}>Websites</span
			>
			<span
				class="customSpan"
				on:mouseenter={() => {
					index = 1;
				}}>Apps</span
			>
			<span
				class="customSpan"
				on:mouseenter={() => {
					index = 2;
				}}>Branding</span
			>
		</h1>
	</main>

	<div class="h-8 w-8 rounded-full absolute customCursor opacity-0 -z-10">
		<video
			src={videos[0]}
			class={`h-full object-cover customVideo absolute scale-0 rounded-full autoplay ${
				index === 0 ? 'opacity-100' : 'opacity-0'
			}`}
		/>
		<video
			src={videos[1]}
			class={`h-full object-cover customVideo absolute scale-0 rounded-full autoplay ${
				index === 1 ? 'opacity-100' : 'opacity-0'
			}`}
		/>
		<video
			src={videos[2]}
			class={`h-full object-cover customVideo absolute scale-0 rounded-full ${
				index === 2 ? 'opacity-100' : 'opacity-0'
			}`}
			autoplay
		/>
	</div>
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
