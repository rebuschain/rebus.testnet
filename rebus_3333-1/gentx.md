# Submitting your GenTx for the Rebus Incentivized Testnet

Thank you for becoming a genesis validator on Rebus! This guide will provide instructions on setting up a node, submitting a gentx, and other tasks needed to participate in the launch of the Rebus v1 incentivized testnet.

A `gentx` does three things:

- Registers the validator account you created as a validator operator account (i.e. the account that controls the validator).
- Self-delegates the provided amount of staking tokens.
- Links the operator account with a Tendermint node pubkey that will be used for signing blocks. If no `--pubkey` flag is provided, it defaults to the local node pubkey created via the `rebusd init` command.

## Setup

Software:

- Go version: [v1.18+](https://golang.org/dl/)
- Rebus version: [v0.0.2](https://github.com/rebuschain/rebus.core/tree/v0.0.2)

To verify that Go is installed:

```sh
go version
# Should return go version go1.18 linux/amd64
```

## Instruction (Until July 27, 2022 24:00 EST)

The following instructions are written targeting an Ubuntu 18.04 system. If you are running a different OS/architecture, make sure to apply the necessary changes.

1. Install `rebusd`

    ```bash
    git clone https://github.com/rebuschain/rebus.core.git 
    cd rebus.core && git checkout testnet
    make install
    ```

    Make sure to checkout to testnet or tags/v0.0.2

    Verify that everything is OK. If you get something like the following, you've successfully installed Rebus on your system.

    ```sh
    rebusd version --long
    
    name: rebus
    server_name: rebusd
    version: testnet.4549a90ec0273ea108fd93d424dd40b25d76bbcb
    commit: 4549a90ec0273ea108fd93d424dd40b25d76bbcb
    build_tags: netgo,ledger
    go: go version go1.18.3 linux/amd64
    ```

2. Initialize the `rebusd` directories and create the local file with the correct chain-id

    ```bash
    rebusd init <moniker> --chain-id=reb_3333-1
    ```

3. Create a local key pair in the keybase

    This will use the os default keychain

    ```bash
    rebusd keys add <your key name> --coin-type 118 —-algo secp256k1
    ```

    Make sure to keep the mnemonic seed that is needed to receive rewards at the time of the mainnet launch.

    Import key from ledger Nano s/x

    ```bash
    rebusd keys add <your key name> –-ledger —-coin-type 118 —-algo secp256k1
    ```

4. Add the account to your local genesis file with a given amount and key you just created.

    ```bash
    rebusd add-genesis-account $(rebusd keys show <your key name> -a) 100rebus
    ```

    Make sure to use the `rebus` denom.

5. Create the gentx

   ```bash
    rebusd gentx <your key name> 100000000000000000000arebus \
    --chain-id=reb_3333-1 \
    --moniker=psval1 \
    --details="my details" \
    --commission-rate=0.05 \
    --commission-max-rate=0.2 \
    --commission-max-change-rate=0.01 \
    --pubkey $(rebusd tendermint show-validator) \
    --identity="<Keybase.io GPG Public Key>"
    ```

    Make sure to use `arebus` denom.

6. Create Pull Request to the [testnet](https://github.com/rebuschain/rebus.testnet) repository with the file `rebus_3333-1/gentxs/<your validator moniker>.json`. To be a valid submission, you need the .json file extension and no whitespace or special characters in your filename. Your PR should be one addition.