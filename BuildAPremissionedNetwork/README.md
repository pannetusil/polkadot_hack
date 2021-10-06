# Build a permissioned network - https://substrate.dev/docs/en/tutorials/build-permission-network/
# Add node-authorization pallet
`git clone -b latest --depth 1 https://github.com/substrate-developer-hub/substrate-node-template`
# From the working directory, create a new branch and check it out
`cd substrate-node-template`
`git branch perm-network`
`git checkout perm-network`

Building takes ages!

When started to modify, it was clear where to copy the code. However, there was a challenge with the tag value for dependencies.pallet-node-authorization -> check it corresponds to the same monthly version as other packages, otherwise it will end up in an error. Besides that, the instruction were clear.


# Launch our permissioned network
Finally, after building everything the final step was to start the individual nodes - Alice, Bob, Charlie, and Dave.

Alice: `./target/release/node-template --chain=local --base-path /tmp/validator1 --alice --node-key=c12b6d18942f5ee8528c8e2baf4e147b5c5c18710926ea492d09cbd9f6c9f82a --port 30333 --ws-port 9944`
Bob: `./target/release/node-template --chain=local --base-path /tmp/validator2 --bob --node-key=6ce3be907dbcabf20a9a5a60a712b4256a54196000a8ed4050d352bc113f8c58 --port 30334 --ws-port 9945`
Charlie: `./target/release/node-template --chain=local --base-path /tmp/validator3 --name charlie  --node-key=3a9d5b35b9fb4c42aafadeca046f6bf56107bd2579687f069b42646684b94d9e --port 30335 --ws-port=9946 --offchain-worker always`
Dave: `./target/release/node-template --chain=local --base-path /tmp/validator4 --name dave --node-key=a99331ff4f0e0a0434a6263da0a5823ea3afcfffe590c9f3014e6cf620f2b19a --port 30336 --ws-port 9947 --offchain-worker always`

We could see the list of well known nodes in the system. To add Charlie we need to execute the sudo command and add him. ![Adding Charlie](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut3_addingSudo.PNG)

To segment the nodes, we can specify that a node can only conect to a single node, this time Dave connects to Charlie. ![Claim Node](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut3_claimNode.PNG)
They both have to be interconneceted, but Dave has only Dave and is connected to him. ![Chaining Dave](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut3_catchingup.PNG)