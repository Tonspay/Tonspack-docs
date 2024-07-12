---
description: How tonspack wallet works ?
---

# 👻 How it works ?

Tonspack is a telegram base mulity chains support wallet .&#x20;

Auth user base on `telegram-webapp-initdata` and `telegram-BiometricManager` .

## How Tonspack work ?&#x20;

There are 2 cores of Tonspack wallet . Works like `@wallet` and `@Tonspace`

1. Centralized Tonspack wallet
2. Decentralized Spacepack wallet&#x20;

### How Centralized Tonspack wallet works ?&#x20;

The centralized part Tonspack wallet , work base on restful-api .&#x20;

Every user login via [Tonspack-telegram-miniapp](https://t.me/tonspack\_bot/app) . Will auto auth base on `telegram-webapp-initdata` , and access to keypair generate base on `BIP44`  using user's telegramID.

#### Example code how it works base on BIP44

```javascript
function getKp(uid)
{
    var row = Math.ceil(uid/process.env.WLLET_HD_MAX)
    var subRow = Math.ceil(uid%process.env.WLLET_HD_MAX)
    var kp = nacl.sign.keyPair.fromSecretKey(
        b58.decode(process.env.WLLET_SK)
    )
    const master = hd.hdkey.fromMasterSeed(kp.publicKey);
    const subKp = nacl.sign.keyPair.fromSeed(
        (
            (
                master.deriveChild(row)
            ).getWallet()
        ).getPrivateKey()
    );
    const subMaster = hd.hdkey.fromMasterSeed(subKp.publicKey);
    var evm = subMaster.deriveChild(subRow)
    var evmWallet = evm.getWallet()
    var evmKp = {
        address : evmWallet.getAddressString(),
        privateKey : evmWallet.getPrivateKeyString()
    }
    var naclKp = nacl.sign.keyPair.fromSeed(evmWallet.getPrivateKey())
    var solKp = {
        address : b58.encode(naclKp.publicKey),
        privateKey :b58.encode(naclKp.secretKey),
    }
    var tonKp = ton.getTonWalletV4KeyPair(naclKp.secretKey,0)
    return {
        naclKp : naclKp,
        evmKp : evmKp,
        solKp : solKp,
        tonKp : tonKp
    }
}
```

All the keypair of users can be locate base on it's telegramID . And generate by `BIP44`

### How decentralized Spacepack wallet work ?

The Spacepack is a MPC wallet base on `telegram-webapp-initdata` and `telegram-BiometricManager` .

Currently the MPC solution provider is [litprotocol](https://www.litprotocol.com/) .

And the Spacepack wallet is currently building .&#x20;
