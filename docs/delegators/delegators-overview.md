# Delegators Overview



## Introduction

OKChain是基于Tendermint，它依赖于一组负责提交区块validators。These validators participate in the consensus protocol by broadcasting votes which contain cryptographic signatures signed by each validator's private key.

令牌持有者可以通过“委托”命令获得选票，选出自己认为对于生态有意义的validators，对于这些令牌持有者称之为delegator。

For a practical guide on how to become a delegator, click [here](./delegator-guide-cli.md).



## Voting Mechanics

In OKChain, any user who has staked OKT tokens can vote. Each user is allowed to vote for up to 30 validator candidates using the full weight of their stake. For example, if a user has 1000 OKT staked, she can cast 1000 votes each for up to 30 validators. The top 21 validator candidates by total number of votes received form the core set of validators. Additional validators, ranked by total votes, are also compensated by the network to serve as validator candidates.

OKChain is a liquid, delegative democracy. Users have the option of voting directly for validator, but they can also delegate their voting power to another account to vote on their behalf. The delegate account, called a proxy, has no control over the original user’s account — the user can proxy her vote trustlessly without handing over any keys. The proxy simply has the power to direct that user’s voting power towards certain validators, but the user can revoke her voting power from the proxy at any point.


## Key Management 
The best way to minimize the risk of theft or loss of OKT is to have a strong storage and backup strategy for your private keys.  The safest way to store your keys is offline,  either in a cryptocurrency wallet or on a device that you never connect to the internet. The best backup strategy for your k yes is to ensure that you have multiple copies of them stored in safe places, and to take specific measures to protect at least one copy of your keys from any kind of natural disaster that is a likely possibility in your part of the world. 

**To protect your OKT, do not share your 12 words with anyone.** The only person who should ever need to know them is you. You do not need to share your private keys if you're delegating OKT to a validator on the network or to use custodial services. If anyone asks for your key material, 


## Software Vulnerabilities
To protect yourself and ensure you're using the safest code is to use the latest version of software available, and to update immediately (or as soon as you can) after a security advisory is released. This is important for your laptops, mobile devices, cryptocurrency wallets, and anything else that may be linked to your identity or your cryptocurrency. 

*To protect your OKT, you should only download software directly from official sources, and make sure that you're always using the latest, most secure version of `okchaincli` when you're doing anything that involves your 12 words*. The latest versions of `Tendermint`, the `OKChain-SDK`, and `okchaincli` will always be available from our official Github repositories.

No one from OKChain, the Tendermint team or the Interchain Foundation will ever send an email that asks for you to download a software attachment  after sending out a security advisory or making a patch available. 


## Verifying Transactions
Be skeptical of technical advice, especially advice that comes from people you do not know in forums and on group chat channels. Familiarize yourself with important commands, especially those that will help you carry out high-risk actions, and consult our official documentation to make sure that you're not being tricked into doing something that will harm you or your validator. 

**When sending transactions or doing anything that may spend coins, you should always verify those transactions before hitting send**. While address strings are long, it is important to visually comparing them in blocks of 4 characters at a time to ensure that you are sending them to the right place rather than into oblivion. 

## Account Security
One of the most important things  you can do to protect your cryptocurrency and eliminate risk is to harden all of your critical online accounts. Attackers will try to gain foothold wherever they can, and will use that foothold to pivot from one place to another. Unprotected accounts like email, social media, your Github account, the OKChain Forum and anything in between could give an attacker an opportunities to gain foothold in your online life. 

For people who hold cryptocurrency, there are two specific account  security actions that can be taken to eliminate specific risks that come with being part of the blockchain world. 

*  First, it is important to enable 2-factor authentication everywhere you can, and to make sure that you are using a code generator or [U2F hardware key](https://en.wikipedia.org/wiki/Universal_2nd_Factor) as a second factor. 

* Second,  be mindful of account recovery methods used to regain access to your most important accounts and make sure that you do not use SMS as a recovery method. If you haven't done so yet, start using an authenticator app or a hardware key immediately for your personal email account and wherever else you manage your tokens, especially if you use online exchanges.


## Supply Chain Attacks
Whether you're buying a hardware or a hardware wallet, it is important  to purchase whatever you need directly from the supplier or from a trusted source. This is the only way to completely eliminate the risk of a compromised device or chip from stealing your private keys, especially since there are reports of compromised wallets being sold on Amazon and through other popular online marketplaces. 

## Disclaimer

Please note that this is highly experimental software. In these early days, we can expect to have issues, updates, and bugs. The existing tools require advanced technical skills and involve risks which are outside of the control of the Interchain Foundation and/or the Tendermint team (see also the risk section in the Interchain OKChain Contribution Terms). Any use of this open source Apache 2.0 licensed software is done at your own risk and on a "AS IS" basis, without warranties or conditions of any kind, and any and all liability of the Interchain Foundation and/or the Tendermint team for damages arising in connection to the software is excluded. Please exercise extreme caution!`