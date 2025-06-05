# USDS IdentityDepository Architecture

The **USDS IdentityDepository** is a Solana smart contract that facilitates algorithmic minting and redeeming of USDS tokens against supported collateral assets (USDC and USDT). Its architecture prioritizes stability, atomicity, and safe execution, relying on a trusted controller and validated vaults to manage collateral securely.

---

## 🧱 Core Components

### 1. IdentityDepository Program

This smart contract handles the primary logic for:

- **Minting USDS** with validated collateral (USDC/USDT)
- **Redeeming USDS** back into collateral
- Ensuring authority constraints and atomic operations

It uses Solana’s account model and Anchor framework for structure and security.

---

## 🔄 Mint Flow

> **Goal**: Mint USDS in exchange for accepted stablecoin collateral.

### 🔧 Steps:

1. **Collateral validation**  
   Only supported mints (USDC, USDT) are allowed.

2. **Fee deduction**  
   Correct fee is calculated and subtracted from collateral before minting.

3. **Vault accounting**  
   Collateral is transferred to a secure vault.

4. **USDS minting**  
   New USDS tokens are issued to the user.

All logic is enforced using strict access control via a `controller` authority and runtime validation checks.

---

## 🔁 Redeem Flow

> **Goal**: Burn USDS to retrieve collateral in a stable and secure way.

### 🔧 Steps:

1. **Burn first**  
   User’s USDS tokens are burned before any collateral is released.

2. **Collateral selection**  
   Based on the user’s input, the correct vault (USDC or USDT) is dynamically selected using an enum-based router.

3. **Transfer second**  
   The corresponding amount of collateral is transferred to the user.

### 🔐 Safety Features:

- Enforces `burn-before-transfer` to prevent double claims.
- All math operations use `checked_*` functions to prevent overflows.
- Only trusted controllers or their delegates can execute redemptions.

---

## 🔍 Design Decisions

- **Trusted Controller**: Central authority (can be a DAO or multisig) is responsible for execution permissions.
- **No Perpetuals**: Unlike previous UXD designs, the protocol does not depend on derivatives for stability.
- **Dual Vault Routing**: Clean separation of USDC and USDT vaults prevents collateral mismatches.

---

## ⚙️ Technical Files (from audit)

- `mint_with_identity_depository.rs`
- `redeem_from_identity_depository.rs`
- `identity_depository.rs` (state definitions)
- `controller.rs` (authority logic)
- `lib.rs` and `mint.rs` (instruction dispatch)
- Utility modules for:
  - Account validation
  - PDA derivation
  - Fee computation

---

## ✅ Summary

The IdentityDepository follows a **minimalist, security-focused architecture**:

- Simplicity improves auditability.
- All flows are linear, atomic, and access-controlled.
- Stablecoin management is deterministic, transparent, and vault-safe.

This design provides a strong foundation for trustless stablecoin issuance within the USDS protocol.
