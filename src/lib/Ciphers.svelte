<script>
  import CryptoJS from 'crypto-js';
  let cipherAlgorithm = 'AES';
  let cipherOption = 'encrypt';
  let disableActionButton = false;
  let decryptedString = '';
  let encryptedString = '';
  let encodeURIComponentOfencryptedString = '';
  let copyBtnForDecryptedString = {
    isCopied: false,
    copiedString: ''
  };
  let copyBtnForEncryptedString = {
    isCopied: false,
    copiedString: ''
  };
  let copyBtnForEncodeUrlComponentString = {
    isCopied: false,
    copiedString: ''
  };
  let key = '';
  let count = 0;
  const cipherFunction = (cipherOption) => {
    if (encryptedString == '' && encodeURIComponentOfencryptedString != '') {
      encryptedString = decodeURIComponent(encodeURIComponentOfencryptedString);
    }
    switch (cipherAlgorithm) {
      case 'AES':
        if (cipherOption == 'encrypt') {
          encryptedString = CryptoJS.AES.encrypt(
            decryptedString,
            key
          ).toString();
        } else {
          decryptedString = CryptoJS.AES.decrypt(encryptedString, key).toString(
            CryptoJS.enc.Utf8
          );
        }
        break;
      case 'DES':
        if (cipherOption == 'encrypt') {
          encryptedString = CryptoJS.DES.encrypt(
            decryptedString,
            key
          ).toString();
        } else {
          decryptedString = CryptoJS.DES.decrypt(encryptedString, key).toString(
            CryptoJS.enc.Utf8
          );
        }
        break;
      case 'Triple_DES':
        if (cipherOption == 'encrypt') {
          encryptedString = CryptoJS.TripleDES.encrypt(
            decryptedString,
            key
          ).toString();
        } else {
          decryptedString = CryptoJS.TripleDES.decrypt(
            encryptedString,
            key
          ).toString(CryptoJS.enc.Utf8);
        }
        break;
      default:
        encryptedString = CryptoJS.AES.encrypt(decryptedString, key).toString();
    }
    if (encryptedString !== '') {
      encodeURIComponentOfencryptedString = encodeURIComponent(encryptedString);
    }
  };

  const getActionButtonText = (cipherOption) => {
    if (cipherOption == 'encrypt') {
      return 'Encrypt';
    }

    if (cipherOption == 'decrypt') {
      return 'Decrypt';
    }
    return 'Action';
  };

  const getActionButtonDisableStatus = () => {
    if (decryptedString == '' && cipherOption == 'encrypt') {
      disableActionButton = true;
    } else if (encryptedString == '' && cipherOption == 'decrypt') {
      disableActionButton = true;
    } else {
      disableActionButton = false;
    }
  };

  getActionButtonDisableStatus();

  const handleCipherOptionCheck = (option) => {
    if (option == 'encrypt') {
      encryptedString = '';
      encodeURIComponentOfencryptedString = '';
    }

    if (option == 'decrypt') {
      decryptedString = '';
    }
  };

  const copyTextToClipboardForEncryptedString = () => {
    if (!encryptedString) {
      return false;
    }
    copyBtnForEncryptedString.isCopied = true;
    copyBtnForEncryptedString.copiedString = encryptedString;
    navigator.clipboard.writeText(encryptedString);
  };

  const copyTextToClipboardForencodeURIComponentOfencryptedString = () => {
    if (!encodeURIComponentOfencryptedString) {
      return false;
    }
    copyBtnForEncodeUrlComponentString.isCopied = true;
    copyBtnForEncodeUrlComponentString.copiedString =
      encodeURIComponentOfencryptedString;
    navigator.clipboard.writeText(encodeURIComponentOfencryptedString);
  };

  const copyTextToClipboardForDecryptedString = () => {
    if (!decryptedString) {
      return false;
    }
    copyBtnForDecryptedString.isCopied = true;
    copyBtnForDecryptedString.copiedString = decryptedString;
    navigator.clipboard.writeText(decryptedString);
  };

  const onBlurCopyTextBox = () => {
    copyBtnForEncryptedString = {
      isCopied: false,
      copiedString: ''
    };
    copyBtnForEncodeUrlComponentString = {
      isCopied: false,
      copiedString: ''
    };
    copyBtnForDecryptedString = {
      isCopied: false,
      copiedString: ''
    };
  };
