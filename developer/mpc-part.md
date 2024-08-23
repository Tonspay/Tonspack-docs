---
description: MPC part of Tonspack wallet
---

# MPC part

## What is MPC ?&#x20;

Multi-Party Computation (MPC) forms the backbone of Web3Auth's advanced wallet infrastructure, offering a secure and non-custodial way to manage digital assets.

[What is Web3auth MPC](https://web3auth.io/mpc?gad\_source=1\&gclid=CjwKCAjw5qC2BhB8EiwAvqa41oInVmjXQSlsJmDivbz2frx7YXp\_5Qd\_nEW1GhsBlzuGCzwzcwJ9DBoCL9YQAvD\_BwE) ?

## How tospack MPC work  ?

Currently , the MPC solution using [Web3auth JWT](https://github.com/Tonspay/Tonspack-Web3auth-Telegram-Webapp-MPC) . Which means the privateKey of users wallet being split into 2 different part .&#x20;

Part 1 : User's telegram auth account information .

Part 2 : Web3auth JWT serivce storage .

So Tonspack wallet will not keep any part of your keypair .

The only thing we do is :

1. Doing telegram webapp auth during user open Tonspack wallet Dapp . The auth-middleware is open source in our github-repo: [https://github.com/Tonspay/Tonspack-Web3auth-Telegram-Webapp-MPC-Middleware](https://github.com/Tonspay/Tonspack-Web3auth-Telegram-Webapp-MPC-Middleware)
2. The keypair generate rules . Using web3auth generate JWT keypair to generate sub keypair using Bip44 rules .&#x20;
3.  Wonderful font-end with action handel . So all the actions including :&#x20;

    1. Connect wallet
    2. Sign message
    3. Send out transaction

    Happened in your webapp font-end .
