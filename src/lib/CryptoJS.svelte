<script>
  import CryptoJS from "crypto-js"
  let decryptedString = "" 
  let encryptedString = "" 
  let encodeURIComponentOfencryptedString = "" 
  let key = ""
  let count = 0
  const encrypt = () => {
    encryptedString = CryptoJS.AES.encrypt(decryptedString, key).toString();
    if(encryptedString !== ""){
      encodeURIComponentOfencryptedString = encodeURIComponent(encryptedString)
    }
  }
</script>

<div>
  <nav class="navbar bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">
        <strong style="color:white">CryptoJS Demo</strong>
      </a>
    </div>
  </nav>
  <div class="container-fluid w-50 py-4">
    <div class="row gy-3">
      <div>
        <label for="exampleFormControlInput1" class="form-label text-primary fw-bold">Plain String</label>
        <textarea bind:value={decryptedString} class="form-control" aria-label="With textarea" style="resize:none" placeholder="enter string you want to encrypt"></textarea>
      </div>
      <div>
        <label for="exampleFormControlInput1" class="form-label text-primary fw-bold">Key</label>
        <input bind:value={key} type="text" class="form-control" placeholder="key" aria-label="key" required="required">
      </div>
      <div>
        <label for="exampleFormControlInput1" class="form-label text-primary fw-bold">Encrypted String</label>
        <textarea class="form-control" aria-label="With textarea" style="resize:none" placeholder="encryptedString" readonly="readonly">{encryptedString}</textarea>
      </div>
      <div>
        <label for="exampleFormControlInput1" class="form-label text-primary fw-bold">encodeURIComponent</label>
        <textarea class="form-control" aria-label="With textarea" style="resize:none" placeholder="encryptedString" readonly="readonly">{encodeURIComponentOfencryptedString}</textarea>
      </div>
      <button on:click={encrypt} class="btn btn-primary mx-auto" style="width:6rem">
        Encrypt
      </button>
    </div>
  </div>
</div>
