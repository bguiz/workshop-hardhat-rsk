# Workshop Hardhat RSK

## Instructions

Follow the instructions below in a POSIX-compliant terminal.
Where you see `code ${FILE}` this means you will need to edit that file.
See the files committed in this repo and use them for reference.

```shell
# start project
npm init
npm i -SDE hardhat @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai

# init hardhat config with defaults
npx hardhat
# select: Create an empty hardhat.config.js

# set up for connecting to RSK Testnet
npx mnemonics > .testnet.seed-phrase
curl https://public-node.testnet.rsk.co/ \
  -X POST 
  -H "Content-Type: application/json"
  --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false],"id":1}'
  > .minimum-gas-price-testnet.json
npx mnemonics > .testnet.seed-phrase
code hardhat.config.js

# create smart contract implementation and compile it
mkdir contracts
touch contracts/Token.sol
code contracts/Token.sol
npx hardhat compile

# create smart contract tests and execute them
mkdir test
touch test/Token.js
code test/Token.js
npx hardhat test

# create smart contract deployment script and dry-run the deployment
mkdir scripts
touch scripts/deploy.js
code scripts/deploy.js
npx hardhat run scripts/deploy.js

# perform an actual deployment to RSK Testnet
# vist htps://faucet.rsk.co/ and dispense to ${ACCOUNT_ADDRESS}
npx hardhat run scripts/deploy.js --network rsktestnet
# visit https://explorer.testnet.rsk.co/address/${TOKEN_ADDRESS}

```