</script>

<div>
  <div class="container-fluid col-xxl-6 py-4 pt-0">
    <div class="row gy-2">
      <div>
        <span class="form-label text-primary fw-bold">Cipher Option</span>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="cipherOption_encrypt"
            id="cipherOption_encrypt"
            bind:group={cipherOption}
            value="encrypt"
            on:click={() => handleCipherOptionCheck('encrypt')}
            checked
          />
          <label class="form-check-label" for="cipherOption_encrypt">
            Encrypt
          </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="cipherOption_decrypt"
            id="cipherOption_decrypt"
            bind:group={cipherOption}
            value="decrypt"
            on:click={() => handleCipherOptionCheck('decrypt')}
          />
          <label class="form-check-label" for="cipherOption_decrypt">
            Decrypt
          </label>
        </div>
      </div>
      <div>
        <span class="form-label text-primary fw-bold">Plain String</span>
        {#if cipherOption === 'decrypt'}
          <textarea
            bind:value={decryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="enter the string you want to encrypt"
            readonly
            on:click={copyTextToClipboardForDecryptedString}
            on:blur={onBlurCopyTextBox}
          />
          {#if copyBtnForDecryptedString.isCopied}
            <span class="text-success copy-btn">Copied text to clipboard</span>
          {:else}
            <span class="copy-btn">Click to copy</span>
          {/if}
        {:else}
          <textarea
            bind:value={decryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="enter the string you want to encrypt"
            on:keyup={getActionButtonDisableStatus}
          />
        {/if}
      </div>
      <div>
        <span class="form-label text-primary fw-bold">Secret Key</span>
        <input
          bind:value={key}
          type="text"
          class="form-control"
          placeholder="key"
          aria-label="key"
          required="required"
        />
      </div>
      <div>
        <span class="form-label text-primary fw-bold">Encrypted String</span>
        {#if cipherOption === 'encrypt'}
          <textarea
            bind:value={encryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="encryptedString"
            readonly
            on:click={copyTextToClipboardForEncryptedString}
            on:blur={onBlurCopyTextBox}
          />
          {#if copyBtnForEncryptedString.isCopied}
            <span class="text-success copy-btn">Copied text to clipboard</span>
          {:else}
            <span class="copy-btn">Click to copy</span>
          {/if}
        {:else}
          <textarea
            bind:value={encryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="encryptedString"
            on:keyup={getActionButtonDisableStatus}
          />
        {/if}
      </div>
      <div>
        <span class="form-label text-primary fw-bold"
          >encodeURIComponent of encryptedString</span
        >
        {#if cipherOption === 'encrypt'}
          <textarea
            bind:value={encodeURIComponentOfencryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="encodeURIComponent of encryptedString"
            readonly="readonly"
            on:click={copyTextToClipboardForencodeURIComponentOfencryptedString}
            on:blur={onBlurCopyTextBox}
          />
          {#if copyBtnForEncodeUrlComponentString.isCopied}
            <span class="text-success copy-btn">Copied text to clipboard</span>
          {:else}
            <span class="copy-btn">Click to copy</span>
          {/if}
        {:else}
          <textarea
            bind:value={encodeURIComponentOfencryptedString}
            class="form-control"
            aria-label="With textarea"
            style="resize:none"
            placeholder="encodeURIComponent of encryptedString"
          />
        {/if}
      </div>
      <div>
        <span class="form-label text-primary fw-bold"
          >The Cipher Algorithms</span
        >
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="AES"
            id="AES"
            bind:group={cipherAlgorithm}
            value="AES"
            checked
          />
          <label class="form-check-label" for="AES"> AES </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="DES"
            id="DES"
            bind:group={cipherAlgorithm}
            value="DES"
          />
          <label class="form-check-label" for="DES"> DES </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="Triple-DES"
            id="Triple_DES"
            bind:group={cipherAlgorithm}
            value="Triple_DES"
          />
          <label class="form-check-label" for="Triple_DES"> Triple DES </label>
        </div>
      </div>
      <div>
        <hr />
      </div>
      <div class="mx-auto" style="width:6rem">
        <button on:click={cipherFunction(cipherOption)} class="btn btn-primary">
          {getActionButtonText(cipherOption)}
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
</style>
