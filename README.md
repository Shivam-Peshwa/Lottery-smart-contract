Ethereum Lottery Smart Contract 🎰🎟️
This is a simple Ethereum-based Lottery Contract written in Solidity. Participants enter by sending ETH, and a randomly selected winner receives the entire pool.

🚀 Features
Users enter the lottery by sending >0.01 ETH.
The manager (deployer) selects a winner using a pseudo-random function.
The contract transfers all ETH to the winner and resets.

📜 Smart Contract Code
The contract is written in Solidity 0.4.17:

pragma solidity ^0.4.17;

contract Lottery {
    address public manager;
    address[] public players;
    
    function Lottery() public {
        manager = msg.sender;
    }
    
    function enter() public payable {
        require(msg.value > .01 ether);
        players.push(msg.sender);
    }
    
    function random() private view returns (uint) {
        return uint(keccak256(block.difficulty, now, players));
    }
    
    function pickWinner() public restricted {
        uint index = random() % players.length;
        players[index].transfer(this.balance);
        players = new address  }
    
    modifier restricted() {
        require(msg.sender == manager);
        _;
    }
    
    function getPlayers() public view returns (address[]) {
        return players;
    }
}

⚙️ Setup & Deployment

1️⃣ Install Dependencies
Make sure you have Node.js and NPM installed. Then, install the required packages:
npm install

2️⃣ Compile the Contract
Compile the contract using Solc:
node compile.js

3️⃣ Deploy to Ethereum
Modify your deploy.js to use a valid Ethereum provider (Infura, Alchemy, etc.), then run:
node deploy.js

🧪 Testing
Run the test suite using Mocha & Ganache:
npm run test

🔍 Tests Covered:
✅ Contract Deployment
✅ Single & Multiple Players Entering
✅ Minimum Entry Fee Check
✅ Restricting pickWinner to Manager
✅ Winner Receives ETH and Players List Resets

📌 Future Improvements
Use Chainlink VRF for true randomness.
Add frontend UI with React & Web3.js.
Deploy on a testnet (Goerli, Sepolia) before mainnet.

📜 License
This project is open-source under the MIT License.
