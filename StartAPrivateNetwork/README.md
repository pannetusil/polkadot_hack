# Start a private network - https://substrate.dev/docs/en/tutorials/start-a-private-network/
## Alice and Bob start Blockhain
We can base our work on the Tutorial 1 - Create first substrate chain. 

Starting with formatting of the previous chain, create a new directory, and then booting Alice.
```
./target/release/node-template \
  --base-path /tmp/alice \
  --chain local \
  --alice \
  --port 30333 \
  --ws-port 9945 \
  --rpc-port 9933 \
  --node-key 0000000000000000000000000000000000000000000000000000000000000001 \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --validator
```

Next, Bob can join following the same steps, just with a different configuration.
```
./target/release/node-template \
  --base-path /tmp/bob \
  --chain local \
  --bob \
  --port 30334 \
  --ws-port 9946 \
  --rpc-port 9934 \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --validator \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWEyoppNCUx8Yx66oV9fJnriXwCcXwDDUA2kj6vnc6iDEp
```

Whoray, Bob joined! 
![Bob joined for the first time](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut5_BobJoined.PNG)
## Generate own keys

For this step we firstly need to install the subkey utility.

`curl https://getsubstrate.io -sSf | bash -s -- --fast`
Install only `subkey`, at a specific version
`cargo install --force subkey --git https://github.com/paritytech/substrate --version 2.0.1 --locked`

We generate at least two keys of each type:
First:
`subkey generate --scheme sr25519` - execute twice
then inspect:
`subkey inspect --scheme ed25519 "<replace>"`  - execute twice with a given secret phrase

## Create custom chain spec
Now, with the generated keys, we can create a custom chain specification.

First, we need to export the old one and modify it.
```
      "aura": {
        "authorities": [
          "SR25519 PKSS58 - 1",
          "SR25519 PKSS58 - 2"
        ]
      },
      "grandpa": {
        "authorities": [
          [
            "EC25519 PKSS58 - 1", 1,
          ],
          [
            "EC25519 PKSS58 - 2", 1
          ]
        ]
      },
      "balances": {
        "balances": [
```
Next, we generate a raw config file which can be later on shared with the rest of the network.
Generete as follows:

`./target/release/node-template build-spec --chain=customSpec.json --raw --disable-default-bootnode > customSpecRaw.json`

Final step is to share the config file.

## Creating your private network

Similarly like before we purge the old chain and start with new nodes.

`./target/release/node-template purge-chain --base-path /tmp/node01 --chain local -y`
Node01
```
./target/release/node-template \
  --base-path /tmp/node01 \
  --chain ./customSpecRaw.json \
  --port 30333 \
  --ws-port 9945 \
  --rpc-port 9933 \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --validator \
  --rpc-methods Unsafe \
  --name MyNode01
```

Now, using `curl`, Polkadot-JS apps, or `key` command we add the key to a given key store.

I chose the Polkadot-JS, which fits the tutorial.
We see how the command can look like:
![Arua keystore insert](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut5_aruaKeyStore.PNG)
![Gran keystore insert](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut5_granKeyStore.PNG)

Node02
```
./target/release/node-template \
  --base-path /tmp/node02 \
  --chain ./customSpecRaw.json \
  --port 30334 \
  --ws-port 9946 \
  --rpc-port 9934 \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --validator \
  --rpc-methods Unsafe \
  --name MyNode02 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/<update to a given id>
```
Given id is visible on the boot of the node. It changes, so must be updated.
If everything goes well, you can see the node start to talk. ![Suceess](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut5_nodeEstablishCommunication.PNG)
This way it would proceed.

