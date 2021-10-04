# Setup up your computer
Starting wih cloning the repo: `git clone -b latest --depth 1 https://github.com/substrate-developer-hub/substrate-node-template`

Navigate to the repo `cd substrate-node-template`

However, before starting the build, I had to make sure I have the proper rustup version of nightly, otherwise it would crash --> https://substrate.dev/docs/en/knowledgebase/getting-started/

Then, finally hit the build and wait `cargo build --release`

While waiting for the backend, I installed additional requirements for the frontend - Node.js (LTS 14.18.x) https://nodejs.org/en/download/package-manager/ and Yarn npm install yarn `npm i yarn`

After dependencies were install, I got the repo:
* Repo `git clone -b latest --depth 1 https://github.com/substrate-developer-hub/substrate-front-end-template`
* Navigate `cd substrate-front-end-template`
* Install `yarn install`


# Background information
It provides an overview of other chans and how Subtrate fits into it - cool!

# Interacting with your node

To Run a temporary node in development mode `./target/release/node-template --dev --tmp`

Now, just missing is the frontend `yarn start`


![It works](figs/Tut1_running.png)

