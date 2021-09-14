Get started with CASPER by korrrba 



---
I order to complete the task, I installed all prerequisites and followed https://docs.casperlabs.io/en/latest/dapp-dev-guide/setup-of-rust-contract-sdk.html . All steps were done on Ubuntu 18.04 LTS. The steps are described above the screenshots.


## Creating and deploying a simple smart contract

A simple CASPER contract built:

![](https://i.imgur.com/w91hezm.png)

and tested:

![](https://i.imgur.com/jRFQzrG.png)

A local CASPER network spin-off using https://docs.casperlabs.io/en/latest/dapp-dev-guide/setup-nctl.html (10 nodes, 5 running):

![](https://i.imgur.com/ESfkP0z.png)

A local faucet account:

![](https://i.imgur.com/iUfxShp.png)

Deploying a simple contract to the local network:

![](https://i.imgur.com/RPOhujJ.png)


## A Counter Contract Tutorial

Followed the instructions described at https://docs.casperlabs.io/en/latest/dapp-dev-guide/tutorials/counter/walkthrough.html

First I cloned the example repository, analyzed the content, built the contracts and deployed to the local Casper network.

Viewing faucet account data

![](https://i.imgur.com/Pw0ZCC0.png)

Getting state root hash and querying the state

![](https://i.imgur.com/yjvqvAz.png)

Deploying the Counter contract and checking the state

![](https://i.imgur.com/lEd9LBd.png)

The counter is currently set to 1.

After incrementing the counter using counter-call, counter is set to 2.

![](https://i.imgur.com/JZ7tZkg.png)


## Demonstrating key management concepts by modifying the client in the Multi-Sig tutorial

I forked the example, deployed and ran the original example.
Then I implemented a managing lost or stolen keys scenario and pushed to https://github.com/gitcoindev/keys-manager

see the following commits

https://github.com/gitcoindev/keys-manager/commit/d82765ed9529ced4f8b78ea60c70ee1ae1df31e3

https://github.com/gitcoindev/keys-manager/commit/12fc50de08f4717c58c9810026827ea1ea1445c5

for the details.

The scenario in action:

```
[x] Current state of the account:
{
  _accountHash: 'account-hash-047192a9c1c58dd0c2fc35fc5b2804f72d8d5fcd35194ade527f400556bc32c0',
  namedKeys: [
    {
      name: 'keys_manager',
      key: 'hash-b26497fd813f230d20feba131aca591f4460937e3fded5059c1f7b348976ac8e'
    },
    {
      name: 'keys_manager_hash',
      key: 'uref-da6914fa8ceb9c4a89615152b0ba71e8cc01b98c0a1d73d2515b5f8a30fced75-007'
    }
  ],
  mainPurse: 'uref-72dc12f39678e9ca0f2f789eedfd3bcdc1d4da324854f849437d7ac9b92470d1-007',
  associatedKeys: [
    {
      accountHash: 'account-hash-047192a9c1c58dd0c2fc35fc5b2804f72d8d5fcd35194ade527f400556bc32c0',
      weight: 3
    },
    {
      accountHash: 'account-hash-2035554e2049817a5b325b101a96edf0786fddb376a8929245ea57f709c9c380',
      weight: 1
    },
    {
      accountHash: 'account-hash-ec97dab085c9715b0e305d5e5785ad053c7ae8affc209f88763535d0919fd6dc',
      weight: 1
    }
  ],
  actionThresholds: { deployment: 2, keyManagement: 3 }
}

Remove stolen mobile key by setting its weight to 0 and set thirdAccount key as a new mobile key
Signed by: account-hash-047192a9c1c58dd0c2fc35fc5b2804f72d8d5fcd35194ade527f400556bc32c0
Deploy hash: 8e951e4d3fe0bdbe77d68758ea3581f79ee650a25757f1d06d9e704568b91085
Deploy result:
{
  deploy: {
    hash: '8e951e4d3fe0bdbe77d68758ea3581f79ee650a25757f1d06d9e704568b91085',
    header: {
      account: '0202b6ad9fcd19cd2ef7684c778c21aa51fb610218b0a612c28b014e820e20f9d110',
      timestamp: '2021-09-13T22:29:39.844Z',
      ttl: '30m',
      gas_price: 1,
      body_hash: '28319e75306125be55fcd79cb1b79121faaa32c3275178ba07d0137425646a43',
      dependencies: [],
      chain_name: 'casper-net-1'
    },
    payment: { ModuleBytes: [Object] },
    session: { StoredContractByName: [Object] },
    approvals: [ [Object] ]
  }
}

[x] Current state of the account:
{
  _accountHash: 'account-hash-047192a9c1c58dd0c2fc35fc5b2804f72d8d5fcd35194ade527f400556bc32c0',
  namedKeys: [
    {
      name: 'keys_manager',
      key: 'hash-b26497fd813f230d20feba131aca591f4460937e3fded5059c1f7b348976ac8e'
    },
    {
      name: 'keys_manager_hash',
      key: 'uref-da6914fa8ceb9c4a89615152b0ba71e8cc01b98c0a1d73d2515b5f8a30fced75-007'
    }
  ],
  mainPurse: 'uref-72dc12f39678e9ca0f2f789eedfd3bcdc1d4da324854f849437d7ac9b92470d1-007',
  associatedKeys: [
    {
      accountHash: 'account-hash-047192a9c1c58dd0c2fc35fc5b2804f72d8d5fcd35194ade527f400556bc32c0',
      weight: 3
    },
    {
      accountHash: 'account-hash-137b239fdf0236528af9c2ee511e6eb5232f75e5ba7b25321edcba65867ec181',
      weight: 1
    },
    {
      accountHash: 'account-hash-2035554e2049817a5b325b101a96edf0786fddb376a8929245ea57f709c9c380',
      weight: 1
    }
  ],
  actionThresholds: { deployment: 2, keyManagement: 3 }
}

[x] Try to make transfer with a stolen key.
Signed by: account-hash-2035554e2049817a5b325b101a96edf0786fddb376a8929245ea57f709c9c380
Signed by: account-hash-ec97dab085c9715b0e305d5e5785ad053c7ae8affc209f88763535d0919fd6dc
Deploy hash: 29f3570c730f02529cc23df202cd9bf5b20ba3c9d9a3e7373d970862a7e34ea6
Deploy result:
(node:1848) UnhandledPromiseRejectionWarning: Error: Contract execution: Authorization failure: not authorized.

```

After the mobile key is stolen, it is removed from the account and a new key is set up. Trying to transfer funds using a stolen key results in `Authorization failure: not authorized` error.

## Demonstrating token transfers

I created a testnet account and requested funds:

https://testnet.cspr.live/account/012c9b5090e048b957981a4ed535f93e28e5b1af5b6779c31316fbda6008c88e59

The account received 1,000.00000 CSPR

Checking the balance on the command line

![](https://i.imgur.com/ceO72t7.png)

Direct token transfer 2.50000 CSPR to another account

![](https://i.imgur.com/cwiNVXP.png)


was successful, can be also verified on the account that received funds:

https://testnet.cspr.live/account/01991d6dd4772fb131fa5b879a860963c6fe8f7cfef7078e1f522367e3f4814642

## Demonstrating Delegate and Undelegate on the Casper Testnet

Delegating 12.50000 CSPR to validator 01c1eff500acd0814729019c0fdcc19821e319eaa10986ec1c3fef3ba996ca4654

![](https://i.imgur.com/T61Ebv3.png)

The delegation was successful.



The final step is to undelegate. I decided to undelegate 2.50000 CSPR and leave 10.00000 CSPR delegated.

![](https://i.imgur.com/xS3biVq.png)

Delegate / Undelegate process can be verified on the testnet account 

Delegating 12.50000 CSPR 

https://testnet.cspr.live/deploy/2fcb4d700f9e9b8444c21db7c74a75f8609bb1a490f5a46054568d4a62d56ade

Undelegating 2.50000 CSPR

https://testnet.cspr.live/deploy/17c4384a099707ce646b07ccb2b5c51cbbc8b0cc14982d48e1a0e8743877eaf0

---

This is the end of the Get Started With Casper task submission. Thank you for reviewing it!
