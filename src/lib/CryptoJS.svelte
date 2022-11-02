<script>
  import CryptoJS from "crypto-js"
  const siteHeader = "CryptoJS Demo"
  let cipherAlgorithm = "AES"
  let decryptedString = "" 
  let encryptedString = "" 
  let encodeURIComponentOfencryptedString = "" 
  let key = ""
  let count = 0
  const encrypt = () => {
    if (decryptedString == ""){
      return false
    }
    switch (cipherAlgorithm) {
      case 'AES':
        encryptedString = CryptoJS.AES.encrypt(decryptedString, key).toString();
        console.log({cipherAlgorithm,decryptedString, key})
        break;
      case 'DES':
        encryptedString = CryptoJS.DES.encrypt(decryptedString, key).toString();
        console.log({cipherAlgorithm,decryptedString, key})
        break;
      case 'Triple_DES':
        encryptedString = CryptoJS.TripleDES.encrypt(decryptedString, key).toString();
        console.log({cipherAlgorithm,decryptedString, key})
        break;
      default:
        encryptedString = CryptoJS.AES.encrypt(decryptedString, key).toString();
    }
    if(encryptedString !== ""){
      encodeURIComponentOfencryptedString = encodeURIComponent(encryptedString)
    }
  }
</script>

<div>
  <nav class="navbar bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href=".">
        <strong style="color:white">{siteHeader}</strong>
      </a>
    </div>
  </nav>
  <div class="container-fluid col-xxl-6 py-4">
    <div class="row gy-2">
      <div>
        <label class="form-label text-primary fw-bold">Plain String</label>
        <textarea bind:value={decryptedString} class="form-control" aria-label="With textarea" style="resize:none" placeholder="enter string you want to encrypt"></textarea>
      </div>
      <div>
        <label class="form-label text-primary fw-bold">Key</label>
        <input bind:value={key} type="text" class="form-control" placeholder="key" aria-label="key" required="required">
      </div>
      <div>
        <label class="form-label text-primary fw-bold">Encrypted String</label>
        <textarea class="form-control" aria-label="With textarea" style="resize:none" placeholder="encryptedString" readonly="readonly">{encryptedString}</textarea>
      </div>
      <div>
        <label class="form-label text-primary fw-bold">encodeURIComponent</label>
        <textarea class="form-control" aria-label="With textarea" style="resize:none" placeholder="encryptedString" readonly="readonly">{encodeURIComponentOfencryptedString}</textarea>
      </div>
      <div>
        <label class="form-label text-primary fw-bold">The Cipher Algorithms</label>
        <div class="form-check">
          <input class="form-check-input" type="radio" name="AES" id="AES" bind:group={cipherAlgorithm} value="AES" checked>
          <label class="form-check-label" for="AES">
            AES
          </label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="radio" name="DES" id="DES" bind:group={cipherAlgorithm} value="DES">
          <label class="form-check-label" for="DES">
            DES
          </label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="radio" name="Triple-DES" id="Triple_DES" bind:group={cipherAlgorithm} value="Triple_DES">
          <label class="form-check-label" for="Triple_DES">
            Triple DES
          </label>
        </div>
      </div>
      <div>
        <hr>
      </div>
      <div class="mx-auto" style="width:6rem">
        <button on:click={encrypt} class="btn btn-primary">
          Encrypt
        </button>
      </div>
    </div>
  </div>
</div>
