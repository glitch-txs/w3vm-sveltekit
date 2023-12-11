<script lang="ts" >
import { initW3 } from '@w3vm/core'
import { WalletConnect } from '@w3vm/walletconnect'
import { connectW3, connectors, disconnectW3, address, chainId, status } from '@w3vm/svelte'

const projectId = 'WALLETCONNECT_PROJECT_ID'

initW3({
  connectors: [
    new WalletConnect({ 
      projectId,
      showQrModal: true,
      optionalChains:[1, 137]
    })
  ],
  defaultChain: 1, // Optional
})

</script>
<h1>Welcome to W3vm & SvelteKit</h1>


{#each $connectors as connector}
<button disabled={Boolean($status)} on:click={()=>connectW3({ connector })}>
  <img src={connector.icon} alt={connector.name} />
  {connector.name}
</button>
{/each}

{#if $address}
<div>
  user: {$address}
</div>
<div>
  chain ID: {$chainId}
</div>
<button on:click={disconnectW3}>
  disconnect
</button>
{/if}