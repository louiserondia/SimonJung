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

	function clickOnTitle() {
		// const option = document.getElementById('option') as HTMLElement;
		if (isTransformed) {
			optionsOpened = false;
			okOpened = false;
			yoOpened = false;
			ouiOpened = false;
			contactOpened = false;
			setTimeout(() => {
				isTransformed = false;
			}, 10);
		} else {
			optionsOpened = true;
			setTimeout(() => {
				// option.classList.toggle('transformed');
				isTransformed = true;
			}, 10);
		}
	}

	function openTab(event: MouseEvent) {
		if (!optionsOpened) return;

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
	<h1 on:mouseenter={enterTitle} on:mouseup={clickOnTitle}>SIMON JUNG</h1>
	<!-- <h1 on:click={clickOnTitle}>SIMON JUNG</h1> -->
</div>
{#if optionsOpened}
	<div class="option yo" class:transformed={isTransformed} class:transformed-2={yoOpened}>
		<button on:click={(e) => openTab(e)}>
			<p>yo</p>
		</button>
	</div>
	<div class="option oui" class:transformed={isTransformed} class:transformed-2={ouiOpened}>
		<button on:click={(e) => openTab(e)}>
			<p>oui</p>
		</button>
	</div>
	<div class="option ok" class:transformed={isTransformed} class:transformed-2={okOpened}>
		<button on:click={(e) => openTab(e)}>
			<p>ok</p>
		</button>
	</div>
	<div class="option contact" class:transformed={isTransformed} class:transformed-2={contactOpened}>
		<!-- <img src="/img/nuage.png" alt="nuage" class="nuage"/> -->
		<button on:click={(e) => openTab(e)}>
			<p>Contact</p>
		</button>
	</div>
	{#if contactOpened}
		<div on:click={() => {
			contactOpened = false;
		}}
		class="tab contact-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if yoOpened}
		<div
			on:click={() => {
				yoOpened = false;
			}}
			class="tab yo-tab"
		>
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if ouiOpened}
		<div on:click={() => {
			ouiOpened = false;
		}}
		class="tab oui-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>Bonjour je m'appelle Simon je suis cool</p>
			</div>
		</div>
	{/if}
	{#if okOpened}
		<div on:click={() => {
			okOpened = false;
		}}
		class="tab ok-tab">
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
		background-image: url('/img/nuage.png');
		height: 1.5rem;
		width: 1.5rem;
		display: flex;
		position: absolute;
		top: 50vh;
		left: 50vw;
		color: transparent;
		text-align: center;
		transition: all 0.5s ease-out;
		// transition: transform 0.5s ease-out, width 0.5s ease-out, height 0.5s ease-out;
		transform: translate(0, 0);
		button {
			margin: auto;
		}
	}

	:global(body.dark-mode) .option {
		background-image: url('/img/nuage-night.png');
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

	.transformed {
		width: 9rem;
		height: 9rem;
	}

	.yo.transformed {
		transform: translate(calc(-20vw - 4.5rem), calc(-17vh - 4.5rem));
	}

	.yo.transformed-2 {
		transform: translate(calc(-15vw - 4.5rem), calc(-13vh - 4.5rem));
	}

	.oui.transformed {
		transform: translate(calc(20vw - 4.5rem), calc(-17vh - 4.5rem));
	}

	.oui.transformed-2 {
		transform: translate(calc(15vw - 4.5rem), calc(-13vh - 4.5rem));
	}

	.ok.transformed {
		transform: translate(calc(-20vw - 4.5rem), calc(17vh - 4.5rem));
	}

	.ok.transformed-2 {
		transform: translate(calc(-15vw - 4.5rem), calc(13vh - 4.5rem));
	}

	.contact.transformed {
		transform: translate(calc(20vw - 4.5rem), calc(17vh - 4.5rem));
	}

	.contact.transformed-2 {
		transform: translate(calc(15vw - 4.5rem), calc(13vh - 4.5rem));
	}

	.tab {
		display: flex;
		position: absolute;
		width: 15rem;
		height: 15rem;
		cursor: pointer;
		div {
			margin: 0.5rem;
		}
	}

	:global(body.dark-mode) .tab {
		@include dark-mode-bg-color;
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
