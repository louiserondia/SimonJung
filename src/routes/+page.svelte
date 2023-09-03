<script lang="ts">
	import Home from '$lib/components/Home.svelte';

	let isNightMode: boolean = false;
	let backgroundColor: string = 'white';
	let fontColor: string = 'black';

	function darkMode() {
		window.document.body.classList.toggle('dark-mode');
	}

	function nightMode() {
		isNightMode = !isNightMode;
		console.log(isNightMode);
		if (isNightMode === true) {
			backgroundColor = '#2f3480';
			fontColor = 'white';
		} else {
			backgroundColor = 'white';
			fontColor = 'black';
		}
	}
</script>

<!-- <body style="--backgroundColor:{backgroundColor}; --fontColor:{fontColor};"> -->
<body>
	<Home />

	<button
		class="night-mode"
		on:click={() => {
			darkMode();
		}}
		>NIGHT
	</button>
</body>

<style lang="scss">
	:global(body) {
		background-color: white;
		color: black;
		transition: background-color 0.3s;
	}

	:global(body.dark-mode) {
		background-color: #2f3480;
		color: white;
	}

	// body {
	// 	background-color: var(--backgroundColor);
	// 	color: var(--fontColor);
	// 	button {
	// 		color: var(--fontColor);
	// 	}
	// }

	.night-mode {
		position: absolute;
		bottom: 2rem;
		left: 2rem;
		border: none;
		background-color: inherit;
		cursor: pointer;
	}
</style>
