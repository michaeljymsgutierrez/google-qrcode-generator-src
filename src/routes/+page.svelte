<script>
	import { onMount } from 'svelte'
	let value = ''

	onMount(() => {
		if (hasStringParam()) {
			const currentURL = window.location.href
			const currentOrigin = window.location.origin
			const extractedString = currentURL.replace(`${currentOrigin}/?string=`, '')

			value = extractedString
			generateQRCode()
		}
	})

	function onInput(event) {
		const input = this
		value = this.value
	}

	function generateQRCode() {
		const canvas = document.querySelector('#qrcode > canvas')
		const image = document.querySelector('#qrcode > img')

		if (canvas) canvas.remove()
		if (image) image.remove()

		const currentOrigin = window.location.origin
		const updatedURL = `${currentOrigin}/?string=${value}`
		window.history.pushState({ path: updatedURL }, '', updatedURL)

		new QRCode(document.getElementById('qrcode'), value)
	}

	function hasStringParam() {
		var url = new URL(window.location.href)
		return url.searchParams.has('string')
	}
</script>

<svelte:head>
	<script async src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
</svelte:head>

<div class="qrcode-container">
	<span id="forkongithub">
		<a href="https://github.com/michaeljymsgutierrez/google-qrcode-generator-src">
			Fork me on GitHub
		</a>
	</span>
	<div class="text-field-container">
		<label>Input text here</label>
		<input
			class="text-field"
			placeholder="Just another boring input..."
			on:input={onInput}
			{value}
		/>
		<button on:click={generateQRCode}>Generate QR Code</button>
	</div>
	<div id="qrcode"></div>
</div>

<style>
	.qrcode-container {
		height: 60vh;
		padding: 20px;
	}

	#qrcode {
		margin-left: auto;
		margin-right: auto;
		margin-top: 20px;
		display: flex;
		justify-content: center;
	}

	.text-field-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	label {
		font-size: 20px;
		font-family: monospace;
		font-weight: bold;
	}

	.text-field {
		width: 300px;
		height: 20px;
		font-size: 16px;
		padding: 2px 4px 2px 4px;
		border: 1px solid #777777;
		border-radius: 4px;
		margin: 4px;
	}

	button {
		display: inline-block;
		padding: 10px 20px;
		font-size: 16px;
		font-weight: bold;
		color: #fff;
		background-color: #4caf50;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		transition: background-color 0.3s;
	}

	button:hover {
		background-color: #45a049;
	}

	button:active {
		background-color: #398438;
	}

	#forkongithub a {
		background: #000;
		color: #fff;
		text-decoration: none;
		font-family: arial, sans-serif;
		text-align: center;
		font-weight: bold;
		padding: 5px 40px;
		font-size: 1rem;
		line-height: 2rem;
		position: relative;
		transition: 0.5s;
	}

	#forkongithub a:hover {
		background: #c11;
		color: #fff;
	}

	#forkongithub a::before,
	#forkongithub a::after {
		content: '';
		width: 100%;
		display: block;
		position: absolute;
		top: 1px;
		left: 0;
		height: 1px;
		background: #fff;
	}

	#forkongithub a::after {
		bottom: 1px;
		top: auto;
	}

	@media screen and (min-width: 800px) {
		#forkongithub {
			position: fixed;
			display: block;
			top: 0;
			right: 0;
			width: 200px;
			overflow: hidden;
			height: 200px;
			z-index: 9999;
		}

		#forkongithub a {
			width: 200px;
			position: absolute;
			top: 60px;
			right: -60px;
			transform: rotate(45deg);
			-webkit-transform: rotate(45deg);
			-ms-transform: rotate(45deg);
			-moz-transform: rotate(45deg);
			-o-transform: rotate(45deg);
			box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.8);
		}
	}
</style>
