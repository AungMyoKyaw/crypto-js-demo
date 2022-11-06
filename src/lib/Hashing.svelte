<script>
  import CryptoJS from 'crypto-js';
  let cipherAlgorithm = 'AES';
  let hashingAlgorithm = 'MD5';
  let sha2Option = '';
  let sha3Option = '';
  let inputMessage = '';
  let hashingOutput = '';
  let chooseMoreOptionHash = {
    sha2: false,
    sha3: false
  };
  let copyBtnForHashString = {
    isCopied: false,
    copiedString: ''
  };
  const hashingFunction = () => {
    let algorithms = hashingAlgorithm;
    if (sha2Option) {
      algorithms = sha2Option;
    }
    if (sha3Option) {
      algorithms = sha3Option;
    }
    switch (algorithms) {
      case 'MD5':
        hashingOutput = CryptoJS.MD5(inputMessage);
        break;
      case 'SHA1':
        hashingOutput = CryptoJS.SHA1(inputMessage);
        break;
      case 'SHA224':
        hashingOutput = CryptoJS.SHA224(inputMessage);
        break;
      case 'SHA384':
        hashingOutput = CryptoJS.SHA384(inputMessage);
        break;
      case 'SHA256':
        hashingOutput = CryptoJS.SHA256(inputMessage);
        break;
      case 'SHA512':
        hashingOutput = CryptoJS.SHA512(inputMessage);
        break;
      case 'SHA3224':
        hashingOutput = CryptoJS.SHA3(inputMessage, { outputLength: 224 });
        break;
      case 'SHA3256':
        hashingOutput = CryptoJS.SHA3(inputMessage, { outputLength: 256 });
        break;
      case 'SHA3384':
        hashingOutput = CryptoJS.SHA3(inputMessage, { outputLength: 384 });
        break;
      case 'SHA3512':
        hashingOutput = CryptoJS.SHA3(inputMessage, { outputLength: 512 });
        break;
      case 'RIPEMD160':
        hashingOutput = CryptoJS.RIPEMD160(inputMessage);
        break;
      default:
        hashingOutput = '';
    }
  };

  const getActionButtonText = () => {
    return 'Hash';
  };

  const copyTextToClipboardForHashString = () => {
    if (!hashingOutput) {
      return false;
    }
    copyBtnForHashString.isCopied = true;
    copyBtnForHashString.copiedString = hashingOutput;
    navigator.clipboard.writeText(hashingOutput);
  };

  const onBlurCopyTextBox = () => {
    copyBtnForHashString = {
      isCopied: false,
      copiedString: ''
    };
  };

  const clearMoreOptionBox = () => {
    sha2Option = '';
    sha3Option = '';
    hashingOutput = '';
    chooseMoreOptionHash = {
      sha2: false,
      sha3: false
    };
  };

  const showMoreOptionForSha2 = () => {
    clearMoreOptionBox();
    chooseMoreOptionHash.sha2 = true;
  };

  const showMoreOptionForSha3 = () => {
    clearMoreOptionBox();
    chooseMoreOptionHash.sha3 = true;
    sha3Option = 'SHA3512';
  };
</script>

