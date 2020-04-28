<!--
order: 1
-->

# What is OKChain?

`okchain` is the name of the OKChain SDK application for the OKChain. It comes with 2 main entrypoints:

- `okchaind`: The OKChain Daemon, runs a full-node of the `okchain` application.
- `okchaincli`: The OKChain command-line interface, which enables interaction with a OKChain full-node.

`okchain` is built on the OKChain SDK using the following modules:

- `x/auth`: Accounts and signatures.
- `x/bank`: Token transfers.
- `x/staking`: Staking logic.
- `x/mint`: Inflation logic.
- `x/distribution`: Fee distribution logic.
- `x/slashing`: Slashing logic.
- `x/gov`: Governance logic.
- `x/ibc`: Inter-blockchain transfers.
- `x/params`: Handles app-level parameters.

About the OKChain: The OKChain is the first Hub to be launched in the OKChain Network. The role of a Hub is to facilitate transfers between blockchains. If a blockchain connects to a Hub via IBC, it automatically gains access to all the other blockchains that are connected to it. The OKChain is a public Proof-of-Stake chain. Its staking token is called the okt.

Next, learn how to [install OKChain](./installation.md).
