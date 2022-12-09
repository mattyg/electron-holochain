# electron-holochain

**Built-in Holochain Version: [v0.0.175  November 29, 2022](https://github.com/holochain/holochain/blob/main/CHANGELOG.md#20221130011217)**

**Important: Expects an HAPP built with HDK [v0.0.163](https://docs.rs/hdk/0.0.163/hdk/index.html) and HDI [v0.1.10](https://docs.rs/hdi/0.1.10/hdi/index.html)**

manage holochain processes during an electron application runtime, using [holochain-runner binary](https://github.com/lightningrodlabs/holochain-runner).

```typescript
// function initAgent(
//   app: App,
//   opts: ElectronHolochainOptions,
//   pathOptions?: PathOptions
// ): Promise<{ statusEmitter: StatusUpdates, shutdown: () => Promise<void> }>

import {app} from 'electron'
import initAgent, {
  StateSignal,
  StatusUpdates,
  STATUS_EVENT,
  APP_PORT_EVENT,
  ElectronHolochainOptions,
  PathOptions
} from 'electron-holochain'

const runnerOptions: ElectronHolochainOptions = {
  happPath: 'pathtomyhapp.happ',
  keystorePath: string
  passphrase: string
  // datastorePath?: 'string' default: databases
  // appId?: string
  // appWsPort?: number
  // adminWsPort?: number
  // proxyUrl?: string
  // membraneProof?: string
  // bootstrapUrl?: string
  // networkSeed?: string
}

const { statusEmitter, shutdown } = await initAgent(app, runnerOptions)

// listen on the statusEmitter for status update
statusEmitter.on(STATUS_EVENT, (status: StateSignal) => {
  // do stuff
})

// listen on the statusEmitter for the websocket port used for app
statusEmitter.on(APP_PORT_EVENT, (appPort: string) => {
  // do stuff
}
// when the app quits, holochain-runner and lair-keystore will shut down automatically

// you can also call the following, to shut them down
await shutdown()
```
