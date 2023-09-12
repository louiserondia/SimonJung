<script lang="ts">

	let isTransformed: boolean = false;
	let optionsOpened: boolean = false;
	let contactOpened: boolean = false;
	let yoOpened: boolean = false;
	let ouiOpened: boolean = false;
	let okOpened: boolean = false;

	function enterTitle() {
		optionsOpened = true;
		setTimeout(() => {
			isTransformed = true;
		}, 10);
	}

	function leaveTitle() {
		optionsOpened = false;
		setTimeout(() => {
			isTransformed = false;
		}, 10);
	}

	function openTab(event: MouseEvent) {
		if (!optionsOpened)
			return;
		
		const x = event.clientX;
		const y = event.clientY;

		if (x < window.innerWidth / 2 && y < window.innerHeight / 2) yoOpened = !yoOpened;
		else if (x > window.innerWidth / 2 && y < window.innerHeight / 2) ouiOpened = !ouiOpened;
		else if (x < window.innerWidth / 2 && y > window.innerHeight / 2) okOpened = !okOpened;
		else if (x > window.innerWidth / 2 && y > window.innerHeight / 2)
			contactOpened = !contactOpened;
	}

	// protéger pour pas que quand on clique sur simon ça ouvre les onglets
</script>

<div class="title">
	<h1 on:mouseenter={enterTitle}>SIMON JUNG</h1>
</div>
{#if optionsOpened}
	<div class="option yo" class:transformed={isTransformed} class:transformed-2={yoOpened}>
		<button on:click={(e) => openTab(e)}>yo</button>
	</div>
	<div class="option oui" class:transformed={isTransformed} class:transformed-2={ouiOpened}>
		<button on:click={(e) => openTab(e)}>oui</button>
	</div>
	<div class="option ok" class:transformed={isTransformed} class:transformed-2={okOpened}>
		<button on:click={(e) => openTab(e)}>ok</button>
	</div>
	<div class="option contact" class:transformed={isTransformed} class:transformed-2={contactOpened}>
		<!-- <img src="/img/nuage.png" alt="nuage" class="nuage"/> -->
		<button on:click={(e) => openTab(e)}>Contact</button>
	</div>
	{#if contactOpened}
		<div class="tab contact-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if yoOpened}
		<div class="tab yo-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if ouiOpened}
		<div class="tab oui-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if okOpened}
		<div class="tab ok-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
{/if}

<style lang="scss">
	@import '$lib/style/header.scss';

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

	:global(body.dark-mode) .title {
		@include dark-mode-bg-color;
		background-image: url('/img/stars.gif');
		background-size: 75%;
		background-repeat: repeat;
		background-attachment: fixed;
	}

	.option {
		background-color: transparent;
		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
		// background-image: url("/img/nuage.png");
		// height: 8rem;
		// width: 8rem;
		display: flex;
		position: absolute;
		top: 38vh;
		left: 48vw;
		color: transparent;
		text-align: center;
		transform: translate(0, 0);
		transition: transform 0.5s ease-out, color 0.5s linear;
		h2 {
			margin: auto;
		}
	}

	button {
		background: none;
		border: none;
		font-size: x-large;
		font-weight: bold;
		cursor: pointer;
	}

	:global(body.dark-mode) button {
		background-color: transparent;
		color: white;
	}

	.yo.transformed {
		transform: translate(-20vw, -17vh);
	}

	.yo.transformed-2 {
		transform: translate(-15vw, -13vh);
	}

	.oui.transformed {
		transform: translate(20vw, -17vh);
	}

	.oui.transformed-2 {
		transform: translate(15vw, -13vh);
	}

	.ok.transformed {
		transform: translate(-20vw, 17vh);
	}

	.ok.transformed-2 {
		transform: translate(-15vw, 13vh);
	}

	.contact.transformed {
		transform: translate(20vw, 17vh);
	}

	.contact.transformed-2 {
		transform: translate(15vw, 13vh);
	}

	.tab {
		display: flex;
		position: absolute;
		width: 15rem;
		height: 15rem;
		div {
			margin: 0.5rem;
		}
	}

	:global(body.dark-mode) .tab {
		@include dark-mode-bg-color
	}

	.contact-tab {
		bottom: 3.5rem;
		right: 3.5rem;
		border: 2px solid black;
	}

	.yo-tab {
		top: 3.5rem;
		left: 3.5rem;
		border: 2px solid red;
	}

	.oui-tab {
		top: 3.5rem;
		right: 3.5rem;
		border: 2px solid blue;
	}

	.ok-tab {
		bottom: 3.5rem;
		left: 3.5rem;
		border: 2px solid green;
	}
</style>
