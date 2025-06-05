# Smart Contracts Overview

The USDS protocol implements a secure and minimal set of smart contracts to manage the minting and redeeming of USDS against stable collateral assets like USDC and USDT. These contracts are deployed on the **Solana blockchain** and built using the **Anchor framework**.

---

## 🧩 Key Contracts

### 1. `identity_depository.rs`

Defines the core on-chain structure that manages:

- Accepted collateral types
- Minting and redemption vault logic
- Controller authority verification
- Configuration for fees, supply limits, and state

---

### 2. `mint_with_identity_depository.rs`

Handles the minting flow:

- Validates supported collateral types
- Verifies signer authority
- Calculates and deducts fees
- Transfers collateral to vault
- Mints USDS tokens to the user

---

### 3. `redeem_from_identity_depository.rs`

Handles the redeem flow:

- Burns the correct amount of USDS
- Validates selected collateral type
- Transfers stablecoins from vault to user
- Protects against reentrancy and access misuse

---

### 4. `controller.rs`

Implements authority logic:

- Governs who can execute privileged instructions (e.g., mint, redeem)
- Can be a multisig, DAO, or centralized authority
- Used to enforce execution constraints via signer validation

---

## 🛠 Additional Components

- **Utility modules**:
  - PDA derivation
  - SPL token interface management
  - Fee calculations

- **Vault logic**:
  - Handles separate vault accounts for USDC and USDT
  - Routes requests based on user-selected collateral type

---

## 🧪 Testing and Deployment

- Written in Rust using the Anchor framework
- Unit and integration tests provided in the `/tests/` folder
- Deployable to Solana mainnet/testnet using Anchor CLI

> View the full source: [GitHub repository](https://github.com/usds-protocol/usds) *(placeholder)*
