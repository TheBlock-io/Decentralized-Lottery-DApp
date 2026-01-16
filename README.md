
# Decentralized Lottery / Raffle DApp (Backend)

A **trustless decentralized lottery/raffle** on Ethereum-compatible blockchains. Users buy tickets, and winners are picked automatically using **Chainlink VRF** for secure randomness and **Chainlink Keepers** for automated draws.


## Features:

* **Decentralized and Trustless:** Smart contracts manage ticket sales and prize distribution.

* **Fair Winner Selection:** Uses *Chainlink* VRF for verifiable randomness.

* **Automated Draws:** *Chainlink Keepers* trigger the raffle at set intervals.

* **Transparent and Auditable:** All activity is on-chain.

* **Configurable Raffles:** Set entrance fees, intervals, and prize pools.


## Tech Stack:

* **Blockchain:** Ethereum / Polygon / BSC ... ` (EVM-compatible) `.

* **Smart Contracts:** Solidity.

* **Automation and Randomness:** *Chainlink VRF and Keepers*.

* **Testing and Deployment:** Hardhat.


## Smart Contract Overview:

| Function               | Description                                                    |
| ---------------------- | -------------------------------------------------------------- |
| `enterRaffle()`        | Buy a ticket to join the raffle.                               |
| `checkUpkeep()`        | Checks if conditions are met for a raffle draw.                |
| `performUpkeep()`      | Triggered by Keepers to request a random winner.               |
| `fulfillRandomWords()` | Called by Chainlink VRF to select a winner and transfer prize. |
| `getRecentWinner()`    | Returns the last winner.                                       |
| `getNumberOfPlayers()` | Returns the number of participants.                            |


## Deployment:

`git clone https://github.com/TheBlock-io/Decentralized-Lottery-DApp.git`
`cd Decentralized-Lottery-DApp`
`npm install`
`npx hardhat compile`
`npx hardhat deploy --network` **<your-network>**

Interact with the contract via Hardhat scripts to enter the raffle, trigger draws, and check winners.


## Security:

* **Immutable contracts** after deployment.

* **Chainlink VRF** guarantees unbiased randomness.

* **Chainlink Keepers** automate draws without manual intervention.

* Always test thoroughly on testnets before mainnet deployment.


## Raffle Flow:
+----------------+        enterRaffle()       +----------------+
|    Player      | ------------------------> |    Raffle      |
|  Buys Ticket   |                           |  Contract      |
+----------------+                           +----------------+
         |                                           |
         |                                           |
         |                                           |
         |                                     checkUpkeep()
         |                                           |
         |                                           v
         |                                +----------------+
         |                                | Chainlink      |
         |                                |   Keepers      |
         |                                |  (Automation)  |
         |                                +----------------+
         |                                           |
         |                                           |
         |                                performUpkeep()
         |                                           |
         |                                           v
         |                                +----------------+
         |                                | Chainlink VRF  |
         |                                |  (Randomness)  |
         |                                +----------------+
         |                                           |
         |                                           |
         |                                fulfillRandomWords()
         |                                           |
         |                                           v
         |                                +----------------+
         |                                | Winner Address |
         |                                | Receives Prize |
         |                                +----------------+

## Flow Summary:

1 - **Players enter** the raffle by sending ETH via `enterRaffle()`.

2 - **Chainlink Keepers** check if the raffle interval has passed, there are players, and ETH is available.

3 - If conditions are met, `performUpkeep()` requests a random number from **Chainlink VRF**.

4 - **VRF returns a secure random number**, which is used to select a winner.

5 - **The winner automatically receives** the prize from the contract.

6 - The raffle **resets** for the next round.


## Acknowledgements:

Special thanks to **PATRICK COLLINS** for creating the course that made this project possible.