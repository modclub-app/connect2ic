
<img height="100" src="https://connect2ic.github.io/docs/img/connect2ic_logo_light.png" />

# Connect2IC
A toolkit which makes it trivial to support any wallet or identity provider, and make authenticated calls to canisters.

## Introduction
There are many new wallets coming out and adding support for these isn't always easy. Connect2ic allows you to get fully working auth for the most popular providers with only a few lines of code. Use the already styled `<ConnectDialog />` component or feel free to create your own. Connect2ic gives you full control and additionally provides you with convenient helper utilities such as `useCanister()` and `useTransfer()`.

## Full documentation
Visit https://connect2ic.github.io/docs/

See https://github.com/MioQuispe/create-ic-app/ for examples

## Community
You can ask us questions directly :)
https://discord.com/invite/4kqMVknpgZ

## Supported providers
- [Internet Identity](https://identity.ic0.app/)
- [Stoic Wallet](https://plugwallet.ooo/)
- [Plug](https://plugwallet.ooo/)
- [AstroX ME](https://astrox.me)
- [Infinity Wallet](https://chrome.google.com/webstore/detail/infinity-wallet/jnldfbidonfeldmalbflbmlebbipcnle)
- [NFID](https://nfid.one)



## Packages
| package | description |
| ----------- | ----------- |
| [@connect2ic/core]() | Client, connectors, assets and utilities |
| [@connect2ic/react]() | React components & hooks |
| [@connect2ic/vue]() | Vue components & composables |
| [@connect2ic/svelte]() | Svelte components & stores |

# React

Following these steps will give you fully working auth with a `<ConnectButton />` and `<ConnectDialog />` as shown in the top image.

**1.** Install the necessary packages

```
npm i -S @connect2ic/core @connect2ic/react
```


**2.** Wrap your app with the Provider and optionally pass in canister definitions (as generated by dfx)

```jsx
import { defaultProviders } from "@connect2ic/core/providers"
import { createClient } from "@connect2ic/core"
import { Connect2ICProvider } from "@connect2ic/react"
import "@connect2ic/core/style.css"
import * as counter from "canisters/counter"

const client = createClient({
  canisters: {
    counter,
  },
  providers: defaultProviders,
})

const AppRoot = () => (
  <Connect2ICProvider client={client}>
    <App />
  </Connect2ICProvider>
)

```

**3.** Place the components

```jsx
import { ConnectButton, ConnectDialog, Connect2ICProvider, useConnect } from "@connect2ic/react"

function App() {
  
  const { isConnected, principal, activeProvider } = useConnect({
    onConnect: () => {
      // Signed in
    },
    onDisconnect: () => {
      // Signed out
    }
  })

  return (
    <>
      <ConnectButton />
      <ConnectDialog dark={false} />
    </>
  )
}

```

**4.** Done

<img height=340 src="https://i.imgur.com/aGREctC.png" />


# Vue

Following these steps will give you fully working auth with a `<ConnectButton />` and `<ConnectDialog />` as shown in the top image.

**1.** Install the necessary packages
```
npm i -S @connect2ic/core @connect2ic/vue
```

**2.** Wrap your app with the Provider and optionally pass in canister definitions (as generated by dfx)

```html

<script setup>
  import { createClient } from "@connect2ic/core"
  import { defaultProviders } from "@connect2ic/core/providers"
  import { Connect2ICProvider } from "@connect2ic/vue"
  import "@connect2ic/core/style.css"
  import * as counter from "canisters/counter"
  
  const client = createClient({
    canisters: {
      counter,
    },
    providers: defaultProviders,
  })
</script>

<template>
  <Connect2ICProvider :client="client">
    <App />
  </Connect2ICProvider>
</template>

```

**3.** Place the components

```html

<script setup>
  import { ConnectButton, ConnectDialog, useConnect } from "@connect2ic/vue"

  const { isConnected, principal, activeProvider } = useConnect({
    onConnect: () => {
      // Signed in
    },
    onDisconnect: () => {
      // Signed out
    }
  })
</script>

<template>
  <div class="my-app">
    <ConnectButton />
    <ConnectDialog />
  </div>
</template>

```

**4.** Done

<img height=340 src="https://i.imgur.com/aGREctC.png" />

## Svelte

Following these steps will give you fully working auth with a `<ConnectButton />` and `<ConnectDialog />` as shown in the top image.

**1.** Install the necessary packages
```
npm i -S @connect2ic/core @connect2ic/svelte
```

**2.** Wrap your app with the Provider and optionally pass in canister definitions (as generated by dfx)

```html
<script>
  import { createClient } from "@connect2ic/core"
  import { defaultProviders } from "@connect2ic/core/providers"
  import { Connect2ICProvider } from "@connect2ic/svelte"
  import "@connect2ic/core/style.css"
  import * as counter from "canisters/counter"

  const client = createClient({
    canisters: {
      counter,
    },
    providers: defaultProviders,
  })
</script>

<Connect2ICProvider client={client}>
  <App />
</Connect2ICProvider>
```

**3.** Place the components

```html
<script>
  import { ConnectButton, ConnectDialog, useConnect } from "@connect2ic/svelte"
  
  const { isConnected, principal, activeProvider } = useConnect({
    onConnect: () => {
      // Signed in
    },
    onDisconnect: () => {
      // Signed out
    }
  })
</script>

<div class="my-app">
  <ConnectButton />
  <ConnectDialog />
</div>
```

**4.** Done

<img height=340 src="https://i.imgur.com/aGREctC.png" />


# How to publish a new package
1. Update the Version
Goto packages/core/package.json, bumping the version.

2. Build the Package
`connect2ic>npm run build`
3. For instance, if updating the "core" package, open packages/core/package.json.
Change the "name" field to "@connect2icmodclub/core" to publish under the correct scope.
5. Goto package.json, change "private" to false.
6. Run publish
`connect2ic/packages/core> npm publish`
Upon successful publication, you should see messages similar to the following:
```npm notice === Tarball Details === 
npm notice name:          @connect2icmodclub/core                 
npm notice version:       0.0.3                                   
npm notice filename:      connect2icmodclub-core-0.0.3.tgz        
npm notice package size:  796.2 kB                                
npm notice unpacked size: 1.5 MB                                  
npm notice shasum:        6a570e6388fd5c311886722d84f3cb03d42ce8ae
npm notice integrity:     sha512-aekjpj+tEfuLA[...]ANQ3rEWQWfCpA==
npm notice total files:   79                                      
npm notice 
npm notice Publishing to https://registry.npmjs.org/ with tag latest and default access
+ @connect2icmodclub/core@0.0.3
```

## Notes
This observation may need attention in the future. Renaming to @connect2icmodclub/core leads to build failures (lots of errors observed). Building must be done with @connect2/core, and publishing with @connect2icmodclub/core. (Clean-up tasks may be necessary.)







