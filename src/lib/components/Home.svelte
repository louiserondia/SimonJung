<script lang="ts">
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';

	const srcs: string[] = ['/img/1.PNG', '/img/2.PNG', '/img/3.PNG'];
	const objects: string[] = ['/img/1a.png', '/img/2a.png', '/img/3a.png'];
	const hover: string[] = ['/img/1b.png', '/img/2b.png', '/img/3b.png'];

	let isTransparent: boolean = false;
	let index: number = randomIndex(-1);
	let clicks: number = 0;

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;

	onMount(() => {
		if (typeof document !== 'undefined' && browser) {
			canvas = document.createElement('canvas');
			ctx = canvas.getContext('2d') as CanvasRenderingContext2D;
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
		if (!isTransparent) img.src = hover[index];
		else img.src = objects[index];
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
<div class="title">
	<h1 on:mouseup={() => {clicks = 0;}}>SIMON JUNG</h1>
</div>
{/if}

<style lang="scss">
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
			height: 80vh;
			width: auto;
		}
	}
	
	.title {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100vh;
		h1 {
			cursor: pointer;
			font-size: xx-large;
			margin-bottom: 10rem;
		}
	}
</style>
