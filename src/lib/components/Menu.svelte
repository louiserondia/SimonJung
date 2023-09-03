<script lang="ts">
	let isTransformed: boolean = false;
	let optionsOpened: boolean = false;
	let tabOpened: boolean = false;

	function clickOnTitle() {
		optionsOpened = !optionsOpened;
		setTimeout(() => {
			isTransformed = !isTransformed;
		}, 10);
	}

	function openTab(event: MouseEvent) {
		const x = event.clientX;
		const y = event.clientY;

		if (x > window.innerWidth / 2 && y > window.innerHeight / 2) tabOpened = !tabOpened;
	}
</script>

<div class="title">
	<h1 on:click={clickOnTitle}>SIMON JUNG</h1>
</div>
{#if optionsOpened}
	<div class="option yo" class:transformed={isTransformed}>
		<h2>Yo</h2>
	</div>
	<div class="option ok" class:transformed={isTransformed}>
		<h2>Ok</h2>
	</div>
	<div class="option oui" class:transformed={isTransformed}>
		<h2>Oui</h2>
	</div>
	<div class="option contact" class:transformed={isTransformed} class:transformed-2={tabOpened}>
		<!-- <img src="/img/nuage.png" alt="nuage" class="nuage"/> -->
		<button on:click={(e) => openTab(e)}>Contact</button>
	</div>
	{#if tabOpened}
		<div class="contact-tab">
			<div>
				<h3>Appelez moi !!!</h3>
				<p>
					Bonjour je m'appelle Simon je suis cool
				</p>
			</div>
		</div>
	{/if}
{/if}

<style lang="scss">
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
		transition: transform 1s ease-out, color 0.5s linear;
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

	.transformed {
		color: black;
	}

	.contact.transformed {
		transform: translate(20vw, 17vh);
	}

	.contact.transformed-2 {
		transform: translate(15vw, 13vh);
	}

	.yo.transformed {
		transform: translate(-20vw, -17vh);
	}

	.ok.transformed {
		transform: translate(-20vw, 17vh);
	}

	.oui.transformed {
		transform: translate(20vw, -17vh);
	}


	.contact-tab {
		display: flex;
		position: absolute;
		bottom: 5rem;
		right: 5rem;
		width: 15rem;
		height: 15rem;
		border: 2px solid black;
		div {
			margin: 0.5rem;
		}
	}

</style>
