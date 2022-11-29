# Voting-System-Block-Chain
Installing and Running Project
Clone Project

git clone git@github.com:sanattaori/techdot.git && cd techdot
Install Dependencies

npm install
Running Project

node index.js
If dependency problem occurs delete package.json, Run

npm init
Again Install dependencies and run project.

Running Project
Step 1 - Setting up Environment Instead of developing the app against the live Ethereum blockchain, we have used an in-memory blockchain (think of it as a blockchain simulator) called testrpc.

npm install ethereumjs-testrpc web3
Step 2 - Creating Voting Smart Contract

npm install solc
Replace your aadhaar no and phone number for running project at

techdot/ui/js/app.js

Line 39 in 7814403

 "<replace your aadhaar no here>": "<your phone number>", 
Step 3 - Testing in node console

Not required just for testing in node console- After writing our smart contract, we'll use Web3js to deploy our app and interact with it

$ node
> Web3 = require('web3')
> web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
Then ensure Web3js is initalized and can query all accounts on the blockchain

> web3.eth.accounts
Lastly, compile the contract by loading the code from Voting.sol in to a string variable and compiling it

> code = fs.readFileSync('Voting.sol').toString()
> solc = require('solc')
> compiledCode = solc.compile(code)
testrpc creates 10 test accounts to play with automatically. These accounts come preloaded with 100 (fake) ethers.

Deploy the contract!

dCode.contracts[‘:Voting’].bytecode: bytecode which will be deployed to the blockchain. compiledCode.contracts[‘:Voting’].interface: interface of the contract (called abi) which tells the contract user what methods are available in the contract.

> abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
> VotingContract = web3.eth.contract(abiDefinition)
> byteCode = compiledCode.contracts[':Voting'].bytecode
>deployedContract = VotingContract.new(['Sanat','Aniket','Mandar','Akshay'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
> deployedContract.address
> contractInstance = VotingContract.at(deployedContract.address)
deployedContract.address. When you have to interact with your contract, you need this deployed address and abi definition we talked about earlier.
Step 4 - Interacting with the Contract via the Nodejs Console

> contractInstance.totalVotesFor.call('Sanat').toLocaleString()
'2'
For TypeError: Cannot read property ':Voting' of undefined :
Make sure you have ganache-cli

sudo npm install ganache-cli -g
copy address of first account

$ ganache-cli
Paste this adderess to ui/js/clist.js line 17

techdot/ui/js/clist.js

Line 17 in cecabc1

 contractInstance = VotingContract.at('0xa7fb89a3fe6927b6d272637b148775f6fee5a8cf'); 
 ![image](https://user-images.githubusercontent.com/90682538/204466245-b0f6e6e9-2c0c-4fb4-b46f-a3e5a51c3ab8.png)
