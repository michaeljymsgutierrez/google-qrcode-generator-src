<svelte:head>
	<script async src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
</svelte:head>

<script>
  let value = '';

  function onInput(event) {
    const input = this;
    value = this.value;
  }

  function onClickGenerate() {
    new QRCode(document.getElementById("qrcode"), value);
  }
</script>

<div class="qrcode-container">
  <div class="text-field-container">
    <label>Input text here:</label>
    <input class="text-field" placeholder="Just another boring input..." on:input={onInput} {value} />
    <button on:click={onClickGenerate}>Generate QR Code</button>
  </div>
  <div id="qrcode"></div>
</div>

<style>
  .qrcode-container {
    height: 100vh;
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
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }

  label {
    font-size: 16px;
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
    background-color: #4CAF50;
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
</style>


