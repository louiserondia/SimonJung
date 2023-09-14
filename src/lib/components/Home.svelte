<script lang="ts">
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';
	import Menu from '$lib/components/Menu.svelte';

	const srcs: string[] = ['/img/1.PNG', '/img/2.PNG', '/img/3.PNG'];
	const objects: string[] = ['/img/1a.png', '/img/2a.png', '/img/3a.png'];
	const hover: string[] = ['/img/1b.png', '/img/2b.png', '/img/3b.png'];

	let isTransparent: boolean = false;
	let index: number;
	let clicks: number = 0;

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;
	
	let img;
	let sizeImg;

	onMount(() => {
		if (typeof document !== 'undefined' && browser) {
			index = randomIndex(-1);
			canvas = document.createElement('canvas');
			ctx = canvas.getContext('2d') as CanvasRenderingContext2D;
			img = document.getElementById('img-overlay') as HTMLElement;
			sizeImg = img.getBoundingClientRect().width;
		}
	});


	function randomIndex(index: number) {
		let res = Math.floor(Math.random() * srcs.length);
		while (res === index) res = Math.floor(Math.random() * srcs.length);
		return res;
	}
	
	function handleMouseMove(event: MouseEvent) {
		let img = event.target as HTMLImageElement;
		canvas.width = img.width;
		canvas.height = img.height;
		ctx.drawImage(img, 0, 0, img.width, img.height);
		const rect = img.getBoundingClientRect();
		const x = Math.floor(((event.clientX - rect.left) / rect.width) * img.width);
		const y = Math.floor(((event.clientY - rect.top) / rect.height) * img.height);
		
		const pixel = ctx.getImageData(x, y, 1, 1).data;
		isTransparent = pixel[3] === 0;
		if (!isTransparent) {
			img.src = hover[index];
		} else img.src = objects[index];
	}
	
	function handleMouseUp() {
		if (!isTransparent) {
			index = randomIndex(index);
			clicks++;
		}
	}

</script>

{#if clicks < 3}
	<div class="img-container">
		<img class="img-overlay" src={srcs[index]} alt={srcs[index]} />
		<img
			class="img-overlay"
			src={objects[index]}
			alt={objects[index]}
			on:mousemove={(e) => handleMouseMove(e)}
			on:mouseup={handleMouseUp}
		/>
	</div>
{:else}
	<Menu />
{/if}

<button
	class="home click"
	on:click={() => {
		clicks = 3;
	}}
>
	CLICK 3
</button>

<button
	class="home"
	on:click={() => {
		clicks = 0;
	}}
>
	<img src="/img/home.png" alt="home" class="home-img" />
</button>

<style lang="scss">
	$var: sizeImg;
	@import '$lib/style/header.scss';

	.img-container {
		position: relative;
		width: 100vw;
		height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
		.img-overlay {
			position: absolute;
			margin: auto;
			width: 90%;
			max-width: 450px;
			@media only screen and (max-width: 500px) {
				height: auto;
				width: 90%;
				max-width: 550px;
			}
			@media only screen and (max-height: 700px) {
				width: auto;
				height: 90%;
				max-height: 650px;
			}
			@media only screen and (max-width: 500px) and (max-height: 700px) {
				height: auto;
				width: 90%;
				max-width: 550px;
			}
		}
	}

	:global(body.dark-mode) .img-container {
		@include dark-mode-bg-color;
	}

	button.home {
		position: absolute;
		right: 1rem;
		bottom: 1rem;
		background: none;
		color: inherit;
		border: none;
		cursor: pointer;
		.home-img {
			width: 7em;
			@media (max-width: 550px) {
				width: 18vw;

			}
		}
	}

	:global(body.dark-mode) button.home {
		color: white;
	}

	:global(body.dark-mode) .home-img {
		content: url('/img/home-white.png');
	}

	.click {
		right: 33vw !important;
		bottom: 2rem !important;
	}

</style>
