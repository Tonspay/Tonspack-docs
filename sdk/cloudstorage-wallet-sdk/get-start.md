---
description: How to use it
---

# Get Start

### Getting Started

1. **Install the SDK**: Install either the HD Wallet SDK or the Cloud Storage Wallet SDK, depending on your use case.
2. **Generate Keypairs**: Use the HD Wallet SDK to generate multichain keypairs or the Cloud Storage Wallet SDK for fully non-custodial wallet management.
3. **Build dApps**: Use the SDK’s simple API to integrate wallet functionality into your Telegram webapps, allowing users to manage crypto assets seamlessly across multiple chains.

## How to use it ?

Install the package

```
pnpm i @tonsprotocol/telegram-cloudstorage-wallet

```

Now try use it in your font-end

```
import CloudStorageWallet from "@tonsprotocol/telegram-cloudstorage-wallet" 

await CloudStorageWallet.init("mywallet")
```