<div>
  <div class="container-fluid col-xxl-6 py-4 pt-0">
    <div class="row gy-2">
      <div>
        <span class="form-label text-primary fw-bold"
          >The Hashing Algorithms</span
        >
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="MD5"
            id="MD5"
            bind:group={hashingAlgorithm}
            value="MD5"
            checked
          />
          <label class="form-check-label" for="MD5"> MD5 </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="SHA-1"
            id="SHA-1"
            bind:group={hashingAlgorithm}
            value="SHA1"
            on:click={clearMoreOptionBox}
            checked
          />
          <label class="form-check-label" for="SHA-1">SHA-1</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="SHA-2"
            id="SHA-2"
            bind:group={hashingAlgorithm}
            value="SHA-2"
            on:click={showMoreOptionForSha2}
            checked
          />
          <label class="form-check-label" for="SHA-2">SHA-2</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="SHA-3"
            id="SHA-3"
            bind:group={hashingAlgorithm}
            value="SHA-3"
            on:click={showMoreOptionForSha3}
            checked
          />
          <label class="form-check-label" for="SHA-3">SHA-3</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="RIPEMD-160"
            id="RIPEMD-160"
            bind:group={hashingAlgorithm}
            value="RIPEMD160"
            on:click={clearMoreOptionBox}
            checked
          />
          <label class="form-check-label" for="RIPEMD-160">RIPEMD-160</label>
        </div>
      </div>
      {#if chooseMoreOptionHash.sha2}
        <div>
          <span class="form-label text-primary fw-bold">SHA-2 varients</span>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-256"
              id="SHA-256"
              bind:group={sha2Option}
              value="SHA256"
              checked
            />
            <label class="form-check-label" for="SHA-256">SHA-256</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-512"
              id="SHA-512"
              bind:group={sha2Option}
              value="SHA512"
              checked
            />
            <label class="form-check-label" for="SHA-512">SHA-512</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-224"
              id="SHA-224"
              bind:group={sha2Option}
              value="SHA224"
              checked
            />
            <label class="form-check-label" for="SHA-224">SHA-224</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-384"
              id="SHA-384"
              bind:group={sha2Option}
              value="SHA384"
              checked
            />
            <label class="form-check-label" for="SHA-384">SHA-384</label>
          </div>
        </div>
      {/if}
      {#if chooseMoreOptionHash.sha3}
        <div>
          <span class="form-label text-primary fw-bold"
            >SHA-3 output hash lengths</span
          >
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-3-224"
              id="SHA-3-224"
              bind:group={sha3Option}
              value="SHA3224"
              checked
            />
            <label class="form-check-label" for="SHA-3-224">SHA-3-224</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-3-256"
              id="SHA-3-256"
              bind:group={sha3Option}
              value="SHA3256"
              checked
            />
            <label class="form-check-label" for="SHA-3-256">SHA-3-256</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-3-384"
              id="SHA-3-384"
              bind:group={sha3Option}
              value="SHA3384"
              checked
            />
            <label class="form-check-label" for="SHA-3-384">SHA-3-384</label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="SHA-3-512"
              id="SHA-3-512"
              bind:group={sha3Option}
              value="SHA3512"
              checked
            />
            <label class="form-check-label" for="SHA-3-512"
              >SHA-3-512 (default)</label
            >
          </div>
        </div>
      {/if}
      <div>
        <span class="form-label text-primary fw-bold">Message</span>
        <textarea
          bind:value={inputMessage}
          class="form-control"
          aria-label="With textarea"
          style="resize:none"
          placeholder="Message"
        />
      </div>
      <div>
        <span class="form-label text-primary fw-bold">Output</span>
        <textarea
          bind:value={hashingOutput}
          class="form-control"
          aria-label="With textarea"
          style="resize:none"
          placeholder="hashingOutput"
          readonly
          on:click={copyTextToClipboardForHashString}
          on:blur={onBlurCopyTextBox}
        />
        {#if copyBtnForHashString.isCopied}
          <span class="text-success copy-btn">Copied text to clipboard</span>
        {:else}
          <span class="copy-btn">Click to copy</span>
        {/if}
      </div>
      <div>
        <hr />
      </div>
      <div class="mx-auto" style="width:6rem">
        <button on:click={hashingFunction} class="btn btn-primary">
          {getActionButtonText()}
        </button>
      </div>
    </div>
  </div>
</div>

<style>
  .copy-btn {
    font-weight: 500;
    font-size: 12px;
    line-height: 20px;
    letter-spacing: -0.2px;
    color: #9da2ad;
  }

  .form-check-label {
    cursor: pointer;
  }
  .form-check-input {
    cursor: pointer;
  }
</style>
