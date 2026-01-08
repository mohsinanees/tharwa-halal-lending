# Shariah-Compliant Crypto Lending Protocol
## A Halal Alternative to Aave & Compound

**Version:** 1.0
**Date:** January 2026
**Status:** Architecture & Design Specification

---

## Executive Summary

This document presents the complete architecture for a Shariah-compliant decentralized lending protocol that enables users to access crypto liquidity (BTC, ETH, SOL, DOT, etc.) without Riba (interest). The protocol uses authentic Islamic finance structures—**Mudarabah** (profit-sharing partnership) and **Murabaha** (cost-plus sale)—to replicate the functionality of protocols like Aave and Compound while maintaining full Shariah compliance.

### Key Innovation

Unlike conventional lending protocols that operate on interest-based models (Riba), our protocol:
- Accepts **stablecoin deposits** (USDC, USDT, thUSD) into **Mudarabah investment pools**
- Protocol acts as **Mudarib** (active manager), buying volatile assets from the market
- Sells these assets to borrowers via **Murabaha** (asset sale with markup, deferred payment in stablecoins)
- Distributes **trading profits** (not interest) to investors

### Core Differentiators

| Feature | Aave/Compound | Our Protocol |
|---------|---------------|--------------|
| Deposit Asset | Any crypto | Stablecoins only (USDC, USDT, thUSD) |
| Returns Source | Interest on loans | Profit from Murabaha trading |
| Borrowing Model | Borrow same asset, repay with interest | Buy asset via Murabaha, repay in stablecoins |
| Investor Role | Lender (creditor) | Partner (investor) in Mudarabah |
| Protocol Role | Facilitator | Mudarib (active capital manager) |
| Risk Sharing | Limited | Yes - investors share profits AND losses |
| Shariah Compliance | No (Riba-based) | Yes (certified by Shariah board) |

---

## Table of Contents

