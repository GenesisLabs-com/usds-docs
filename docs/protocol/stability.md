# Stability Mechanism

USDS maintains its stability algorithmically without using fiat or crypto collateral.

## 🧠 Core Mechanism: Elastic Supply

USDS uses a **rebase mechanism** that automatically:
- Increases supply when price is above peg
- Decreases supply when price is below peg

## 🛰️ Price Oracles

- Pull real-time price data from decentralized oracles
- Use time-weighted averages to prevent manipulation

## 📉 Contraction Example

If USDS > $1:
- Protocol mints USDS to incentivize arbitrage
- Supply expands until peg is restored

If USDS < $1:
- Protocol contracts supply via bonding, burns, or delayed minting
- Demand-supply balance is restored without collateral backing

## 💡 Design Philosophy

Stability arises from **protocol logic + market behavior**, not from reserves or custodians.

---
