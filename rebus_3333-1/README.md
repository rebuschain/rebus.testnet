# Rebus v1 Testnet

## Instructions Updated

### Genesis Validators

Update the rebus.core pulling the latest code 

```bash
git clone https://github.com/rebuschain/rebus.core.git 
cd rebus.core && git checkout testnet
make install
```

## Validators files

Remeber to use your previous validator keys used to generate your gentx, these are in the ~/.rebusd/config where you ran rebusd:
```
node_key.json
priv_validator_key.json
```


## Init the data folder and configure the Chain ID 

```
rebusd init <your-moniker> --chain-id reb_3333-1
```
 
## Genesis File

You can download the genesis file for the chain with all the gentxs submitted and accepted and the intial chain state.

```
curl https://raw.githubusercontent.com/rebuschain/rebus.testnet/master/rebus_3333-1/genesis.json > ~/.rebusd/config/genesis.json
```

We recommend using sha256sum to check the hash of the genesis.

Linux
```
cd ~/.rebusd/config
echo "d382339b5187693ef2e57ff4f33c571ee9bb238ce9fcd68ca99c02116576c41b  genesis.json" | sha256sum -c
```
MacOS
```
cd ~/.rebusd/config
echo "d382339b5187693ef2e57ff4f33c571ee9bb238ce9fcd68ca99c02116576c41b  genesis.json" | shasum -a 256 -c
```

The correct genesis file is in the https://github.com/rebuschain/rebus.testnet/tree/master/rebus_3333-1 folder

## Reset Chain Database

There shouldn't be any chain database yet, but in case there is for some reason, you should reset it. This is a good idea especially if you ran rebusd start on a broken genesis file. 

rebusd unsafe-reset-all


## Seed 

The file seeds contains the Rebus id/ip nodes.


## Details

- Network Chain ID: `reb_3333-1`
- EIP155 Chain ID: `3333`
- rebusd version: `v0.0.3`
