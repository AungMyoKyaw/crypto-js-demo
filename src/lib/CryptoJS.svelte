<script>
  import Ciphers from './Ciphers.svelte';
  import Hashing from './Hashing.svelte';
  let hashingOrCiphers = 'ciphers';
</script>

<div>
  <div class="container-fluid col-xxl-6 pt-4 mb-0" style="margin-top: 3em;">
    <span class="form-label text-primary fw-bold">Hashing or Ciphers</span>
    <div class="form-check">
      <input
        class="form-check-input"
        type="radio"
        name="ciphers_cryptojs"
        id="ciphers_cryptojs"
        bind:group={hashingOrCiphers}
        value="ciphers"
        checked
      />
      <label class="form-check-label" for="ciphers_cryptojs"> Ciphers </label>
    </div>
    <div class="form-check">
      <input
        class="form-check-input"
        type="radio"
        name="hashing_cryptojs"
        id="hashing_cryptojs"
        bind:group={hashingOrCiphers}
        value="hashing"
      />
      <label class="form-check-label" for="hashing_cryptojs">Hashing</label>
    </div>
    <hr />
  </div>

  {#if hashingOrCiphers === 'ciphers'}
    <Ciphers />
  {:else}
    <Hashing />
  {/if}
</div>
