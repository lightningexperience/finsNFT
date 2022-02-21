This is has sample code to explore blockchain & especially NFT concepts using a local blockchain development environment.

## What this dApp does
There are two main operations that happen in this dApp (decentralized app) powered by two contracts:
* Mint (i.e.generate) an NFT
* Allows you to offer your newly minted NFT

## How I deployed this dApp

### Prerequisites
* Install node
* Install Ganache cli - local blockchain environment for development (the ganache GUI never worked for me unfortunately)
* Install MetaMask - blockchain wallet which installs as a plugin to firefox, chrome or ios.
* Create an account in MetaMask and note the secret recovery phrase
* Install Truffle - (npm install -g truffle)  - Truffle is a great framework for building dApps including compiling contracts and deploying Contracts.
* Install an IDE - I personally use Atom as it is integrated with GitHub  - the official Ethereum IDE is Remix which has not proved to be very happy tool for me.


### Deploying locally
The project contains untested code only for understanding blockchain and NFT related concepts. It has not been tested as a safe code either for local or for remote deployment.

The steps I followed:

* git  clone - clone this repo locally
* cd to the repo directory and do 'npm install' - this  downloads all the necessary dependencies
* compile the smart contracts by running the following command in your terminal: truffle compile
* run ganache
* Ensure that truffle-config.js has the correct ganache port
* run tests that validate your solution can be executed truffle test
* deploy the contracts on your Ganache local blockchain by running the following command: truffle migrate
* assuming that we have MetaMask installed as  a browser extension, click on metamask icon in the brower toolbar and you will see that it automatically picks up the localhost:8545 wich is the ganache blockchain network. If it doesn't then you need to configure it explicitly in the MetaMask network configuration panel/
* now in the git repo directory open the UI by typing: npm start

It will spin up a browser tab at 127.0.0.1:3000 and bring up the UI for the dApp.

### Deployment on public blockchain
To deploy this dApp on a public blockchain two things  need to be done.
* deploy the UI of the dApp on a host (e.g., Heroku)
* deploy the smart contracts on Ethereum. Here we have several options as follows:
    * deploy on ethereum mainnet - this is very expensive and requires real dollars :) as I understand around a few hundred
    * deploy on one of the  etherum testnets such as ropsten
    * deploy on a layer to blockchain network like Polygon which works as a secondary scaling solution on top of ethereum. Additionally Polygon uses a different logic called 'proof of stake' instead of 'proof of work' that would be used if directly deploying on etherum. Using Proof of stake to resolve transactions requires less compute power and so is said to be climate friendly.
    * deploy on one of the blockchain node providers like Infura, Alchemy or Moralis. This last option is the easiest lowest cost (free) way of getting on etherium network. All these node providers also have libraries to make coding easier - e.g., I found it easier to use Alechemy Web3 library than directly coding web3.js to connect to Solidity (Ethereum language which is used to write smart contracts)

To deploy the contracts on public blockchain network we need to specify the following variables (if hosting locally then we can use .env file; if hosting on a server such as Heroku then the config variables feature should be used to prevent exposing values) .

* PRIVATE_KEYS --> Private Key of the account you are using to deploy (typically the first one in the list of Ganache)
* INFURA_API_KEY --> API key from the node provider (e.g., Infura when we register)

After this we need to get some free ether to deploy on testnet. This is needed even if you use alchemy or infura or moralis. We can request free ether by going to a faucet - an Ethereum Faucet is where we are paid a minuscule amount of ETH with basic ad viewing and clicking. This gets deposited in your MetaMask account and then with this account we can connect to an ethereum testnet either directly or via a node provider that we have mentioned above.

Then we need to run the truffle migrate to migrate to the testnet e.g. ropsten: truffle migrate --network ropsten



## Technology stack

- Smart Contract: contains all the logic e.g., to mint NFT, create  offer.
- Solidity: Solidity is an object-oriented, high-level language for implementing smart contracts. Somewhat similar to both JS and Java
- React.js
- Truffle: We discussed this above.
- Web3.js: The set of libraries that  are used to interact with a local or remote ethereum node. The glue between front end of the dApp and the Smart Contracts written in Solidity programs
- Ganache
- Node.js
- Metamask
- IPFS: Inter Planetary File System - When we mint or create a NFT, the state and the logic (Smart Contract) gets stored in the blocks - but a distributed filesystem is needed to store the related media and this is what IPFS provides. Pinata is one of the easy frameworks to integrate IPFS in our dApp.

- React.js front-end UI a

### Project architecture

<img src="./img/architecture.PNG" alt="architecture">

The user can access the application via web-browser, and he must have the Metamask wallet installed. This interface, built with React.js, relies on the web3.js library to communicate with the smart contracts through Metamask. This means that the data reflected on the front-end application is fetched from the Ethereum blockchain. Each action performed by the user (mint a NFT, offer NFT, buy NFT...) creates a transaction on Ethereum, which will require Metamask confirmation and pay a small fee, and this transaction will permanently modify the state of the NFTCollection and NFTMarketplace smart contracts. On top of it, the user will upload the NFT Metadata to the IPFS, creating a permanent hash which will be permanently recorded on the blockchain itself to prove ownership.

### NFT Marketplace features


The user can perform the following actions on this NFT Marketplace:

#### Mint

The user must input a name, description and upload a file (image) to mint his own NFT. Once minted, a representation of this NFT will be displayed in the marketplace and initially it will be owned by its creator. This is open for everyone, meaning everyone can participate in this NFT creation within this collection.

#### Make Offer

The user can offer his NFT by specifying its price (in Ether). If someone fulfills this offer, then the ownership is transferred to a new owner.

#### Cancel Offer

The user can cancel an offer he did in the past if in the end he does not want to sell his NFT or wants to adjust the price.
