

# Testnet USDT (TRC20-Compatible) Token for Shasta

This repository contains a Solidity smart contract designed to simulate the Tether USD (USDT) TRC20 token, specifically for **testing purposes** on the Tron Shasta testnet. It's ideal for developers building marketplaces or dApps that need a mock USDT for their Tron testnet environment without dealing with real funds.

**❗ IMPORTANT: This is NOT the official USDT token and holds no real-world value. It is solely for development and testing on the Shasta testnet.**

## Table of Contents

-   [Features](#features)
-   [Prerequisites](#prerequisites)
-   [Contract Code](#contract-code)
-   [Deployment to Shasta Testnet](#deployment-to-shasta-testnet)
-   [Usage and Interaction](#usage-and-interaction)
-   [Security Disclaimer](#security-disclaimer)
-   [License](#license)

## Features

This `TestUSDTTRC20` contract extends OpenZeppelin's robust smart contract libraries to provide the following functionalities:

*   **ERC20 Standard Compliance:** Implements all core ERC20 functions (`transfer`, `transferFrom`, `balanceOf`, `approve`, `allowance`, `totalSupply`).
*   **USDT Metadata:**
    *   **Name:** "Tether USD"
    *   **Symbol:** "USDT"
    *   **Decimals:** `6` (matching the official USDT TRC20 token)
*   **Burnable:** Allows token holders to destroy their own tokens or tokens they have allowance for.
*   **Pausable:** Includes an emergency stop mechanism that can pause/unpause all token transfers, minting, and burning.
*   **Role-Based Access Control:** Utilizes OpenZeppelin's `AccessControl` for managing permissions:
    *   `DEFAULT_ADMIN_ROLE`: Grants/revokes all other roles. Initially assigned to the contract deployer.
    *   `PAUSER_ROLE`: Controls the `pause()` and `unpause()` functions. Initially assigned to the contract deployer.
    *   `MINTER_ROLE`: Allows authorized accounts to mint new tokens. Initially assigned to the contract deployer.
*   **Initial Supply:** An initial supply of `1,000,000 USDT` (equivalent to `1,000,000 * 10^6` raw units) is minted to the contract deployer upon creation.

## Prerequisites

Before deploying this contract, you'll need:

1.  **TronLink Wallet:** A browser extension wallet for Tron, set to the **Shasta Testnet**.
    *   [Download TronLink](https://www.tronlink.org/)
2.  **Shasta Testnet TRX:** You'll need some test TRX (Tron's native currency) in your TronLink wallet to cover deployment and transaction fees (bandwidth and energy) on the Shasta network.
    *   You can get free Shasta TRX from a faucet, e.g.: [https://nileex.io/join/getFreeTestTron](https://nileex.io/join/getFreeTestTron) or [https://www.trongrid.io/faucet](https://www.trongrid.io/faucet) (ensure the faucet supports Shasta).


## Deployment to Shasta Testnet

Follow these steps to deploy your `TestUSDTTRC20` token to the Tron Shasta testnet:

1.  **Ensure TronLink is on Shasta:**
    *   Open your TronLink browser extension.
    *   Click on the network dropdown (usually shows "Mainnet").
    *   Select `Shasta Testnet`.
2.  **Get Test TRX:**
    *   Copy your TronLink wallet address (it should start with 'T').
    *   Visit a Shasta TRX Faucet (e.g., [https://nileex.io/join/getFreeTestTron](https://nileex.io/join/getFreeTestTron)).
    *   Paste your address and request test TRX. You'll need TRX to cover energy/bandwidth costs for deployment and transactions.
3.  **Compile & Deploy via Tronscan:**
    *   Go to the Tronscan Shasta Testnet Contract Compiler: [https://shasta.tronscan.org/#/contract/compile](https://shasta.tronscan.org/#/contract/compile)
    *   **Paste the entire `TestUSDTTRC20.sol` code** (from the "Contract Code" section above, including all comments and OpenZeppelin libraries) into the editor.
    *   Verify the `Solidity version` selected in the compiler matches the `pragma solidity ^0.8.18;` in the contract (or is compatible).
    *   Click the **"Compile"** button. If successful, you'll see a green "Compiled" message.
    *   Scroll down to the **"Deploy"** section.
    *   In the `Contract` dropdown, select `TestUSDTTRC20`.
    *   The `Constructor Params` should be empty, as the token name, symbol, and initial mint are hardcoded in the constructor.
    *   Click the **"Deploy"** button.
    *   Your TronLink wallet will pop up. Review the transaction details (especially the TRX cost for bandwidth/energy) and **"Accept"** or **"Sign"** the transaction.
4.  **Record Contract Address:**
    *   After the transaction is confirmed, Tronscan will display the **deployed contract address**. Copy this address. This is the address of your new "Fake USDT" token on Shasta.
    *   You can also find this address in your TronLink transaction history.
5.  **Add Custom Token to TronLink:**
    *   Open your TronLink wallet.
    *   Navigate to the "Assets" tab.
    *   Click the **"+"** (Add Asset) button.
    *   Select **"Custom Token"**.
    *   Paste the deployed contract address you copied in the previous step.
    *   TronLink should automatically populate the `Token Name` as "Tether USD", `Token Symbol` as "USDT", and `Decimals` as "6".
    *   Confirm to add the token.

You should now see your `TestUSDTTRC20` (as USDT) with the initial `1,000,000` balance in your TronLink wallet on Shasta!

## Usage and Interaction

With your `TestUSDTTRC20` deployed, you can now use it to test your marketplace:

*   **Transfer Tokens:** Send test USDT from your deployer account to other test accounts or your marketplace contract.
*   **Check Balances:** Verify balances of various accounts interacting with your marketplace.
*   **Mint More Tokens:** If you need more test USDT, call the `mint(address to, uint256 amount)` function from the deployer's account (which has `MINTER_ROLE`). Remember to include the `6` decimals when specifying `amount` (e.g., `100 * 10**6` for 100 USDT).
*   **Pause/Unpause:** Test pausing all token operations using `pause()` and `unpause()` (only callable by `PAUSER_ROLE`).
*   **Burn Tokens:** Test burning tokens using `burn()` or `burnFrom()`.
*   **Role Management:** Practice granting or revoking roles like `PAUSER_ROLE` or `MINTER_ROLE` to other test accounts using `grantRole()` and `revokeRole()`.

## Security Disclaimer

**THIS CONTRACT IS INTENDED SOLELY FOR DEVELOPMENT AND TESTING ON THE TRON SHASTA TESTNET.**

*   **DO NOT DEPLOY THIS CONTRACT ON THE TRON MAINNET.**
*   **IT IS NOT THE OFFICIAL USDT TOKEN.**
*   **IT HAS NO REAL-WORLD VALUE OR BACKING.**
*   Any use of this contract on a live network or for purposes other than testnet development is strongly discouraged and done at your own risk.
*   While this contract leverages battle-tested OpenZeppelin libraries, any modifications or integration into a larger system should be thoroughly reviewed and audited for security vulnerabilities.

## License

This project is licensed under the MIT License - see the `LICENSE` file (if applicable, or simply state here) for details. The underlying OpenZeppelin contracts are also MIT licensed.
