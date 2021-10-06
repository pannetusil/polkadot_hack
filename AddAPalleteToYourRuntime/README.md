# Link - https://substrate.dev/docs/en/tutorials/add-a-pallet/import-a-pallet
The focus is on adding Nicks pallet to the runtime. I used the CreateFirstSubstrateChain tutorial as a base for next action, we already have the repo.


I did not include the `serde`package which causes issues and change the `tag` in the pallet-nicks dependencies to proper monthly version, in our case `2021-10`. Fortunately, afterwards the node builds well, but takes a bit of time.

Once running the compiled node with the frontend, I could start to interact with it.

I could see nicks in the pallet interactor, where I could set a name as I wanted. ![setName](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut4_devsRock.PNG)

Based on the generated event I could get the AccountId which I could later on query for. ![query](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut4_query.PNG)

Following with the `killName` action, which worked only once. When I tried to kill it again, I got an Error message. 

Overall, it was good learning. Next plan is to publish my own Pallet.

# my own pallet 
[dependencies.my-first-pallet]
default_features = false
git = 'https://github.com/pannetusil/polkadot_hack/test-pallet'
