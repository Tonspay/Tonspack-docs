---
description: How tonspack wallet works ?
---

# 👻 How it works ?

Tonspack is a telegram base mulity chains support wallet .&#x20;

Auth user base on `telegram-webapp-initdata` and `telegram-BiometricManager` .

## How Tonspack work ?&#x20;

The core of Tonspack wallet is Web3auth base telegram webapp initData MPC . Details of MPC part can be found [here](developer/mpc-part.md) .

### Tonspack working flow&#x20;

* Login telegram webapp
* Auth telegram webapp initData into [Tonspack-mpc-auth-middleware ](https://github.com/Tonspay/Tonspack-Web3auth-Telegram-Webapp-MPC-Middleware). Generate JWT token.
* Redirect JWT token into Tonspack wallet font-end .&#x20;
* Tonspack wallet font-end request Web3auth for it's privateKey part .  And culcuate the privateKey in local font-end .
* Using BIP-44 to generate the different keypair for chains in local font-end .
* Do follow connect/sign message/send transaction in font-end .&#x20;

### How Tonspack using Bip-44 works ?&#x20;

#### Example code how it works base on BIP44

```javascript
function getKp(sk:string)
{
    const master = hd.hdkey.fromMasterSeed(Buffer.from(sk,'hex'));
    const derive = master.deriveChild(derivePath)
    const evmWallet = derive.getWallet()
    const naclKp = nacl.sign.keyPair.fromSeed(evmWallet.getPrivateKey())
    
    return {
        naclKp : naclKp,
        evmKp :  {
            address : evmWallet.getAddressString(),
            privateKey : evmWallet.getPrivateKeyString()
        },
        solKp : {
            address : bs58.encode(naclKp.publicKey),
            privateKey :bs58.encode(naclKp.secretKey),
        },
        tonKp : ton.getTonWalletV4KeyPair(
            Buffer.from(naclKp.secretKey),0),
        btcKp : btc.getKeyPair(
            Buffer.from(evmWallet.getPrivateKey())
        )

    } as objKP
```

The init sk comes from Web3auth SDK generate .&#x20;

And it can generate different keypair by BIP-44 rules .&#x20;

