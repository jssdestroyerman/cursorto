<script>
	import Header from '../lib/components/Header.svelte';
	import { gsap } from 'gsap';
	import { onMount } from 'svelte';

	let hoveringMain = false;
	let index = 0;
	const videos = ['websites.mp4', 'apps.mp4', 'branding.mp4'];

	onMount(() => {
		window.addEventListener('mousemove', (e) => {
			gsap.to('.styleCursor', {
				opacity: 1,
				x: e.clientX,
				y: e.clientY
			});
		});

		const styleMain = document.querySelector('.styleMain');
		styleMain?.addEventListener('mouseenter', () => {
			hoveringMain = true;
			gsap.to('.styleCursor', {
				scale: 8,
				duration: 0.5
			});
		});
		styleMain?.addEventListener('mouseleave', () => {
			hoveringMain = false;
			gsap.to('.styleCursor', {
				scale: 1,
				duration: 0.5
			});
		});

		const customSpan = document.querySelectorAll('.customSpan');
		customSpan.forEach((span) => {
			span?.addEventListener('mouseenter', () => {
				gsap.to('.styleCursor', {
					scale: 15
				});
			});
			span?.addEventListener('mouseleave', () => {
				gsap.to('.styleCursor', {
					scale: 8
				});
			});
		});

		const styleLi = document.querySelectorAll('.styleLi');
		styleLi.forEach((li) => {
			li.addEventListener('mouseenter', () => {
				gsap.to('.styleCursor', {
					scale: 0,
					duration: 0.5
				});
			});

			li.addEventListener('mouseleave', () => {
				gsap.to('.styleCursor', {
					scale: 1,
					duration: 0.5
				});
			});
		});
	});
</script>

<div class="h-[100vh] flex flex-col">
	<Header />
	<main class="flex justify-center px-[250px] flex-col grow styleMain">
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

	<div class={`styleCursor ${hoveringMain ? '' : 'bg-gray-100'}`}>
		<video
			src={videos[0]}
			class={`customVideo ${index === 0 ? 'scale-100' : 'scale-0'} ${
				hoveringMain ? '' : 'delay-300 opacity-0'
			}`}
			autoplay
			loop
		>
			<track kind="captions" /></video
		>
		<video
			src={videos[1]}
			class={`customVideo ${index === 1 ? 'scale-100' : 'scale-0'} ${
				hoveringMain ? '' : 'delay-300 opacity-0'
			}`}
			autoplay
			loop
		>
			<track kind="captions" /></video
		>
		<video
			src={videos[2]}
			class={`customVideo ${index === 2 ? 'scale-100' : 'scale-0'} ${
				hoveringMain ? '' : 'delay-300 opacity-0'
			}`}
			autoplay
			loop
		>
			<track kind="captions" />
		</video>
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
	.styleCursor {
		@apply h-8 w-8 rounded-full fixed opacity-0 translate-x-[-50%] translate-y-[-50%] pointer-events-none;
		transform: scale(1);
	}
	.customVideo {
		@apply h-full object-cover absolute rounded-full transition duration-700;
	}
</style>
