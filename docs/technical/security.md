# Security Model

USDS was designed with a security-first mindset, drawing from industry best practices in Solana smart contract development.

---

## 🔐 Key Security Mechanisms

### 1. **Authority Enforcement**

- All mint and redeem instructions are **restricted to trusted signers**
- Controller keys are enforced at runtime and validated using PDAs
- Prevents unauthorized access to vaults or token supply

---

### 2. **Atomic Transaction Structure**

- **Mint flow**: validates inputs → transfers collateral → mints USDS
- **Redeem flow**: burns USDS → transfers collateral
- Order ensures no race conditions or reentrancy vulnerabilities

---

### 3. **Safe Arithmetic**

- Uses Rust’s `checked_*` math functions throughout
- Prevents overflow/underflow during:
  - Fee calculations
  - Token transfers
  - Vault balances

---

### 4. **Collateral Routing Protection**

- Enum-based selection of USDC/USDT vaults
- Prevents mixing up or cross-leaking between collateral types
- Verifies vault account ownership and derivation on-chain

---

### 5. **Pre-Execution Validation**

- Confirms all inputs are correct and state is initialized
- Checks balances, token mints, rent exemption, and signer seeds
- Stops transactions early on invalid conditions

---

## 🧪 Audit Summary

- **Auditor**: Genesis IT Lab
- **Version Audited**: v1.0.0
- **Date**: June 2025
- **Severity**: No critical or high-impact vulnerabilities
- **All findings**: Informational only, resolved or acknowledged

> See [Audit Report](../audit/) for detailed findings.

---

## ⚠️ Known Limitations

- **No runtime decimal validation** for USDC/USDT — assumes standard (6 decimals)
- **Trusted controller** model — does not yet use DAO-based governance

---

## 🛡 Recommendations

- Add dynamic checks for token mint decimals
- Consider DAO-based governance for future iterations
- Monitor mint/redeem volume to evaluate performance under load

---

USDS is secure by design, leveraging conservative assumptions, strict validation, an
