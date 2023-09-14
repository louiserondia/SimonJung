<script lang="ts">
	import Home from '$lib/components/Home.svelte';

	function darkMode() {
		window.document.body.classList.toggle('dark-mode');
	}

</script>

<body>
	<Home />

	<button
		class="dark-mode-btn"
		on:click={() => {
			darkMode();
		}}
		>NIGHT
	</button>
</body>

<style lang="scss">
	@import '$lib/style/header.scss';

	:global(body) {
		background-color: white;
		color: black;
		transition: background-color 0.3s;
	}

	:global(body.dark-mode) {
		background-color: #2f3480;
		color: white;
	}

	.dark-mode-btn {
		position: absolute;
		bottom: 2rem;
		left: 2rem;
		border: none;
		background-color: inherit;
		cursor: pointer;
	}

	:global(body.dark-mode) .dark-mode-btn{
		@include dark-mode-bg-color;
		
	}
</style>
