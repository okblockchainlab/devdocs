<!--
order: 4
-->

# Join the Public Testnet 

::: tip Current Testnet
See the [testnet repo](https://github.com/okex/testnets) for
information on the latest testnet, including the correct version
of OKChain to use and details about the genesis file.
:::

::: warning
**You need to [install okchain](./install-okchain.html) before you go further**
:::

## Starting a New Node

> NOTE: If you ran a full node on a previous testnet, please skip to [Upgrading From Previous Testnet](#upgrading-from-previous-testnet).

To start a new node, the mainnet instructions apply:

- [Join the mainnet](./join-okchain-mainnet.html)
- [Deploy a validator](../validators/validators-guide-cli.html)

The only difference is the OKChain version and genesis file. See the [testnet repo](https://github.com/okex/testnets) for information on testnets, including the correct version of the OKChain to use and details about the genesis file.

## Upgrading Your Node

These instructions are for full nodes that have ran on previous versions of and would like to upgrade to the latest testnet.

### Reset Data

First, remove the outdated files and reset the data.

```bash
rm $HOME/.okchaind/config/addrbook.json $HOME/.okchaind/config/genesis.json
okchaind unsafe-reset-all
```

Your node is now in a pristine state while keeping the original `priv_validator.json` and `config.toml`. If you had any sentry nodes or full nodes setup before,
your node will still try to connect to them, but may fail if they haven't also
been upgraded.

::: danger Warning
Make sure that every node has a unique `priv_validator.json`. Do not copy the `priv_validator.json` from an old node to multiple new nodes. Running two nodes with the same `priv_validator.json` will cause you to double sign.
:::

### Software Upgrade

Now it is time to upgrade the software:

```bash
git clone https://github.com/okex/okchain.git
cd okchain
git fetch --all && git checkout master
make install
```

::: tip
_NOTE_: If you have issues at this step, please check that you have the latest stable version of GO installed.
:::

Note we use `master` here since it contains the latest stable release.
See the [testnet repo](https://github.com/okex/testnets) for details on which version is needed for which testnet, and the [OKChain release page](https://github.com/okex/okchain/releases) for details on each release.

Your full node has been cleanly upgraded!