1. [Fundamental Shariah Principles](#1-fundamental-shariah-principles)
2. [The Core Problem & Solution](#2-the-core-problem--solution)
3. [Protocol Architecture Overview](#3-protocol-architecture-overview)
4. [Component A: Mudarabah Investment Pools](#4-component-a-mudarabah-investment-pools)
5. [Component B: Volatile Asset Inventory](#5-component-b-volatile-asset-inventory)
6. [Component C: Murabaha Execution Engine](#6-component-c-murabaha-execution-engine)
7. [Component D: Collateral Management](#7-component-d-collateral-management)
8. [Component E: Liquidation Engine](#8-component-e-liquidation-engine)
9. [Component F: Shariah Governance](#9-component-f-shariah-governance)
10. [Smart Contract Architecture](#10-smart-contract-architecture)
11. [Key User Workflows](#11-key-user-workflows)
12. [Risk Management Framework](#12-risk-management-framework)
13. [Economic Model & Projections](#13-economic-model--projections)
14. [Protocol Parameters](#14-protocol-parameters)
15. [User Interfaces](#15-user-interfaces)
16. [Implementation Roadmap](#16-implementation-roadmap)
17. [Shariah Compliance Documentation](#17-shariah-compliance-documentation)

---

## 1. Fundamental Shariah Principles

### 1.1 The Core Prohibition: Riba (Interest)

**Riba** is strictly forbidden in Islamic finance. It is defined as:
> "Any predetermined increase or profit on a loan or debt"

**Examples of Riba:**
- ❌ Lend 10 ETH → Receive back 12 ETH (interest on same asset)
- ❌ Deposit $100K USDC → Earn 5% APY interest
- ❌ Time-value of money (charging more just because time has passed)

### 1.2 What IS Permissible (Halal)

**Profit from Trade:**
- ✅ Buy 10 ETH for $20K → Sell 10 ETH for $22K (trading profit)
- ✅ Partner in a business venture → Share in profits/losses
- ✅ Charge fees for genuine services (not disguised interest)

**Key Principle:**
> "You cannot earn profit on an asset if you are receiving the same asset back in greater quantity. But you CAN earn profit by trading different assets."

### 1.3 The Three Islamic Finance Structures We Use

#### **Mudarabah (Investment Partnership)**

**Structure:**
- **Rab-ul-Maal** (Capital Provider): Provides 100% of capital
- **Mudarib** (Manager): Provides expertise, actively manages capital
- **Profit Sharing:** Pre-agreed ratio (e.g., 70% to investors, 30% to manager)
- **Loss Bearing:** Capital provider bears financial losses; manager loses time/effort

**Example:**
- Investor deposits $100K → Protocol deploys it for trading
- Protocol earns $10K profit → Split 70/30
- Investor gets $7K, Protocol gets $3K

#### **Murabaha (Cost-Plus Sale)**

**Structure:**
- Buyer wants an asset but lacks liquidity
- Seller purchases the asset first (takes ownership)
- Seller sells asset to buyer at **cost + known markup**
- Payment can be deferred (installments)

**Example:**
- Bob wants 10 ETH but has no cash
- Protocol buys 10 ETH for $20,000 (cost price)
- Protocol sells 10 ETH to Bob for $21,200 (6% markup)
- Bob pays $21,200 in installments over 90 days
- Bob repays in USDC (different asset), not ETH

**Critical:** Protocol must **own the asset** before selling it (bears ownership risk).

#### **Wakalah (Agency)**

**Structure:**
- Principal appoints an agent to act on their behalf
- Agent manages assets, executes transactions
- Agent earns fixed fee or profit share for services

**In Our Protocol:**
- Investors appoint Protocol as their agent (Wakeel)
- Protocol has authority to deploy capital
- Combined with Mudarabah for profit-sharing

### 1.4 Why Traditional Crypto Lending Violates Shariah

**Aave/Compound Model:**
```
User deposits 10 ETH → Earns 3% APY → Withdraws 10.3 ETH
                        ↑
                    Pure Riba
```

**The Problem:**
- Same asset in, same asset out, with increase
- No real trading or business venture
- Interest accrues based on time (time-value of money)
- No profit/loss sharing—lenders always earn positive return

---

## 2. The Core Problem & Solution

### 2.1 What We're Trying to Achieve

Build a protocol where:
- **Investors** can deposit idle stablecoins and earn halal returns
- **Borrowers** can access crypto liquidity (BTC, ETH, SOL, etc.) against collateral
- **No Riba** - all returns come from legitimate trading profits
- **Scalable** - works like Aave (pooled liquidity, automated, permissionless)

### 2.2 The Breakthrough Insight

**Islamic banks solved this decades ago:**

They DON'T give borrowers money from the deposit pool directly. Instead:

1. **Deposit Side:** Structured as **Mudarabah** (investment partnership)
   - Depositors are investors, not lenders
   - No guaranteed returns—they share in profits/losses

2. **Lending Side:** Structured as **Murabaha** (asset purchase & sale)
   - Bank BUYS the asset customer wants (car, house, inventory)
   - Bank SELLS asset to customer at markup with deferred payment
   - Customer repays in money (different from asset received)

**Key Transformation:**
- The pool funds flow through, but there's an **asset transaction** in the middle
- Bank takes **ownership risk** when it buys the asset
- Profit comes from **trading** (buying/selling), not from time-value of money

### 2.3 Our Crypto Adaptation

**The Model:**

```
┌─────────────────────────────────────────────────────────────┐
│                    SHARIAH-COMPLIANT FLOW                    │
└─────────────────────────────────────────────────────────────┘

INVESTOR SIDE (Mudarabah):
   Investor deposits USDC
        ↓
   Becomes partner in Mudarabah pool
        ↓
   Protocol (Mudarib) deploys capital
        ↓
   Profits distributed 70/30

PROTOCOL (Mudarib + Wakeel):
   Takes USDC from pool
        ↓
   BUYS volatile assets (BTC, ETH, SOL) from market
        ↓
   OWNS these assets in inventory pools
        ↓
   SELLS to borrowers via Murabaha
        ↓
   Earns markup profit

BORROWER SIDE (Murabaha):
   Wants 10 ETH
        ↓
   Protocol sells 10 ETH at cost + markup ($20K → $21.2K)
        ↓
   Borrower receives 10 ETH immediately
        ↓
   Repays $21.2K USDC in installments
        ↓
   Provides BTC collateral
```

**Why This Works:**
- ✅ No Riba: Investors deposit USDC, earn USDC from trading profits
- ✅ Real ownership: Protocol actually BUYS and OWNS the crypto assets
- ✅ Different assets: Borrower gets ETH, repays USDC (no same-asset Riba)
- ✅ Mudarabah compliance: Investors are true partners, sharing profits AND losses
- ✅ Murabaha compliance: Clear asset sale with known markup

---

## 3. Protocol Architecture Overview

### 3.1 High-Level System Design

```
┌─────────────────────────────────────────────────────────────┐
│              THARWA SHARIAH LENDING PROTOCOL                 │
│           (Mudarabah + Murabaha Hybrid Model)                │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│  DEPOSIT SIDE │    │ PROTOCOL CORE │    │ BORROWER SIDE │
│  (Mudarabah)  │    │  (Mudarib)    │    │  (Murabaha)   │
│               │    │               │    │               │
│  - Investors  │───▶│ - Asset Pools │───▶│ - Borrowers   │
│  - Stablecoins│    │ - Inventory   │    │ - Get Crypto  │
│  - 70-80%     │◀───│ - Management  │◀───│ - Repay USDC  │
│    Returns    │    │ - 20-30% Fee  │    │ - Collateral  │
└───────────────┘    └───────────────┘    └───────────────┘
```

### 3.2 Core Components

The protocol consists of six major components:

1. **Mudarabah Investment Pools** - Accept stablecoin deposits from investors
2. **Volatile Asset Inventory** - Protocol-owned pools of BTC, ETH, SOL, DOT, etc.
3. **Murabaha Execution Engine** - Facilitates asset sales to borrowers
4. **Collateral Management System** - Secures borrower obligations
5. **Liquidation Engine** - Protects against defaults
6. **Shariah Governance Board** - Ensures ongoing compliance

### 3.3 Technology Stack

**Blockchain:**
- Primary: Ethereum (mainnet)
- Future: Multi-chain (Polygon, Arbitrum, Base)

**Smart Contracts:**
- Solidity 0.8.x
- OpenZeppelin libraries
- ERC-4626 for vault shares
- Proxy pattern for upgradeability

**Oracles:**
- Chainlink Price Feeds (primary)
- Pyth Network (backup)
- Shariah Oracle (asset certification)

**Frontend:**
- React + TypeScript
- Web3.js / Ethers.js
- WalletConnect integration

---

## 4. Component A: Mudarabah Investment Pools

### 4.1 Overview

Mudarabah pools are the **deposit side** of the protocol where investors provide capital.

**Key Characteristics:**
- Accepts ONLY stablecoins (USDC, USDT, thUSD)
- Structured as profit-sharing partnerships (Mudarabah)
- Fixed lock-up periods (term-based)
- Proportional profit distribution
- Investors share in profits AND losses

### 4.2 Pool Types

We offer four pool types with different risk/return profiles:

#### **30-Day Mudarabah Pool**

| Parameter | Value |
|-----------|-------|
| Lock Period | 30 days (fixed) |
| Target APY | 4-6% |
| Mudarib Share | 25% |
| Investor Share | 75% |
| Minimum Deposit | 1,000 USDC |
| Use Case | Short-term parking, conservative investors |

#### **90-Day Mudarabah Pool**

| Parameter | Value |
|-----------|-------|
| Lock Period | 90 days (fixed) |
| Target APY | 6-9% |
| Mudarib Share | 25% |
| Investor Share | 75% |
| Minimum Deposit | 5,000 USDC |
| Use Case | Medium-term investment, balanced risk/return |

#### **180-Day Mudarabah Pool**

| Parameter | Value |
|-----------|-------|
| Lock Period | 180 days (fixed) |
| Target APY | 10-14% |
| Mudarib Share | 25% |
| Investor Share | 75% |
| Minimum Deposit | 10,000 USDC |
| Use Case | Long-term investment, aggressive returns |

#### **Flexible Pool**

| Parameter | Value |
|-----------|-------|
| Lock Period | None (withdraw anytime) |
| Target APY | 2-4% |
| Mudarib Share | 30% (higher due to liquidity risk) |
| Investor Share | 70% |
| Minimum Deposit | 100 USDC |
| Use Case | Emergency liquidity, liquidity buffer |

### 4.3 Accepted Stablecoins

| Asset | Rationale | Weight Cap |
|-------|-----------|------------|
| USDC | Most liquid, regulated, audited | 60% |
| USDT | High liquidity, widely accepted | 30% |
| thUSD | Tharwa's RWA-backed stablecoin, strategic | 10% |

**Why Stablecoins Only?**
- Eliminates same-asset Riba (deposit USDC → earn USDC from trading)
- Provides stable base for acquiring volatile assets
- Simplifies accounting and profit calculation
- Reduces volatility risk for investors

### 4.4 Deposit Workflow

**Step-by-Step Process:**

1. **Investor selects pool:**
   - Reviews APY, lock period, terms
   - Example: "90-Day Pool - 8.1% APY"

2. **Investor deposits stablecoins:**
   - Approves USDC spend
   - Deposits 100,000 USDC

3. **Investor receives receipt tokens:**
   - Protocol mints **mdUSDC-90** tokens (Mudarabah vault shares)
   - These are ERC-4626 tokens representing proportional ownership
   - Example: Receives 100,000 mdUSDC-90 tokens

4. **Capital deployed:**
   - Protocol (as Mudarib) deploys capital to acquire assets
   - Buys BTC, ETH, SOL from market
   - Sells to borrowers via Murabaha

5. **Profit accumulation:**
   - Murabaha profits accumulate in protocol treasury
   - Tracked per pool, per investor

6. **Maturity & Withdrawal:**
   - After 90 days, investor can redeem mdUSDC-90 tokens
   - Receives: Principal (100,000 USDC) + Profit Share (e.g., 8,100 USDC)
   - Total: 108,100 USDC (8.1% return)

### 4.5 Profit Distribution Mechanics

**Monthly Distribution Cycle:**

1. Protocol collects all Murabaha revenues for the month
   - Example: $50,000 total profit

2. Mudarib/Investor split applied:
   - Mudarib (Protocol): 25% = $12,500
   - Investors (Rab-ul-Maal): 75% = $37,500

3. Investor allocation (proportional by pool):
   - 30-Day Pool TVL: $10M (20%) → $7,500
   - 90-Day Pool TVL: $25M (50%) → $18,750
   - 180-Day Pool TVL: $15M (30%) → $11,250

4. Individual investor allocation:
   - Alice has 100K USDC in 90-Day pool (total: $25M)
   - Alice's share: 0.4%
   - Alice receives: $18,750 × 0.4% = $75 for the month
   - Annualized: ~9% APY

**Profit Accrual:**
- Profits accrue to the vault share token (mdUSDC)
- Redemption value increases over time
- Example: 1 mdUSDC-90 = 1.081 USDC after 90 days

### 4.6 Loss Sharing (Critical for Mudarabah)

**Unlike Aave:** Investors can experience losses if Protocol performs poorly.

**Scenario:**
- Protocol buys 50 ETH @ $2,000 = $100K
- ETH drops to $1,800 before selling
- Inventory loss: $10K
- This loss is borne by investors (capital providers)

**Mitigation:**
- Protocol actively manages inventory risk (see Risk Management)
- Conservative purchasing policies
- Hedging strategies
- Over-collateralization on borrower side reduces default risk

**Important:** This loss-sharing is REQUIRED for Shariah compliance. Guaranteed returns = Riba.

---

## 5. Component B: Volatile Asset Inventory

### 5.1 Overview

The Protocol maintains **inventory pools** of volatile crypto assets that are purchased using Mudarabah pool funds and sold to borrowers via Murabaha.

**Key Point:** The Protocol **OWNS** these assets. This ownership is critical for Shariah compliance—the Protocol bears the risk of price depreciation.

### 5.2 Supported Assets

Assets must be **halal-certified** by the Shariah Governance Board before inclusion.

**Initial Asset List:**

| Asset | Symbol | Certification Status | Risk Tier |
|-------|--------|---------------------|-----------|
| Bitcoin | BTC | Certified Halal | Low |
| Ethereum | ETH | Certified Halal | Low |
| Polkadot | DOT | Certified Halal | Medium |
| Solana | SOL | Under Review | Medium |
| Polygon | MATIC | Under Review | Medium |

**Certification Criteria:**
- ✅ Decentralized governance
- ✅ Utility-driven (not pure speculation)
- ✅ No direct involvement in haram activities (gambling, interest-bearing protocols)
- ✅ Transparent tokenomics
- ❌ Privacy coins (potential for illicit use)
- ❌ Meme coins (pure speculation = Maysir)
- ❌ DeFi governance tokens that earn protocol revenue from Riba

### 5.3 Inventory Management Strategy

**Goal:** Maintain sufficient inventory to meet borrower demand while minimizing price risk exposure.

#### **Inventory Targets:**

| Asset | Min Inventory | Target Inventory | Max Inventory |
|-------|---------------|------------------|---------------|
| BTC | 20 BTC | 50 BTC | 100 BTC |
| ETH | 200 ETH | 500 ETH | 1,000 ETH |
| DOT | 50,000 DOT | 100,000 DOT | 200,000 DOT |
| SOL | 10,000 SOL | 25,000 SOL | 50,000 SOL |

**Rebalancing Logic:**

```
IF inventory < Min Target:
    → Buy from market using Mudarabah pool funds
    → Target: 80% of Target Inventory

IF inventory > Max Target:
    → Sell excess to market
    → Convert to stablecoins
    → Return to Mudarabah pools

ELSE:
    → Maintain current levels
    → Fulfill Murabaha requests from inventory
```

#### **Just-In-Time Purchasing:**

For large orders (>10 ETH or equivalent), Protocol can buy on-demand:

1. Borrower requests 50 ETH
2. Protocol checks inventory: only 30 ETH available
3. Protocol buys 20 ETH from Uniswap/DEX (takes 5-10 minutes)
4. Executes Murabaha with borrower
5. Borrower waits briefly but gets better price execution

### 5.4 Asset Acquisition Process

**Example: Buying ETH for Inventory**

1. **Trigger:** ETH inventory drops to 180 ETH (below 200 min)

2. **Calculate purchase amount:**
   - Target: 400 ETH (80% of 500 target)
   - Need to buy: 220 ETH

3. **Check Mudarabah pool availability:**
   - Current USDC available: $2M
   - ETH price: $2,000
   - Cost: 220 ETH × $2,000 = $440K ✅ Available

4. **Execute purchase:**
   - Protocol pulls $440K USDC from pools
   - Swaps via Uniswap/1inch (best execution)
   - Receives 220 ETH
   - Deposits into ETH Inventory Pool

5. **Record cost basis:**
   - Cost: $440,000 / 220 ETH = $2,000 per ETH
   - This becomes the "cost price" for future Murabaha sales
   - Markup will be added on top

6. **Update accounting:**
   - Protocol now OWNS 400 ETH
   - Inventory value: $800K
   - Bears price risk on these assets

### 5.5 Ownership Risk Management

**The Risk:** Protocol owns volatile assets that can depreciate.

**Example of Loss:**
- Protocol buys 220 ETH @ $2,000 = $440K
- ETH drops to $1,800 within 2 weeks
- Inventory value: $396K
- Unrealized loss: $44K (10%)

**This loss is borne by:**
- Mudarabah investors (capital providers)
- Protocol (loses opportunity cost, reputation)

**Mitigation Strategies:**

1. **Velocity Targeting:**
   - Target 30-day inventory turnover
   - Assets should be sold via Murabaha within 30 days of purchase
   - Reduces holding period risk

2. **Hedging (Shariah-Compliant):**
   - Convert 30% of inventory to thUSD during high volatility
   - Use Tharwa's own stablecoin for hedging
   - Maintain 70/30 volatile/stable inventory ratio in volatile markets

3. **Dynamic Markup Adjustment:**
   - Higher volatility → higher markup to compensate for risk
   - ETH volatility spikes → increase markup from 6% to 8%

4. **Inventory Caps:**
   - Never exceed max inventory levels
   - Limits total exposure
   - Example: Max 1,000 ETH = max $2M exposure @ $2,000/ETH

---

## 6. Component C: Murabaha Execution Engine

### 6.1 Overview

The Murabaha Engine is the core of the **borrowing side**. It facilitates the sale of Protocol-owned crypto assets to borrowers with deferred payment terms.

**Shariah Structure:**
- Protocol owns the asset (purchased from inventory)
- Protocol sells asset to borrower at **cost + markup**
- Borrower receives asset immediately
- Borrower repays in **stablecoins** (USDC) via installments
- Collateral ensures repayment

### 6.2 Murabaha Process Flow

#### **Step 1: Borrower Request**

Borrower specifies:
- Desired asset: "I want 10 ETH"
- Term: 90 days
- Collateral offered: 1 BTC

#### **Step 2: Cost Calculation**

Protocol calculates the **cost price** (what Protocol paid for the asset):

```
Asset: 10 ETH
Current inventory cost basis: $2,000/ETH
Cost Price = 10 ETH × $2,000 = $20,000
```

**Important:** Cost price is based on Protocol's ACTUAL purchase cost (FIFO accounting), not current market price.

#### **Step 3: Markup Calculation**

Protocol applies markup based on:
- Asset type (volatility tier)
- Term length
- Market conditions

**Markup Schedule:**

| Term | BTC/ETH (Low Risk) | DOT/SOL (Medium Risk) | Smaller Assets (High Risk) |
|------|--------------------|-----------------------|----------------------------|
| 30 days | 2% | 3% | 4% |
| 90 days | 6% | 7% | 10% |
| 180 days | 12% | 14% | 18% |

**Example:**
- Asset: ETH (low risk tier)
- Term: 90 days
- Markup: 6%
- Markup Amount = $20,000 × 6% = $1,200

#### **Step 4: Sale Price Determination**

```
Cost Price:    $20,000
Markup (6%):   $1,200
─────────────────────
Sale Price:    $21,200
```

**This is the total amount borrower must repay.**

#### **Step 5: Installment Schedule**

```
Term: 90 days
Monthly installments: 3
Installment amount: $21,200 / 3 = $7,067 USDC/month

Payment Schedule:
- Month 1: $7,067 USDC (due 30 days after execution)
- Month 2: $7,067 USDC (due 60 days after execution)
- Month 3: $7,066 USDC (due 90 days after execution, rounds to $21,200 total)
```

#### **Step 6: Collateral Lock**

Borrower must provide collateral worth **150% of sale price**:

```
Sale Price: $21,200
Required Collateral: $21,200 × 150% = $31,800

Borrower provides: 1 BTC @ $32,000 = $32,000 ✅ Sufficient
```

Collateral is locked in smart contract until full repayment.

#### **Step 7: Asset Transfer (Murabaha Sale)**

1. Protocol transfers 10 ETH from inventory to borrower's wallet
2. Borrower now OWNS the 10 ETH (can do whatever they want with it)
3. Murabaha agreement created on-chain
4. Repayment obligation: $21,200 USDC over 90 days

### 6.3 Key Shariah Compliance Points

**✅ Ownership:** Protocol owned the 10 ETH before selling (bought from market, held in inventory)

**✅ Cost Transparency:** Borrower knows exact cost price ($20,000) and markup ($1,200)

**✅ Different Assets:** Borrower receives ETH, repays USDC (no same-asset Riba)

**✅ Fixed Markup:** Markup is FIXED at time of agreement, doesn't compound or change

**✅ No Time Penalties:** If borrower repays early, NO penalty (Shariah requirement)

**❌ Would Violate Shariah:** If Protocol lent 10 ETH and asked for 12 ETH back (same asset Riba)

### 6.4 Early Repayment Policy

**Shariah Requirement:** Borrower can repay early WITHOUT penalty.

**Example:**
- Borrower executed 90-day Murabaha for $21,200
- After 45 days, borrower wants to repay early
- Borrower STILL owes full $21,200 (markup is NOT prorated)
- But no additional penalty for early exit

**Why borrower might still repay early:**
- To unlock collateral sooner
- Sold the ETH at profit, wants to exit position
- Needs the BTC collateral for other purposes

**Why markup isn't reduced:**
- Murabaha is a SALE, not a loan
- The $21,200 price was agreed at time of sale
- Similar to buying a house: if you pay mortgage off early, you still paid interest already accrued, but no future interest

### 6.5 Example: Complete Murabaha Execution

**Scenario:**

Bob wants to acquire 10 ETH. He has 1 BTC to use as collateral.

**Execution:**

```
1. Bob requests: "10 ETH, 90-day term"

2. Protocol calculates:
   Cost Price:     $20,000 (Protocol's acquisition cost)
   Markup (6%):    $1,200
   Sale Price:     $21,200
   Installments:   3 × $7,067/month

3. Bob provides collateral:
   Asset:          1 BTC
   Value:          $32,000 (as per Chainlink oracle)
   Collateral %:   151% ✅ (exceeds 150% minimum)

4. Bob signs Murabaha agreement (smart contract transaction)

5. Protocol executes:
   - Locks 1 BTC in CollateralManager contract
   - Transfers 10 ETH from inventory to Bob's wallet
   - Creates Murabaha Agreement #1234 on-chain
   - Sets next payment due: 30 days from now

6. Bob receives 10 ETH immediately
   - Can trade it, hold it, use it for yield farming, whatever

7. Payment Schedule Activated:
   - Day 30: Bob pays $7,067 USDC → Protocol treasury
   - Day 60: Bob pays $7,067 USDC → Protocol treasury
   - Day 90: Bob pays $7,066 USDC → Protocol treasury
   - Total paid: $21,200 USDC

8. Upon final payment:
   - CollateralManager releases 1 BTC back to Bob
   - Agreement marked as "Completed"
   - Protocol profit: $1,200 → Distributed to Mudarabah investors (75%) and Protocol (25%)
```

**Bob's Outcome:**
- Got 10 ETH immediately
- Paid $21,200 over 90 days
- Effective cost: 6% over 90 days = 24% annualized
- Recovered collateral after full repayment

**Protocol's Outcome:**
- Sold ETH from inventory
- Earned $1,200 markup
- Protocol share (25%): $300
- Investor share (75%): $900

---

## 7. Component D: Collateral Management

### 7.1 Overview

Collateral secures the borrower's repayment obligation. Since Murabaha is a **sale with deferred payment**, collateral ensures the buyer (borrower) fulfills their payment obligation.

### 7.2 Accepted Collateral Assets

**Designated Collateral Assets:**

| Asset | Accepted? | Min Collateralization | Liquidation Threshold | Risk Tier |
|-------|-----------|----------------------|-----------------------|-----------|
| BTC | ✅ Yes | 150% | 130% | Low |
| ETH | ✅ Yes | 150% | 130% | Low |
| DOT | ✅ Yes | 160% | 140% | Medium |
| SOL | ✅ Yes | 160% | 140% | Medium |
| MATIC | ✅ Yes | 170% | 150% | Medium-High |

**Why These Assets:**
- High liquidity (can be sold quickly if liquidation needed)
- Halal-certified by Shariah board
- Reliable price oracles available
- Deep markets on DEXs/CEXs

**NOT Accepted:**
- Stablecoins (defeats purpose of over-collateralization)
- Low-liquidity tokens (can't liquidate effectively)
- Haram-certified assets
- Algorithmic stablecoins (high depeg risk)

### 7.3 Collateralization Ratios

**Calculation:**

```
Collateral Ratio = (Collateral Value / Outstanding Debt) × 100%
```

**Example:**
- Borrower owes: $21,200 USDC
- Collateral: 1 BTC @ $32,000
- Collateral Ratio: ($32,000 / $21,200) × 100% = 151%

**Minimum Requirements:**

| Collateral Asset | Min at Opening | Liquidation Threshold | Buffer |
|------------------|----------------|----------------------|--------|
| BTC | 150% | 130% | 20% |
| ETH | 150% | 130% | 20% |
| DOT | 160% | 140% | 20% |
| SOL | 160% | 140% | 20% |

**Buffer:** The difference between minimum and liquidation threshold provides room for price volatility before liquidation.

### 7.4 Collateral States

#### **State 1: Healthy** (Above Min Ratio)

```
Collateral Ratio: ≥150% (for BTC/ETH)
Status: ✅ Healthy
Actions: None required
User Experience: Normal
```

#### **State 2: Warning** (Between Liquidation and Min)

```
Collateral Ratio: 130-150% (for BTC/ETH)
Status: ⚠️ Warning
Actions:
  - User notified (email, in-app notification)
  - Encouraged to add collateral or repay debt
User Experience: Warning displayed in dashboard
```

#### **State 3: Liquidation** (Below Threshold)

```
Collateral Ratio: <130% (for BTC/ETH)
Status: 🔴 Liquidatable
Actions:
  - Liquidation can be triggered by anyone (keepers/bots)
  - Collateral seized and sold
  - Debt repaid from proceeds
User Experience: Account liquidated
```

### 7.5 Collateral Top-Up & Withdrawal

#### **Adding Collateral**

Borrower can add collateral anytime to improve health ratio:

```
function addCollateral(uint256 agreementId, uint256 amount) external {
    // Transfer additional collateral from user
    // Update agreement collateral amount
    // Improve collateral ratio
}
```

**Use Case:**
- Bob's collateral dropped to 135% due to BTC price decline
- Bob adds 0.1 BTC more
- New collateral: 1.1 BTC @ $32K = $35,200
- New ratio: 166% ✅ Back to healthy

#### **Withdrawing Excess Collateral**

If collateral ratio is very high, borrower can withdraw excess:

```
Current: 1.5 BTC @ $48,000 = $72,000 collateral
Debt: $21,200
Ratio: 340% (far above 150% minimum)

Borrower can withdraw: Up to a level that maintains 150%+buffer
Max withdrawal: Keep collateral at 160% = $33,920
Excess: $38,080 → Can withdraw ~0.8 BTC
```

**Important:** Withdrawal must maintain AT LEAST min ratio + 5% buffer.

### 7.6 Multi-Collateral Support

Borrowers can provide multiple assets as collateral:

**Example:**
- Debt: $21,200
- Required: $31,800 (150%)
- Borrower provides:
  - 0.5 BTC @ $32K = $16,000
  - 10 ETH @ $2K = $20,000
  - Total: $36,000 ✅ 170% collateralization

**Benefits:**
- Diversification (reduces single-asset risk)
- More flexible for users
- Can use idle assets

**Implementation:**
- Each collateral asset tracked separately
- Combined value calculated via price oracles
- Liquidation can seize one or all assets

---

## 8. Component E: Liquidation Engine

### 8.1 Overview

Liquidation protects the protocol and Mudarabah investors when a borrower's collateral value drops below safe thresholds or when borrower defaults on payments.

**Purpose:**
- Recover outstanding debt
- Minimize losses to investors
- Maintain protocol solvency
- Incentivize timely repayment

### 8.2 Liquidation Triggers

#### **Trigger 1: Collateral Depreciation**

```
IF Collateral Ratio < Liquidation Threshold:
    → Liquidation eligible

Example:
- Debt: $21,200
- Collateral: 1 BTC
- BTC price drops: $32,000 → $27,000
- New ratio: ($27,000 / $21,200) = 127% < 130% ❌
- LIQUIDATION TRIGGERED
```

#### **Trigger 2: Payment Default**

```
IF Borrower misses 2 consecutive installment payments:
    → Liquidation eligible

Example:
- Bob misses Month 1 payment (Day 30)
- Bob misses Month 2 payment (Day 60)
- After Day 60+7 days grace period: LIQUIDATION TRIGGERED
```

**Grace Period:** 7 days after missed payment before liquidation can be triggered for payment default.

### 8.3 Liquidation Process

**Step-by-Step:**

```
1. DETECTION
   - Keeper bot monitors collateral ratios
   - Detects Agreement #1234: 127% ratio < 130% threshold

2. LIQUIDATION TRANSACTION
   - Keeper calls liquidate(agreementId)
   - Smart contract verifies liquidation conditions
   - Proceeds with liquidation

3. COLLATERAL SEIZURE
   - Collateral already in contract custody
   - Now formally transferred to LiquidationEngine

4. ASSET SALE
   - LiquidationEngine swaps collateral for USDC
   - Uses DEX aggregators (1inch, Uniswap) for best price
   - Example: Sells 1 BTC for $27,000 USDC

5. PROCEEDS DISTRIBUTION
   Calculate:
   - Outstanding debt: $21,200 (amount borrower still owed)
   - Liquidation penalty: 5% of debt = $1,060
   - Total claim: $22,260
   - Sale proceeds: $27,000
   - Excess: $4,740

   Distribute:
   - Debt repayment: $21,200 → Mudarabah pools
   - Liquidation penalty: $1,060 → Split:
     - 50% to Protocol ($530)
     - 50% to Investors ($530)
   - Excess collateral: $4,740 → Returned to borrower

6. AGREEMENT CLOSURE
   - Mark agreement as "Liquidated"
   - Release all claims
   - Emit Liquidation event
```

### 8.4 Liquidation Penalties

**Penalty Structure:**

| Collateral Asset | Liquidation Penalty | Distribution |
|------------------|---------------------|--------------|
| BTC | 5% of outstanding debt | 50% Protocol, 50% Investors |
| ETH | 5% of outstanding debt | 50% Protocol, 50% Investors |
| DOT | 7% of outstanding debt | 50% Protocol, 50% Investors |
| SOL | 7% of outstanding debt | 50% Protocol, 50% Investors |

**Purpose of Penalty:**
- Incentivizes borrowers to maintain healthy ratios
- Compensates protocol for liquidation costs (gas, slippage)
- Compensates investors for risk

**Example:**
```
Outstanding Debt: $21,200
Penalty (5%): $1,060

Distribution:
- Protocol: $530 (covers gas, keeper incentive, profit)
- Investors: $530 (additional yield)
```

### 8.5 Keeper Incentives

Liquidations are executed by external **keepers** (bots/users who monitor and trigger liquidations).

**Keeper Reward:**

```
Keeper receives: 2% of liquidation penalty
Example: $1,060 penalty × 2% = $21.20 keeper reward
```

**Remaining penalty split:**
```
Protocol: 48% × $1,060 = $509
Investors: 50% × $1,060 = $530
```

**Why keepers participate:**
- Automated profit opportunity
- No capital required (just gas)
- Competitive market ensures liquidations happen quickly

### 8.6 Partial Liquidations

For very large positions, we support **partial liquidation** to minimize impact:

```
Debt: $100,000
Collateral: 5 BTC @ $27,000 = $135,000
Ratio: 135% (just below 150% healthy, but above 130% liquidation)

Instead of liquidating entire position:
→ Liquidate 1 BTC to bring ratio back to 150%

After partial liquidation:
- Sell 1 BTC for $27,000
- Repay $20,000 of debt
- Remaining debt: $80,000
- Remaining collateral: 4 BTC @ $27,000 = $108,000
- New ratio: 135% → 150% ✅
```

**Benefits:**
- Less disruptive for borrower
- Maintains user relationship
- Reduces slippage on large liquidations

### 8.7 Excess Collateral Return

**Shariah Requirement:** If collateral sale proceeds exceed debt + penalty, excess MUST be returned to borrower.

**Example:**
```
Debt: $21,200
Penalty: $1,060
Total Claim: $22,260

Collateral sold for: $27,000

Excess: $27,000 - $22,260 = $4,740
→ Returned to borrower's wallet automatically
```

This is both Shariah-compliant and ethically important—we only claim what's owed.

### 8.8 Bad Debt Handling

**Scenario:** Collateral value is insufficient to cover debt.

**Example:**
```
Debt: $21,200
Collateral: 1 BTC @ $20,000 (flash crash)
Ratio: 94% 🔴

Liquidation:
- Sell 1 BTC for $20,000
- Debt owed: $21,200
- Shortfall: $1,200 (bad debt)
```

**Protocol Response:**

1. **Insurance Fund:** First line of defense
   - Protocol maintains insurance fund (5% of profits)
   - Covers shortfall from insurance
   - Target: Insurance fund = 10% of TVL

2. **Socialized Loss:** If insurance insufficient
   - Loss distributed among Mudarabah investors
   - Proportional to pool stake
   - Example: $1,200 loss / $50M TVL = 0.0024% haircut

**Important:** This is Shariah-compliant because investors are PARTNERS (Mudarabah), not lenders. They share in losses.

---

## 9. Component F: Shariah Governance

### 9.1 Overview

The Shariah Governance Board ensures the protocol maintains continuous compliance with Islamic finance principles.

**Composition:**
- 3-5 qualified Islamic scholars
- Expertise in Islamic finance, blockchain, and contemporary jurisprudence
- Independent (not employed by protocol, compensated via grants)

### 9.2 Responsibilities

#### **1. Asset Certification**

Review and certify crypto assets as halal/haram:

**Evaluation Criteria:**
```
✅ HALAL if:
   - Decentralized, permissionless infrastructure
   - Real utility (not pure speculation)
   - No involvement in prohibited activities
   - Transparent, auditable code
   - Legitimate use cases

❌ HARAM if:
   - Used primarily for gambling (casino tokens)
   - Associated with interest-bearing protocols
   - Privacy-focused for illicit activities (to avoid justice)
   - Ponzi/pyramid scheme dynamics
   - No real utility (pure meme/speculation)

⚠️ REQUIRES MONITORING:
   - Governance tokens (depends on protocol)
   - Staking rewards (must verify no Riba)
   - Wrapped assets (depends on backing)
```

**Example Decisions:**
- **Bitcoin (BTC):** ✅ Halal - Decentralized, store of value, legitimate use
- **Ethereum (ETH):** ✅ Halal - Smart contract platform, real utility
- **AAVE Token:** ❌ Haram - Governance of interest-based lending protocol
- **Monero (XMR):** ❌ Haram - Privacy coin facilitating illicit use
- **Shiba Inu (SHIB):** ❌ Haram - Pure speculation, no utility (Maysir)

#### **2. Protocol Review**

Quarterly audits of protocol mechanisms:

**Review Areas:**
- Mudarabah pool structures (still compliant?)
- Murabaha execution (proper ownership, markup transparency?)
- Profit distribution (fair, accurate?)
- No Riba introduction (interest-like mechanisms?)
- No Gharar (excessive uncertainty?)

**Deliverable:** Shariah Audit Report (published on-chain + website)

#### **3. FATWA Issuance**

Issue religious rulings on new features or edge cases:

**Example FATWAs:**
```
Q: Can we offer flash Murabaha (same-day term)?
FATWA: Permissible, as long as markup is fixed and ownership transfer occurs.

Q: Can borrowers use acquired crypto for yield farming?
FATWA: Permissible if yield farming protocol itself is halal. Borrower's responsibility.

Q: Can we accept NFTs as collateral?
FATWA: Requires case-by-case evaluation. Halal NFTs (art, utility) acceptable. Haram NFTs (gambling) not acceptable.
```

#### **4. Purification Process**

If any revenue is determined to be haram (post-facto):

**Process:**
1. Identify haram revenue source
2. Calculate exact amount
3. Immediately donate to registered charity
4. Publish purification report on-chain
5. Adjust protocol to prevent recurrence

**Example:**
```
Situation: Protocol unknowingly accepted AAVE token as collateral
Amount: Earned $5,000 from liquidating AAVE collateral
Resolution:
   - $5,000 donated to Islamic Relief
   - AAVE removed from accepted collateral list
   - On-chain purification record: TX 0x123abc...
```

### 9.3 Shariah Oracle (Smart Contract)

**On-chain registry of halal/haram assets:**

The Shariah Oracle is a smart contract that maintains the certification status of all crypto assets. Only Shariah Board members can certify or revoke asset certifications.

**Key Features:**
- **Certification Statuses:** NotReviewed, Halal, Haram, UnderReview, RequiresMonitoring
- **Expiry-based:** Certifications expire after 365 days (annual recertification required)
- **IPFS Integration:** Each certification links to detailed FATWA document on IPFS
- **Multi-signature:** Multiple scholars must sign off on certifications
- **Immutable History:** All certification changes recorded on-chain

**Data Structure:**
```solidity
struct AssetCertification {
    address assetAddress;
    CertificationStatus status;
    uint256 certificationDate;
    uint256 expiryDate;
    string fatwahIPFS;       // IPFS link to FATWA document
    address[] certifiedBy;   // Scholar addresses who signed
}
```

**Usage Throughout Protocol:**

The protocol automatically checks asset certification before critical operations:

```solidity
// Before accepting collateral
require(shariahOracle.isAssetHalal(collateralToken), "Collateral not halal-certified");

// Before adding to inventory
require(shariahOracle.isAssetHalal(assetAddress), "Cannot acquire haram asset");

// Before executing Murabaha
require(shariahOracle.isAssetHalal(assetType), "Asset not Shariah-certified");
```

See **Section 10.3** for full `IShariahOracle` interface specification.

### 9.4 Annual Recertification

All assets must be recertified annually:

**Process:**
1. Shariah board reviews asset status (any changes in last year?)
2. Checks: New use cases? Association with haram activities? Community concerns?
3. Decision: Renew certification, Revoke, or Monitor
4. Update Shariah Oracle on-chain

**Example:**
```
Asset: Solana (SOL)
Initial Certification: Jan 2025 - Halal
Annual Review: Jan 2026
Findings:
   - Solana ecosystem now hosts gambling DApps
   - SOL itself still has utility beyond gambling
   - But association raises concerns
Decision:
   - Maintain Halal status
   - Add "Requires Monitoring" flag
   - Re-review in 6 months
```

### 9.5 Community Input

Users can submit concerns for board review:

**Submission Process:**
1. User submits concern via governance forum
2. Example: "Protocol X (which uses our liquidity) is offering interest-based products"
3. Shariah board reviews within 30 days
4. Issues response + FATWA if needed
5. Protocol adjusts if necessary

---

## 10. Smart Contract Architecture

### 10.1 Contract Overview

```
TharwaShariahLending (Main Protocol Contract)
│
├─── MudarabahPoolFactory
│    ├─── MudarabahPool30Day (ERC-4626 Vault)
│    ├─── MudarabahPool90Day (ERC-4626 Vault)
│    ├─── MudarabahPool180Day (ERC-4626 Vault)
│    └─── FlexiblePool (ERC-4626 Vault)
│
├─── AssetInventoryManager
│    ├─── BTCInventoryPool
│    ├─── ETHInventoryPool
│    ├─── DOTInventoryPool
│    └─── SOLInventoryPool
│
├─── MurabahaEngine
│    ├─── createMurabaha()
│    ├─── makePayment()
│    ├─── earlyRepayment()
│    └─── MurabahaAgreement[] (state)
│
├─── CollateralManager
│    ├─── lockCollateral()
│    ├─── addCollateral()
│    ├─── withdrawExcess()
│    ├─── getCollateralRatio()
│    └─── calculateLiquidationThreshold()
│
├─── LiquidationEngine
│    ├─── liquidate()
│    ├─── partialLiquidate()
│    └─── KeeperIncentives
│
├─── ProfitDistributor
│    ├─── distributeMonthly()
│    ├─── calculateShares()
│    └─── claimProfits()
│
├─── PriceOracle (Chainlink Integration)
│    ├─── getPrice()
│    └─── Asset/USD Price Feeds
│
└─── ShariahOracle
     ├─── isAssetHalal()
     ├─── certifyAsset()
     └─── AssetCertification[]
```

### 10.2 Core Contract Prototypes

#### **MurabahaEngine Contract**

**Purpose:** Manages Murabaha asset sale agreements between Protocol and borrowers.

**Key Data Structures:**

```solidity
enum AssetType { BTC, ETH, DOT, SOL, MATIC }
enum AgreementStatus { Active, Completed, Liquidated, Defaulted }

struct MurabahaAgreement {
    uint256 agreementId;
    address borrower;
    AssetType assetType;
    uint256 assetAmount;
    uint256 costPrice;          // What Protocol paid
    uint256 markup;             // Markup amount
    uint256 salePrice;          // Total owed
    uint256 installmentAmount;
    uint256 installmentsTotal;
    uint256 installmentsPaid;
    address collateralToken;
    uint256 collateralAmount;
    uint256 executionDate;
    uint256 maturityDate;
    AgreementStatus status;
}
```

**Core Functions:**

```solidity
interface IMurabahaEngine {
    // Execute new Murabaha agreement
    function executeMurabaha(
        AssetType assetType,
        uint256 assetAmount,
        uint256 termDays,
        address collateralToken,
        uint256 collateralAmount
    ) external returns (uint256 agreementId);

    // Make installment payment
    function makePayment(uint256 agreementId) external;

    // Early full repayment (no penalty)
    function earlyRepayment(uint256 agreementId) external;

    // Get agreement details
    function getAgreement(uint256 agreementId)
        external view returns (MurabahaAgreement memory);

    // Calculate pricing for quote
    function calculatePricing(
        AssetType assetType,
        uint256 assetAmount,
        uint256 termDays
    ) external view returns (
        uint256 costPrice,
        uint256 markup,
        uint256 salePrice
    );
}
```

**Key Events:**

```solidity
event MurabahaExecuted(
    uint256 indexed agreementId,
    address indexed borrower,
    AssetType assetType,
    uint256 assetAmount,
    uint256 salePrice
);

event PaymentMade(
    uint256 indexed agreementId,
    uint256 installmentNumber,
    uint256 amount
);

event AgreementCompleted(uint256 indexed agreementId);
event EarlyRepayment(uint256 indexed agreementId, uint256 amountPaid);
```

**Implementation Notes:**
- Uses OpenZeppelin's `AccessControl`, `ReentrancyGuard`, `Pausable`
- Integrates with `IAssetInventory`, `ICollateralManager`, `IPriceOracle`, `IShariahOracle`
- Markup schedule stored in mapping: `AssetType => TermDays => BasisPoints`
- All agreements tracked in mapping: `agreementId => MurabahaAgreement`

---

#### **MudarabahPool Contract**

**Purpose:** ERC-4626 vault for stablecoin deposits with profit-sharing.

**Core Functions:**

```solidity
interface IMudarabahPool {
    // ERC-4626 Standard Functions
    function deposit(uint256 assets, address receiver)
        external returns (uint256 shares);

    function withdraw(uint256 assets, address receiver, address owner)
        external returns (uint256 shares);

    function redeem(uint256 shares, address receiver, address owner)
        external returns (uint256 assets);

    // Custom Functions
    function distributeProfits(uint256 profitAmount) external;

    function getMaturityDate(address investor)
        external view returns (uint256);

    function canWithdraw(address investor)
        external view returns (bool);
}
```

---

#### **AssetInventoryManager Contract**

**Purpose:** Manages Protocol-owned volatile asset inventory.

**Core Functions:**

```solidity
interface IAssetInventory {
    // Check inventory availability
    function hasBalance(AssetType assetType, uint256 amount)
        external view returns (bool);

    // Get cost basis for FIFO accounting
    function getCostBasis(AssetType assetType, uint256 amount)
        external view returns (uint256);

    // Transfer asset to borrower (Murabaha sale)
    function transferAsset(AssetType assetType, uint256 amount, address to)
        external;

    // Acquire assets from market
    function buyAsset(AssetType assetType, uint256 amount)
        external returns (uint256 costBasis);

    // Get inventory status
    function getInventoryStatus(AssetType assetType)
        external view returns (
            uint256 currentBalance,
            uint256 targetBalance,
            uint256 averageCost,
            uint256 unrealizedPnL
        );
}
```

---

#### **CollateralManager Contract**

**Purpose:** Manages borrower collateral with health monitoring.

**Core Functions:**

```solidity
interface ICollateralManager {
    // Lock collateral for agreement
    function lockCollateral(
        uint256 agreementId,
        address borrower,
        address token,
        uint256 amount
    ) external;

    // Release collateral after full repayment
    function releaseCollateral(uint256 agreementId, address to) external;

    // Add more collateral to improve health
    function addCollateral(uint256 agreementId, uint256 amount) external;

    // Withdraw excess collateral
    function withdrawExcess(uint256 agreementId, uint256 amount) external;

    // Get collateral ratio
    function getCollateralRatio(uint256 agreementId)
        external view returns (uint256 ratio);

    // Check if liquidatable
    function isLiquidatable(uint256 agreementId)
        external view returns (bool);

    // Get minimum collateral required
    function getMinCollateral(address token, uint256 debt)
        external view returns (uint256);
}
```

---

#### **LiquidationEngine Contract**

**Purpose:** Handles under-collateralized position liquidations.

**Core Functions:**

```solidity
interface ILiquidationEngine {
    // Liquidate position
    function liquidate(uint256 agreementId)
        external returns (uint256 proceeds);

    // Partial liquidation
    function partialLiquidate(uint256 agreementId, uint256 amount)
        external returns (uint256 proceeds);

    // Check if agreement can be liquidated
    function canLiquidate(uint256 agreementId)
        external view returns (bool, string memory reason);

    // Get liquidation preview
    function previewLiquidation(uint256 agreementId)
        external view returns (
            uint256 collateralToSell,
            uint256 estimatedProceeds,
            uint256 debtToRepay,
            uint256 penaltyAmount,
            uint256 excessToReturn
        );
}
```

---

### 10.3 Supporting Contract Interfaces

#### **PriceOracle Contract**

**Purpose:** Provides reliable price feeds for all assets using Chainlink.

```solidity
interface IPriceOracle {
    // Get USD value of token amount
    function getValue(address token, uint256 amount)
        external view returns (uint256 valueUSD);

    // Get current price per token
    function getPrice(address token)
        external view returns (uint256 priceUSD);

    // Get historical price (for inventory cost basis)
    function getHistoricalPrice(address token, uint256 timestamp)
        external view returns (uint256 priceUSD);
}
```

---

#### **ShariahOracle Contract**

**Purpose:** On-chain registry of halal/haram certified assets.

```solidity
interface IShariahOracle {
    enum CertificationStatus {
        NotReviewed,
        Halal,
        Haram,
        UnderReview,
        RequiresMonitoring
    }

    struct AssetCertification {
        address assetAddress;
        CertificationStatus status;
        uint256 certificationDate;
        uint256 expiryDate;
        string fatwahIPFS;  // IPFS link to FATWA
        address[] certifiedBy;
    }

    // Check if asset is halal-certified
    function isAssetHalal(address asset)
        external view returns (bool);

    // Get full certification details
    function getCertification(address asset)
        external view returns (AssetCertification memory);

    // Certify asset (Shariah board only)
    function certifyAsset(
        address asset,
        CertificationStatus status,
        string calldata fatwahIPFS
    ) external;

    // Revoke certification
    function revokeCertification(address asset) external;
}
```

---

#### **ProfitDistributor Contract**

**Purpose:** Distributes Murabaha profits to Mudarabah pool investors.

```solidity
interface IProfitDistributor {
    // Add profit from Murabaha sale
    function addMurabahaProfit(uint256 amount) external;

    // Add profit from liquidation penalty
    function addLiquidationProfit(uint256 amount) external;

    // Execute monthly distribution to all pools
    function distributeMonthly() external;

    // Calculate investor's share
    function calculateInvestorShare(address investor, address pool)
        external view returns (uint256 shareAmount);

    // Claim accumulated profits
    function claimProfits(address pool) external;
}
```

---

## 11. Key User Workflows

### 11.1 Workflow 1: Investor Deposits into Mudarabah Pool

**User Story:** Alice wants to earn halal returns on her $100,000 USDC.

**Steps:**

1. **Visit Protocol dApp**
   - Navigate to "Invest" tab
   - See available Mudarabah pools with APYs

2. **Select Pool**
   - Reviews options:
     - 30-Day: 5.2% APY
     - 90-Day: 8.1% APY ← Alice selects this
     - 180-Day: 12.3% APY
     - Flexible: 3.5% APY

3. **Understand Terms**
   - Reads Mudarabah agreement:
     - "You are entering an investment partnership (Mudarabah)"
     - "Protocol will deploy your capital to acquire and trade halal assets"
     - "Profits shared 75% to you, 25% to Protocol"
     - "You share in losses if Protocol makes poor decisions"
     - "Locked for 90 days - no early withdrawal"

4. **Deposit**
   - Approves USDC spend (ERC-20 approval)
   - Deposits 100,000 USDC
   - Transaction confirmed

5. **Receive Receipt Tokens**
   - Receives 100,000 mdUSDC-90 tokens (Mudarabah vault shares)
   - These represent her proportional ownership in the 90-day pool

6. **Monitor Investment**
   - Dashboard shows:
     - Invested: 100,000 USDC
     - Current Pool Size: $25M
     - Your Share: 0.4%
     - Earned So Far: $3,250 (updated monthly)
     - Maturity Date: 90 days from now
     - Projected Return: $8,100 (8.1%)

7. **Maturity & Withdrawal**
   - After 90 days, "Withdraw" button becomes active
   - Alice redeems 100,000 mdUSDC-90 tokens
   - Receives: 108,100 USDC (principal + profit)
   - Can re-invest or withdraw to wallet

---

### 11.2 Workflow 2: Borrower Acquires Crypto via Murabaha

**User Story:** Bob wants to acquire 10 ETH for trading/holding. He has 1 BTC as collateral.

**Steps:**

1. **Visit Protocol dApp**
   - Navigate to "Borrow" tab
   - See available assets: BTC, ETH, DOT, SOL

2. **Configure Murabaha Request**
   - Select Asset: ETH
   - Amount: 10 ETH
   - Term: 90 days

3. **View Pricing**
   - System calculates and displays:
     ```
     Asset: 10 ETH
     Cost Price: $20,000 (Protocol's cost)
     Markup (6%): $1,200
     ────────────────────
     Sale Price: $21,200

     Payment Terms:
     - 3 monthly installments
     - $7,067 USDC per month
     - First payment due: 30 days after execution
     ```

4. **Provide Collateral**
   - System shows collateral requirement:
     ```
     Required Collateral: $31,800 (150% of sale price)

     Your Collateral:
     Asset: BTC
     Amount: 1 BTC
     Current Value: $32,000 ✅ Sufficient
     Collateral Ratio: 151%
     ```

5. **Review Murabaha Agreement**
   - Reads key terms:
     - "Protocol is selling you 10 ETH for $21,200"
     - "You will repay in USDC (not ETH) over 90 days"
     - "Your 1 BTC collateral will be locked until full repayment"
     - "No penalty for early repayment"
     - "If collateral drops below 130% ratio, liquidation may occur"

6. **Execute Transaction**
   - Approves BTC spend (transfer collateral)
   - Signs Murabaha agreement (smart contract)
   - Transaction confirmed

7. **Receive Asset**
   - 10 ETH instantly transferred to Bob's wallet
   - Bob can now use ETH however he wants (trade, hold, yield farm)
   - Agreement #1234 created on-chain

8. **Dashboard Shows Active Agreement**
   ```
   Agreement #1234
   ──────────────────────────
   Asset Received: 10 ETH
   Total Owed: $21,200 USDC

   Payment Schedule:
   ✅ Payment 1: $7,067 (paid)
   ⏳ Payment 2: $7,067 (due in 15 days)
   ⏳ Payment 3: $7,066 (due in 45 days)

   Collateral:
   Asset: 1 BTC
   Current Value: $32,000
   Ratio: 151% ✅ Healthy
   ```

9. **Make Monthly Payments**
   - Every 30 days, Bob approves and pays $7,067 USDC
   - System auto-updates agreement status
   - After payment 2: "1 payment remaining"

10. **Final Payment & Collateral Release**
    - Bob makes 3rd payment: $7,066 USDC
    - Agreement marked "Completed"
    - 1 BTC collateral automatically released to Bob's wallet
    - Bob keeps the 10 ETH he received initially

**Bob's Net Position:**
- Received: 10 ETH (Day 1)
- Paid: $21,200 USDC (over 90 days)
- Effective cost: 6% over 90 days = ~24% annualized
- Got access to ETH liquidity without selling his BTC

---

### 11.3 Workflow 3: Protocol Builds Asset Inventory

**Internal Process:** Protocol maintains inventory of volatile assets to fulfill Murabaha requests.

**Steps:**

1. **Monitor Inventory Levels**
   - Automated system checks inventory every hour
   - Example check:
     ```
     ETH Inventory:
     Current: 180 ETH
     Target: 400 ETH (80% of 500 target)
     Min: 200 ETH
     Status: 🟡 Below target, above minimum
     ```

2. **Trigger Rebalancing**
   - System determines: Need to buy 220 ETH
   - Cost: 220 ETH × $2,000 = $440,000 USDC

3. **Check Mudarabah Pool Availability**
   - Query available USDC in pools:
     ```
     Total TVL: $50M
     Deployed: $35M (70%)
     Available: $15M ✅ Sufficient for $440K purchase
     ```

4. **Execute Purchase**
   - Smart contract pulls $440K USDC from Mudarabah pools
   - Routes through DEX aggregator (1inch) for best execution
   - Buys 220 ETH @ average $2,000/ETH
   - Total cost: $440,000

5. **Add to Inventory**
   - 220 ETH deposited into ETH Inventory Pool
   - Cost basis recorded: $2,000/ETH
   - This will be used for future Murabaha cost calculations

6. **Update Inventory Status**
   ```
   ETH Inventory:
   Current: 400 ETH ✅ At target
   Cost Basis: $2,000/ETH (FIFO)
   Total Value: $800,000
   Status: 🟢 Healthy
   ```

7. **Risk Monitoring**
   - Protocol now bears $800K exposure to ETH price volatility
   - If ETH drops to $1,800:
     - Inventory value: $720K
     - Unrealized loss: $80K (10%)
     - This loss borne by Mudarabah investors (capital providers)

---

### 11.4 Workflow 4: Liquidation Event

**Scenario:** Bob's collateral value drops due to BTC price decline.

**Timeline:**

**Day 1:** Agreement executed
```
Debt: $21,200
Collateral: 1 BTC @ $32,000
Ratio: 151% ✅ Healthy
```

**Day 15:** BTC price drops
```
Debt: $21,200 (after 1 payment, 2 remaining = $14,133)
Collateral: 1 BTC @ $28,000
Ratio: 198% ✅ Still healthy
```

**Day 20:** BTC flash crashes
```
Debt: $14,133 (2 payments remaining)
Collateral: 1 BTC @ $18,000
Ratio: 127% 🔴 Below 130% threshold
LIQUIDATION TRIGGERED
```

**Liquidation Process:**

1. **Keeper Bot Detects**
   - Off-chain keeper monitoring system detects ratio < 130%
   - Calls `liquidate(agreementId: 1234)`

2. **Smart Contract Verification**
   - Contract verifies:
     - Collateral ratio is indeed below 130% ✅
     - OR borrower missed 2 payments ✅
   - Liquidation conditions met

3. **Collateral Seizure**
   - 1 BTC already in CollateralManager contract
   - Formally transferred to LiquidationEngine

4. **Sell Collateral**
   - LiquidationEngine swaps 1 BTC for USDC via 1inch
   - Execution: 1 BTC → $18,000 USDC (market price)

5. **Distribute Proceeds**
   ```
   Proceeds from sale: $18,000

   Distribution:
   1. Outstanding Debt: $14,133 → To Mudarabah pools
   2. Liquidation Penalty (5%): $707 → Split:
      - 50% Protocol: $353
      - 50% Investors: $354
   3. Keeper Reward (2% of penalty): $14 → To keeper bot
   4. Excess Collateral: $18,000 - $14,840 = $3,160 → Returned to Bob

   Final Distribution:
   - Mudarabah Pools: $14,487 ($14,133 debt + $354 penalty share)
   - Protocol: $353 (penalty share)
   - Keeper: $14 (incentive)
   - Bob (borrower): $3,160 (excess collateral returned)
   ```

6. **Agreement Closure**
   - Agreement #1234 marked as "Liquidated"
   - Bob's dashboard shows:
     ```
     Agreement #1234: LIQUIDATED
     - Collateral sold: 1 BTC for $18,000
     - Debt repaid: $14,133
     - Returned to you: $3,160
     ```

7. **Notifications**
   - Bob receives notification: "Your agreement was liquidated due to low collateral ratio. Excess collateral has been returned to your wallet."

---

## 12. Risk Management Framework

### 12.1 Risk Categories

The protocol faces five primary risk categories:

1. **Inventory Risk** - Protocol holds volatile assets
2. **Default Risk** - Borrowers fail to repay
3. **Liquidity Risk** - Investors want to withdraw simultaneously
4. **Smart Contract Risk** - Bugs, exploits, vulnerabilities
5. **Shariah Compliance Risk** - Inadvertent violation of principles

---

### 12.2 Inventory Risk Management

**Risk:** Protocol owns volatile crypto assets that may depreciate before being sold via Murabaha.

**Example:**
```
Protocol buys: 500 ETH @ $2,000 = $1M
ETH drops to: $1,800
Inventory value: $900K
Unrealized loss: $100K (10%)
```

**Who bears this loss:** Mudarabah investors (capital providers) - this is a core Mudarabah principle.

#### **Mitigation Strategies:**

**1. Inventory Velocity Targeting**
```
Target: 30-day inventory turnover
Goal: Assets should be sold via Murabaha within 30 days of purchase

Example:
- Buy 500 ETH on Day 1
- Sell via Murabaha by Day 30
- Limits price exposure window to 30 days
```

**2. Dynamic Inventory Caps**
```
Max exposure per asset = 20% of total Mudarabah TVL

Example:
- Total TVL: $50M
- Max ETH exposure: $10M
- If ETH @ $2,000: Max 5,000 ETH inventory
```

**3. Volatility-Adjusted Markups**
```
Higher volatility → Higher markup to compensate risk

Standard markup (ETH, 90-day): 6%
Volatile market (VIX-equivalent >30): 8%
Extreme volatility (>50): 10%
```

**4. Hedging Strategy (Shariah-Compliant)**
```
During high volatility periods:
- Convert 30% of volatile inventory to thUSD
- Maintain 70/30 volatile/stable ratio
- Reduces downside exposure
- Still allows upside participation
```

**5. Just-In-Time Purchasing**
```
For large orders (>$100K):
- Don't pre-buy inventory
- Buy on-demand when borrower commits
- Reduces holding period to minutes instead of days
- User waits 5-10 minutes for execution
```

---

### 12.3 Default Risk Management

**Risk:** Borrower stops making installment payments despite having collateral.

#### **Mitigation:**

**1. Over-Collateralization**
```
Min ratio: 150%
Example:
- Debt: $20,000
- Collateral: $30,000
- Buffer: 50% cushion for price volatility
```

**2. Two-Tier Warning System**
```
Tier 1 - Warning (140-150% ratio):
  - User notified via email + in-app
  - Suggested actions: Add collateral or repay early
  - No penalties yet

Tier 2 - Critical (130-140% ratio):
  - Urgent notifications
  - 24-hour grace period to add collateral
  - After grace period: Liquidation enabled
```

**3. Payment Default Tracking**
```
After 1 missed payment:
  - Warning notification
  - 7-day grace period
  - Late fee: None (not allowed in Shariah)

After 2 missed payments:
  - Liquidation becomes eligible
  - Collateral can be seized and sold
```

**4. Credit Score System (Future)**
```
Track on-chain repayment history:
- Perfect payment history: Lower markups (5% instead of 6%)
- 1 late payment: Standard markups
- 2+ late payments or liquidation: Higher markups (8%) or denied
```

---

### 12.4 Liquidity Risk Management

**Risk:** Too many investors want to withdraw from Mudarabah pools simultaneously, but capital is deployed in Murabaha agreements.

#### **Mitigation:**

**1. Term-Based Pools (Primary Defense)**
```
90-Day Pool:
  - Investors LOCKED for 90 days
  - Protocol knows exactly when withdrawals can occur
  - Can plan Murabaha terms to mature before pool maturity

Example:
- Pool matures on Day 90
- Only issue Murabaha with max 60-day terms
- Ensures liquidity available when investors want to withdraw
```

**2. Staggered Maturities**
```
Protocol ensures Murabaha agreements mature continuously:

Day 30: 10 agreements mature ($1M returned to pools)
Day 60: 15 agreements mature ($1.5M returned)
Day 90: 20 agreements mature ($2M returned)

Continuous liquidity inflow prevents bottlenecks
```

**3. Flexible Pool Reserve**
```
Maintain 20% of total TVL in unlocked Flexible Pool:
- Investors can withdraw anytime
- Lower APY (2-4%) compensates for availability
- Provides emergency liquidity buffer

Example:
- Total TVL: $50M
- Flexible Pool: $10M (always available)
- Locked Pools: $40M (deployed for higher returns)
```

**4. Utilization Rate Caps**
```
Never deploy more than 80% of any pool:

90-Day Pool:
- Total deposits: $25M
- Max deployment: $20M (80%)
- Reserve: $5M (20% for unexpected needs)
```

**5. Withdrawal Queue System**
```
If mass withdrawal event occurs:
- Withdrawals processed FIFO (first in, first out)
- Using maturing Murabaha proceeds
- Transparent queue position shown to users

Example:
- 1000 investors want to withdraw $50M
- Available liquidity: $10M
- First 200 in queue get immediate withdrawal
- Remaining 800 wait for Murabaha maturities (max 30-60 days)
```

---

### 12.5 Smart Contract Risk Management

**Risk:** Bugs, exploits, or vulnerabilities in smart contracts could lead to loss of funds.

#### **Mitigation:**

**1. Multi-Stage Audit Process**
```
Stage 1: Internal review (2 weeks)
Stage 2: External audit #1 - Certik (4 weeks)
Stage 3: External audit #2 - Trail of Bits (4 weeks)
Stage 4: External audit #3 - OpenZeppelin (4 weeks)
Stage 5: Bug bounty program (ongoing)
```

**2. Gradual TVL Rollout**
```
Phase 1 (Months 1-3): $1M TVL cap
  - Limited exposure
  - Real-world testing
  - Identify edge cases

Phase 2 (Months 4-6): $10M TVL cap
  - Proven stability
  - Expand carefully

Phase 3 (Months 7-12): $50M TVL cap
  - Mature protocol

Phase 4 (12+ months): Unlimited
  - Only after 12 months + zero critical incidents
```

**3. Insurance Fund**
```
Source: 5% of protocol profits → insurance fund
Target: 10% of total TVL
Use: Cover losses from exploits or bugs

Example:
- TVL: $50M
- Target insurance: $5M
- If exploit causes $2M loss:
  - Insurance covers it
  - Investors made whole
```

**4. Circuit Breakers**
```
Automatic pause if:
- >10% of TVL withdrawn in 1 hour (bank run)
- >50% of collateral liquidated in 1 day (market crash)
- Shariah Oracle flags protocol violation
- Admin emergency pause

Resume: Requires 3/5 multisig approval
```

**5. Upgrade Mechanism**
```
Proxy pattern for upgradeability:
- Fix bugs without redeploying
- Improve features over time

Safety:
- 48-hour timelock (users can exit if they disagree)
- 3/5 multisig required (board members)
- Community veto option (governance token holders)
```

---

### 12.6 Shariah Compliance Risk Management

**Risk:** Protocol inadvertently violates Islamic principles, making all returns haram.

#### **Mitigation:**

**1. Quarterly Shariah Audits**
```
Every 90 days:
- External Shariah board reviews all activities
- Checks: asset types, profit structures, new features
- Issues compliance report (published on-chain)
```

**2. Shariah Oracle (Real-Time)**
```
On-chain registry of halal/haram assets:
- Prevents accepting non-certified collateral
- Blocks acquisition of haram assets
- Automatic enforcement
```

**3. Purification Process**
```
If any revenue determined haram:

Step 1: Identify amount (forensic accounting)
Step 2: Immediately donate to registered Islamic charity
Step 3: Publish purification report on-chain (transparency)
Step 4: Adjust protocol to prevent recurrence
Step 5: Update Shariah guidance documents

Example:
- Unknowingly earned $5K from haram source
- Donated to Islamic Relief
- TX proof: 0x123abc...
- Investors' returns remain halal
```

**4. Conservative Bias**
```
When in doubt, DON'T do it:
- If 2/3 scholars disagree → Don't implement feature
- If similar traditional structure is debated → Avoid
- If feels like "legal trick" (Hilah) → Reject

Philosophy: Losing a feature is better than risking haram
```

**5. Community Flagging**
```
Users can submit concerns:
- "Is accepting Asset X really halal?"
- "Does this new feature violate Riba?"

Process:
- Submission via governance forum
- Shariah board reviews within 30 days
- Issues FATWA + protocol adjusts if needed
```

---

## 13. Economic Model & Projections

### 13.1 Revenue Model

The protocol earns revenue from three sources:

#### **Source 1: Murabaha Markup (95% of revenue)**

```
Example:
- Protocol sells 10 ETH via Murabaha
- Cost: $20,000
- Markup (6%): $1,200
- Revenue: $1,200

Annual Scale:
- 1,000 Murabaha agreements per year
- Average markup: $1,500
- Annual revenue: $1.5M
```

#### **Source 2: Liquidation Penalties (3-5% of revenue)**

```
Example:
- Borrower liquidated with $20K debt
- Penalty (5%): $1,000
- Protocol share (50%): $500
- Revenue: $500

Annual Scale:
- 5% of agreements liquidated (50 liquidations)
- Average penalty to protocol: $500
- Annual revenue: $25K
```

#### **Source 3: Early Repayment (No Penalty - $0 Revenue)**

```
Shariah requirement: No penalties for early repayment
Borrowers still pay full markup even if early
But this is already counted in Murabaha markup revenue
```

### 13.2 Revenue Distribution

**Protocol's Share (Mudarib): 20-30%**

Example with 25%:
```
Monthly revenue: $500,000
Protocol share: $125,000 (25%)
Investor share: $375,000 (75%)
```

**Protocol Expenses:**
```
Monthly Costs:
- Shariah Board: $10,000
- Development Team: $40,000
- Operations & Gas: $15,000
- Marketing: $20,000
- Insurance Fund (5% of revenue): $6,250
- Audits & Security: $10,000
──────────────────────────
Total Monthly Costs: $101,250

Monthly Profit: $125,000 - $101,250 = $23,750
Annual Profit (Protocol): $285,000
```

**Investor Returns:**
```
Investor share: $375,000/month
Annual investor returns: $4.5M
On $50M TVL: 9% APY average
```

### 13.3 Year 1 Projections

**Assumptions:**
- Start: $5M TVL (bootstrap)
- End of Year 1: $50M TVL
- Average markup: 6%
- Capital utilization: 70% (30% reserved for liquidity)
- Average term: 90 days (4 cycles per year)
- Mudarib share: 25%

**Calculations:**

```
Deployed Capital (average): $50M × 70% = $35M

Revenue per cycle:
- Murabaha markup: $35M × 6% = $2.1M
- Liquidation penalties: $50K
- Total per cycle: $2.15M

Annual Revenue (4 cycles): $8.6M

Distribution:
- Protocol (25%): $2.15M
- Investors (75%): $6.45M

Average Investor APY: $6.45M / $50M = 12.9%
```

**Month-by-Month Growth:**

| Month | TVL | Deployed | Revenue | Protocol Share | Investor Share |
|-------|-----|----------|---------|----------------|----------------|
| 1 | $5M | $3.5M | $210K | $52.5K | $157.5K |
| 3 | $10M | $7M | $420K | $105K | $315K |
| 6 | $25M | $17.5M | $1.05M | $262.5K | $787.5K |
| 9 | $40M | $28M | $1.68M | $420K | $1.26M |
| 12 | $50M | $35M | $2.1M | $525K | $1.575M |

**Year 1 Summary:**
```
Total Revenue: $8.6M
Protocol Profit (after costs): $2.15M - $1.2M costs = $950K
Investor Returns: $6.45M (12.9% APY average)
```

### 13.4 Year 2-3 Growth Projections

**Year 2 Target:**
- TVL: $200M
- Deployed: $140M (70%)
- Revenue per cycle: $8.4M
- Annual Revenue: $33.6M
- Protocol profit: $8.4M - $2.5M costs = $5.9M
- Investor returns: $25.2M (12.6% APY)

**Year 3 Target:**
- TVL: $500M
- Deployed: $350M
- Revenue per cycle: $21M
- Annual Revenue: $84M
- Protocol profit: $21M - $5M costs = $16M
- Investor returns: $63M (12.6% APY)

### 13.5 Comparison to Aave/Compound

**Aave (as of 2024):**
- TVL: $10B+
- Revenue: ~$50M annual (0.5% of TVL)
- Model: Facilitator, takes small cut

**Our Protocol (Year 3 projection):**
- TVL: $500M
- Revenue: $84M annual (16.8% of TVL)
- Model: Active Mudarib, takes 25% share

**Key Difference:**
- We earn MORE per dollar of TVL (16.8% vs 0.5%)
- But we also WORK MORE (acquire assets, bear risk, active management)
- Mudarib role justifies higher share vs passive facilitator

---

## 14. Protocol Parameters

### 14.1 Collateral Parameters

| Asset | Min LTV | Liquidation Threshold | Penalty | Risk Tier |
|-------|---------|----------------------|---------|-----------|
| BTC | 150% | 130% | 5% | Low |
| ETH | 150% | 130% | 5% | Low |
| DOT | 160% | 140% | 7% | Medium |
| SOL | 160% | 140% | 7% | Medium |
| MATIC | 170% | 150% | 7% | Medium |

### 14.2 Markup Schedule (Basis Points)

| Term | BTC/ETH | DOT/SOL | Smaller Assets |
|------|---------|---------|----------------|
| 30 days | 200 bps (2%) | 300 bps (3%) | 400 bps (4%) |
| 90 days | 600 bps (6%) | 700 bps (7%) | 1000 bps (10%) |
| 180 days | 1200 bps (12%) | 1400 bps (14%) | 1800 bps (18%) |

### 14.3 Pool Configurations

| Pool | Lock Period | Target APY | Mudarib Share | Min Deposit |
|------|-------------|------------|---------------|-------------|
| 30-Day | 30 days | 4-6% | 25% | 1,000 USDC |
| 90-Day | 90 days | 6-9% | 25% | 5,000 USDC |
| 180-Day | 180 days | 10-14% | 25% | 10,000 USDC |
| Flexible | None | 2-4% | 30% | 100 USDC |

### 14.4 Risk Management Parameters

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Max Utilization Rate | 80% | Maintain liquidity buffer |
| Max Asset Exposure | 20% of TVL | Diversification |
| Inventory Turnover Target | 30 days | Minimize holding risk |
| Insurance Fund Target | 10% of TVL | Cover exploit losses |
| Circuit Breaker (Withdrawal) | 10% TVL/hour | Prevent bank runs |
| Circuit Breaker (Liquidation) | 50% TVL/day | Prevent cascade |

### 14.5 Fee Structure

| Fee Type | Amount | Distribution |
|----------|--------|--------------|
| Mudarib Profit Share | 20-30% | Protocol treasury |
| Liquidation Penalty | 5-7% of debt | 50% Protocol, 50% Investors |
| Keeper Reward | 2% of penalty | Liquidation bot/caller |
| Early Repayment Fee | 0% | Shariah prohibition |
| Protocol Upgrade Fee | 0% | Community-funded |

---

## 15. User Interfaces

### 15.1 Investor Dashboard

```
┌────────────────────────────────────────────────────────────┐
│              THARWA SHARIAH LENDING - INVEST               │
└────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════╗
║              MUDARABAH INVESTMENT POOLS                  ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     ║
║  │  30-DAY     │  │  90-DAY     │  │  180-DAY    │     ║
║  │             │  │             │  │             │     ║
║  │  APY: 5.2%  │  │  APY: 8.1%  │  │  APY: 12.3% │     ║
║  │  TVL: $10M  │  │  TVL: $25M  │  │  TVL: $15M  │     ║
║  │  Lock: 30d  │  │  Lock: 90d  │  │  Lock: 180d │     ║
║  │             │  │             │  │             │     ║
║  │  [Deposit]  │  │  [Deposit]  │  │  [Deposit]  │     ║
║  └─────────────┘  └─────────────┘  └─────────────┘     ║
║                                                          ║
║  ┌─────────────┐                                        ║
║  │  FLEXIBLE   │   ← No lock-up, withdraw anytime       ║
║  │             │                                        ║
║  │  APY: 3.5%  │                                        ║
║  │  TVL: $5M   │                                        ║
║  │  Lock: None │                                        ║
║  │             │                                        ║
║  │  [Deposit]  │                                        ║
║  └─────────────┘                                        ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              YOUR ACTIVE INVESTMENTS                     ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  90-Day Mudarabah Pool                                   ║
║  ────────────────────────────────────────────────────    ║
║  • Invested:        100,000 USDC                        ║
║  • Pool Share:      0.4%                                ║
║  • Invested On:     Nov 15, 2025                        ║
║  • Maturity Date:   Feb 13, 2026 (45 days remaining)    ║
║  • Earned So Far:   3,250 USDC                          ║
║  • Projected Total: 8,100 USDC (8.1% return)            ║
║  • Status:          🟢 Active, Locked                    ║
║                                                          ║
║  [View Details]  [Withdraw (Available in 45 days)]      ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              PROFIT DISTRIBUTION HISTORY                 ║
╠══════════════════════════════════════════════════════════╣
║  Nov 2025:  +875 USDC                                    ║
║  Dec 2025:  +920 USDC                                    ║
║  Jan 2026:  +1,050 USDC                                  ║
║  ────────────────────────                                ║
║  Total:     +2,845 USDC                                  ║
╚══════════════════════════════════════════════════════════╝
```

### 15.2 Borrower Dashboard

```
┌────────────────────────────────────────────────────────────┐
│            THARWA SHARIAH LENDING - BORROW                 │
└────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════╗
║           MURABAHA ASSET ACQUISITION                     ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  Step 1: Select Asset                                    ║
║  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐                    ║
║  │ BTC  │ │ ETH  │ │ DOT  │ │ SOL  │                    ║
║  └──────┘ └──────┘ └──────┘ └──────┘                    ║
║            [Selected: ETH]                               ║
║                                                          ║
║  Step 2: Configure                                       ║
║  Amount:  [10] ETH                                       ║
║  Term:    [90 days ▼]                                    ║
║                                                          ║
║  ────────────────────────────────────────                ║
║                                                          ║
║  PRICING BREAKDOWN                                       ║
║  Cost Price (Protocol's cost):    $20,000               ║
║  Markup (6% for 90-day term):     $1,200                ║
║  ═══════════════════════════════════════                ║
║  Total Sale Price:                $21,200               ║
║                                                          ║
║  Payment Terms:                                          ║
║  • 3 monthly installments                                ║
║  • $7,067 USDC per month                                 ║
║  • First payment due 30 days after execution             ║
║                                                          ║
║  ────────────────────────────────────────                ║
║                                                          ║
║  Step 3: Provide Collateral                              ║
║  Required: $31,800 (150% of sale price)                  ║
║                                                          ║
║  Your Collateral:                                        ║
║  Asset:   [BTC ▼]                                        ║
║  Amount:  [1] BTC                                        ║
║  Value:   $32,000 ✅ Sufficient                          ║
║  Ratio:   151% ✅                                         ║
║                                                          ║
║  ────────────────────────────────────────                ║
║                                                          ║
║  [Review Murabaha Agreement]  [Execute Transaction]      ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              YOUR ACTIVE AGREEMENTS                      ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  Agreement #1234                                         ║
║  ────────────────────────────────────────                ║
║  Asset Received:    10 ETH                               ║
║  Total Owed:        $21,200 USDC                         ║
║  Remaining:         $14,133 USDC                         ║
║                                                          ║
║  Payment Schedule:                                       ║
║  ✅ Payment 1:  $7,067 (Paid on Dec 15, 2025)            ║
║  ⏳ Payment 2:  $7,067 (Due in 15 days)                  ║
║  ⏳ Payment 3:  $7,066 (Due in 45 days)                  ║
║                                                          ║
║  Collateral Status:                                      ║
║  Asset:         1 BTC                                    ║
║  Current Value: $32,000                                  ║
║  Ratio:         151% 🟢 Healthy                          ║
║                                                          ║
║  [Make Payment Now]  [Add Collateral]  [Repay Early]    ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝
```

### 15.3 Protocol Analytics Dashboard (Admin)

```
┌────────────────────────────────────────────────────────────┐
│             PROTOCOL ANALYTICS - ADMIN VIEW                │
└────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════╗
║              PROTOCOL HEALTH OVERVIEW                    ║
╠══════════════════════════════════════════════════════════╣
║  Total TVL:              $50,000,000                     ║
║  Deployed Capital:       $35,000,000 (70%)               ║
║  Available Liquidity:    $15,000,000 (30%)               ║
║  Active Agreements:      1,250                           ║
║  Total Borrowers:        890                             ║
║  Total Investors:        5,430                           ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              ASSET INVENTORY STATUS                      ║
╠══════════════════════════════════════════════════════════╣
║  BTC:   45/50 🟢   ($2.7M / $3M target)                  ║
║  ETH:   380/500 🟡 ($760K / $1M target)                  ║
║  DOT:   95K/100K 🟢                                      ║
║  SOL:   18K/25K 🟡                                       ║
║  Total Inventory Value: $4.5M                            ║
║  Unrealized P&L: +$180K (4.2% gain)                      ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              REVENUE & PROFITABILITY                     ║
╠══════════════════════════════════════════════════════════╣
║  This Month:                                             ║
║    Murabaha Markup:         $520,000                     ║
║    Liquidation Penalties:   $18,000                      ║
║    Total Revenue:           $538,000                     ║
║                                                          ║
║  Distribution:                                           ║
║    Protocol (25%):          $134,500                     ║
║    Investors (75%):         $403,500                     ║
║                                                          ║
║  Year-to-Date:                                           ║
║    Total Revenue:           $6,450,000                   ║
║    Protocol Profit:         $1,612,500                   ║
║    Avg Investor APY:        12.8%                        ║
╚══════════════════════════════════════════════════════════╝

╔══════════════════════════════════════════════════════════╗
║              RISK METRICS                                ║
╠══════════════════════════════════════════════════════════╣
║  Agreements at Risk (130-140%):     42 (3.4%)            ║
║  Agreements Healthy (>150%):        1,180 (94.4%)        ║
║  Liquidations (This Month):         8 (0.6%)             ║
║  Bad Debt:                          $0 (0%)              ║
║  Insurance Fund:                    $4.2M (8.4% of TVL)  ║
╚══════════════════════════════════════════════════════════╝
```

---

## 16. Implementation Roadmap

### 16.1 Phase 0: Foundation (Months 1-2)

**Objectives:**
- Shariah board formation
- Legal entity setup
- Initial asset certification

**Deliverables:**
```
✅ Shariah Advisory Board (3-5 scholars)
✅ Legal entity (Foundation in UAE/Singapore)
✅ Initial FATWA on protocol structure
✅ BTC & ETH certified as halal
✅ Whitepaper published
✅ Community building (Discord, Twitter)
```

**Team:**
- 1 CEO/Founder
- 1 CTO
- 2 Smart Contract Developers
- 1 Frontend Developer
- 3-5 Shariah Scholars (advisory)

**Budget:** $150K

---

### 16.2 Phase 1: Smart Contract Development (Months 3-5)

**Objectives:**
- Build core smart contracts
- Internal testing
- Testnet deployment

**Deliverables:**
```
✅ MudarabahPool contracts (4 variants)
✅ AssetInventoryManager
✅ MurabahaEngine
✅ CollateralManager
✅ LiquidationEngine
✅ PriceOracle integration (Chainlink)
✅ ShariahOracle
✅ ProfitDistributor
✅ Deployed to Sepolia Testnet
✅ Internal testing & bug fixes
```

**Team:**
- 3 Smart Contract Developers
- 1 Security Engineer
- 1 QA Engineer

**Budget:** $300K

---

### 16.3 Phase 2: Security Audits (Months 6-8)

**Objectives:**
- Professional security audits
- Bug bounty program
- Fix all critical/high findings

**Deliverables:**
```
✅ Audit #1: Certik (4 weeks, $80K)
✅ Audit #2: Trail of Bits (4 weeks, $100K)
✅ Audit #3: OpenZeppelin (4 weeks, $120K)
✅ Bug Bounty: $50K pool (Immunefi)
✅ All findings addressed
✅ Final audit reports published
```

**Team:**
- 3 Smart Contract Developers (fixing issues)
- 1 Security Engineer
- External audit firms

**Budget:** $350K

---

### 16.4 Phase 3: Frontend & UX (Months 7-9, parallel with audits)

**Objectives:**
- Build user-facing dApp
- Mobile-responsive design
- Wallet integration

**Deliverables:**
```
✅ Investor Dashboard (deposit, track, withdraw)
✅ Borrower Dashboard (request, repay, monitor)
✅ Admin Analytics Dashboard
✅ WalletConnect integration
✅ Metamask, Coinbase Wallet, Rainbow support
✅ Mobile-responsive design
✅ Arabic language support (optional but recommended)
```

**Team:**
- 2 Frontend Developers
- 1 UI/UX Designer
- 1 Backend Developer (API, database)

**Budget:** $200K

---

### 16.5 Phase 4: Mainnet Launch (Month 10)

**Objectives:**
- Deploy to Ethereum mainnet
- Bootstrap initial liquidity
- Launch with limited TVL cap

**Deliverables:**
```
✅ Mainnet deployment (all contracts)
✅ Verification on Etherscan
✅ Bootstrap liquidity: $5M from foundation/investors
✅ TVL Cap: $10M for first 3 months
✅ Launch announcement
✅ Marketing campaign
✅ Media coverage (CoinDesk, CoinTelegraph)
```

**Initial Assets:**
- BTC (certified halal)
- ETH (certified halal)
- Initial collateral: BTC, ETH only

**Team:**
- Full team (15 people)
- Marketing team (2 people)
- Community managers (2 people)

**Budget:** $500K (includes $5M bootstrap capital separate)

---

### 16.6 Phase 5: Growth & Expansion (Months 11-18)

**Objectives:**
- Increase TVL to $50M
- Add new assets
- Expand to L2s

**Deliverables:**
```
✅ TVL growth: $10M → $50M
✅ New assets: DOT, SOL, MATIC (after certification)
✅ L2 deployment: Arbitrum, Polygon
✅ 5,000+ investors
✅ 1,000+ active Murabaha agreements
✅ Partnerships: DeFi protocols, Islamic fintech
✅ Educational content (halal investing guides)
```

**Budget:** $800K (marketing, operations, team expansion)

---

### 16.7 Phase 6: Advanced Features (Months 18-24)

**Objectives:**
- Qard Hassan pools
- RWA integration
- Institutional products

**New Products:**
```
✅ Qard Hassan Pool (zero-interest emergency loans)
✅ RWA Murabaha (buy Tharwa's thBonds via Murabaha)
✅ Institutional Desk (large borrowers >$1M)
✅ Automated strategies (Confluence Engine integration)
✅ Mobile app (iOS, Android)
```

**Budget:** $1M

---

### 16.8 Total 24-Month Budget

| Phase | Duration | Cost | Cumulative |
|-------|----------|------|------------|
| 0: Foundation | 2 months | $150K | $150K |
| 1: Development | 3 months | $300K | $450K |
| 2: Audits | 3 months | $350K | $800K |
| 3: Frontend | 3 months | $200K | $1M |
| 4: Launch | 1 month | $500K | $1.5M |
| 5: Growth | 8 months | $800K | $2.3M |
| 6: Advanced | 6 months | $1M | $3.3M |

**Total 24-Month Budget: $3.3M**

**Funding Sources:**
- Seed round: $2M (investors)
- Bootstrap capital: $5M (foundation/strategic partners for initial liquidity)
- Revenue after Month 12: Self-sustaining

---

## 17. Shariah Compliance Documentation

### 17.1 Core Shariah Principles Adherence

#### **Prohibition of Riba (Interest)**

**Compliance:**
- ✅ Investors deposit USDC, earn USDC from trading profits (not interest on loans)
- ✅ Borrowers receive ETH, repay USDC (different assets, no same-asset Riba)
- ✅ Markup is from asset trading (Murabaha), not time-value of money
- ✅ No compounding, no variable rates tied to time

**Traditional Violation Example:**
- ❌ Lend 10 ETH → Receive 12 ETH (Riba on same asset)

**Our Model:**
- ✅ Buy 10 ETH with USDC → Sell 10 ETH for more USDC (trading profit)

---

#### **Prohibition of Gharar (Excessive Uncertainty)**

**Compliance:**
- ✅ All terms known upfront (cost price, markup, sale price, installments)
- ✅ Assets exist before sale (Protocol owns inventory)
- ✅ No hidden fees or terms
- ✅ Transparent profit calculation

**Example Murabaha Agreement:**
```
Cost Price:    $20,000 (disclosed)
Markup:        $1,200 (6%, disclosed)
Sale Price:    $21,200 (fixed, known)
Term:          90 days (fixed)
Installments:  3 × $7,067/month (fixed)

Total Certainty: 100%
```

---

#### **Prohibition of Maysir (Gambling/Speculation)**

**Compliance:**
- ✅ Assets have real utility (BTC, ETH are used for transactions, smart contracts)
- ✅ No pure gambling tokens (casino tokens rejected)
- ✅ No meme coins (pure speculation = Maysir)
- ✅ Shariah Oracle filters out speculative assets

**Rejected Assets:**
- ❌ Shiba Inu (SHIB) - No utility, pure speculation
- ❌ Dogecoin (DOGE) - Meme coin, no serious utility
- ❌ Casino/gambling protocol tokens

---

#### **Asset-Backed Requirement**

**Compliance:**
- ✅ Protocol OWNS assets before selling (real asset transaction)
- ✅ Not selling what we don't own (prohibition in Hadith)
- ✅ Ownership risk: Protocol bears price volatility

**Process:**
```
1. Mudarabah investors provide USDC
2. Protocol BUYS 10 ETH from market
3. Protocol OWNS 10 ETH (in inventory)
4. Protocol SELLS 10 ETH to borrower

At step 3, Protocol bears risk of ETH price drop.
This ownership makes it halal trade, not prohibited forward sale.
```

---

### 17.2 Mudarabah Structure Compliance

**Classical Definition:**
> "A partnership where one party provides capital (Rab-ul-Maal) and the other provides expertise/management (Mudarib). Profits are shared according to pre-agreed ratio. Losses are borne by capital provider unless Mudarib was negligent."

**Our Implementation:**

| Requirement | Our Protocol |
|-------------|--------------|
| Capital Provider | Investors (deposit USDC) |
| Manager | Protocol (Mudarib) |
| Profit Sharing | 70-80% investors, 20-30% Protocol |
| Loss Bearing | Investors bear capital losses (e.g., inventory depreciation) |
| Negligence Clause | Protocol liable if proven negligent (e.g., buying haram assets, not managing collateral) |
| Fixed Return Prohibition | No guaranteed returns - profits vary based on performance ✅ |

**Key Compliance Point:**
- Traditional Mudarabah: Silent partner invests in trader's caravan
- Our Mudarabah: Investors invest in Protocol's crypto asset trading business

---

### 17.3 Murabaha Structure Compliance

**Classical Definition:**
> "A sale contract where seller purchases an asset, takes ownership, then sells to buyer at cost + known markup with deferred payment."

**Our Implementation:**

| Requirement | Our Protocol |
|-------------|--------------|
| Seller owns asset first | Protocol buys from market, holds in inventory ✅ |
| Cost price disclosed | Shown to borrower: "Cost: $20,000" ✅ |
| Markup disclosed | Shown to borrower: "Markup: $1,200 (6%)" ✅ |
| Sale price fixed | $21,200 fixed at time of agreement ✅ |
| Deferred payment allowed | Installments over 90 days ✅ |
| Ownership transfer | ETH transferred to borrower immediately ✅ |
| No same-asset Riba | Receive ETH, repay USDC (different) ✅ |

**Key Compliance Point:**
- Traditional Murabaha: Bank buys house, sells to customer at markup
- Our Murabaha: Protocol buys ETH, sells to borrower at markup

---

### 17.4 FATWA Template

**Sample FATWA for Protocol:**

```
بسم الله الرحمن الرحيم

FATWA: Shariah Compliance of Tharwa Lending Protocol

Question:
Is the Tharwa Shariah-Compliant Crypto Lending Protocol permissible under Islamic law?

Answer:
After thorough review of the protocol's structure, smart contracts, and operational procedures, we conclude:

✅ PERMISSIBLE (Halal) based on the following:

1. MUDARABAH COMPLIANCE:
   - Investors enter genuine profit-sharing partnership
   - No guaranteed returns (complies with risk-sharing requirement)
   - Losses borne by capital providers (classical Mudarabah)
   - Protocol acts as active manager (Mudarib), not passive facilitator

2. MURABAHA COMPLIANCE:
   - Protocol acquires asset before selling (ownership requirement met)
   - Cost and markup disclosed transparently (no Gharar)
   - Fixed sale price agreed upfront
   - Different assets in/out (USDC → ETH → USDC repayment)
   - No time-based penalties (early repayment allowed)

3. NO RIBA:
   - No same-asset increase (no lending 10 ETH for 12 ETH)
   - Profit from trading, not from time-value of money
   - All returns traceable to legitimate business activities

4. ASSET HALAL CERTIFICATION:
   - Only Shariah-certified assets accepted
   - Continuous monitoring via Shariah Oracle
   - Purification process for inadvertent haram income

CONDITIONS:
- Annual recertification of all assets
- Quarterly Shariah audit of operations
- Immediate purification of any haram revenue
- No lending to protocols engaged in Riba

والله أعلم

[Signature]
Dr. [Scholar Name]
Shariah Advisory Board Chair
Date: [Date]
```

---

### 17.5 Comparison to Traditional Islamic Banking

| Feature | Islamic Bank | Our Protocol |
|---------|--------------|--------------|
| Deposit Structure | Mudarabah investment accounts | Mudarabah pools ✅ |
| Returns Guarantee | No (profits vary) | No (profits vary) ✅ |
| Lending Structure | Murabaha, Ijarah, Musharaka | Murabaha ✅ |
| Asset Ownership | Bank owns before selling | Protocol owns before selling ✅ |
| Transparency | Moderate | High (on-chain, immutable) ✅ |
| Riba Prohibition | Yes | Yes ✅ |
| Shariah Board | Yes | Yes ✅ |

**Key Difference:**
- Islamic banks: Physical assets (cars, houses, inventory)
- Our protocol: Digital assets (BTC, ETH, crypto)

**Same Principles, Different Assets** ✅

---

### 17.6 Ongoing Compliance Measures

**1. Quarterly Shariah Audits**
```
Every 90 days:
- Review all new features
- Check asset portfolio
- Verify profit calculations
- Assess investor complaints
- Issue compliance report
```

**2. Annual Asset Recertification**
```
Every 12 months:
- Re-evaluate all accepted assets
- Check for changes in usage/ecosystem
- Renew or revoke certification
- Update Shariah Oracle
```

**3. Purification Process**
```
If haram revenue detected:
- Calculate exact amount
- Donate to registered Islamic charity
- Publish TX proof on-chain
- Adjust protocol to prevent recurrence
```

**4. Community Reporting**
```
Users can flag concerns:
- Submit via governance forum
- Shariah board reviews within 30 days
- Issue FATWA/guidance
- Implement changes if needed
```

---

## Conclusion

This Shariah-compliant crypto lending protocol represents a breakthrough in Islamic DeFi:

**Key Innovations:**
1. ✅ **Authentic Mudarabah:** True profit-sharing, not rebranded interest
2. ✅ **Real Murabaha:** Protocol OWNS assets before selling (not legal fiction)
3. ✅ **No Riba:** Different asset in/out, trading profit (not interest)
4. ✅ **Scalable:** Pooled liquidity like Aave, but Shariah-compliant
5. ✅ **Transparent:** On-chain, auditable, Shariah Oracle enforcement

**Market Opportunity:**
- $3+ trillion Islamic finance industry globally
- <1% has access to crypto
- MRHB, HAQQ have NO lending products
- We're first-to-market with authentic structure

**Next Steps:**
1. Form Shariah Advisory Board
2. Secure $2M seed funding + $5M bootstrap capital
3. Begin smart contract development
4. Launch within 12 months
5. Target $50M TVL by end of Year 1

**This is the future of halal DeFi. Let's build it.**

---

**Document Version:** 1.0
**Last Updated:** January 2026
**Status:** Architecture Complete - Ready for Implementation

For questions or collaboration: [Contact Information]

الحمد لله رب العالمين
