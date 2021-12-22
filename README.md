# Proof of Authority Development Chain

To deploy the private blockchain, follow the below steps: 

## Step 1: Ensuring Go Ethereum (GETH) and Metamask have been installed 

https://geth.ethereum.org/downloads

https://metamask.io/

## Step 2: Create x2 new nodes with GETH
Open Terminal > Locate 'Blockchain-Tools' directory > Enter the following code

``` 
./geth --datadir node1 account new
./geth --datadir node2 account new
```
Note down the Public Key / Account Address onto a text file

## Step 3: Generate Genesis Block

* Run puppeth, name your network, and select the option to configure a new genesis block.

* Choose the Clique (Proof of Authority) consensus algorithm.

* Paste both account addresses from the first step one at a time into the list of accounts to seal.

* Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

* Continue with the default option for the prompt that asks, Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? Answer 'Yes".

* Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

* Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.


## Step 4: Initializing nodes with genesis json file

Using geth, initialize each node with the new networkname.json.

```
./geth --datadir node1 init networkname.json
./geth --datadir node2 init networkname.json
```

## Step 5: Enable nodes to start mining

Now the nodes can be used to begin mining blocks.

Run the nodes in separate terminal windows with the commands:
```
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
```

NOTE: Type your password and hit enter - even if you can't see it visually!

Your private PoA blockchain should now be running!

With both nodes up and running, the blockchain can be added to Metamask for testing.

## Step 6: Add Network to Metamask

* Log-in to your Metamask 
* Go to Settings > Networks > Add Network 
* Chain ID: Used the information generated in #Step 3
* New RPC URL: http://127.0.0.1:8545
* Currency Symbol: ETH
* Network Name: Any Names

## Step 7: Add Nodes to Metamask by importing keystore

* In Metamask, select Import Account
* Select Type set as 'JSON file' 
* Locate your keystore (should be in 'Blockchain-Tools\node1\keystore' in your local machine)
* Type in your node password that is set in #Step 2 (Note this is NOT your Metamask password)
* Click Import, this might take a while, just be patient and do not close the Metamask

## Step 8: Send a Test Transactions 

* In Metamask, go to either node, copy the wallet address 
* Click on Send > Paste Wallet Address > Set the amount of ETH > Confirm 
* Your transaction status will be displayed in the Activity tab


































