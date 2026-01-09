# Shariah-Compliant Crypto Lending Protocol
## A Halal Alternative to Aave & Compound

**Version:** 0.1 | **Date:** January 2026 | **Status:** Architecture Specification

---

## Executive Summary

This document presents a Shariah-compliant decentralized lending protocol enabling access to crypto liquidity (BTC, ETH, SOL, DOT) without Riba (interest). The protocol uses authentic Islamic finance structures—**Mudarabah** (profit-sharing partnership) and **Murabaha** (cost-plus sale)—to replicate Aave/Compound functionality while maintaining full Shariah compliance.

### The Problem

The $3 trillion Islamic finance market cannot access crypto lending because all existing protocols (Aave, Compound, MakerDAO) operate on interest-based models:

**Current Protocols (Riba-Based):**
- Deposit ETH → Earn interest on lending
- Borrow ETH → Pay interest on borrowing
- Same asset in/out with predetermined increase = Pure Riba (forbidden)

**Market Gap:**
- MRHB Network: No lending products
- HAQQ Network: No lending products
- Islamic DeFi: Massive untapped opportunity

### Our Solution

We replace interest-based lending with Islamic trading structures:

**Innovation:** Instead of lending, we facilitate **asset trading** using authentic Islamic contracts:

| Aspect | Aave/Compound | Our Protocol |
|--------|---------------|--------------|
| Deposit | Lend crypto → Earn interest | Invest USDC → Profit-sharing partnership |
| Borrow | Borrow same asset + interest | Buy asset via sale contract (Murabaha) |
| Returns | Interest (Riba) | Trading profits (Halal) |
| Asset Flow | ETH → ETH (same asset) | USDC → ETH → USDC (different assets) |
| Compliance | Haram ❌ | Halal ✅ |

**Key Principle:** You cannot profit from lending 10 ETH and receiving 12 ETH back (Riba). But you CAN profit from buying 10 ETH with $20K USDC and selling it for $21.2K USDC (trading).

---

## Table of Contents

1. [Shariah Compliance Foundation](#1-shariah-compliance-foundation)
2. [The Core Model](#2-the-core-model)
3. [Protocol Architecture](#3-protocol-architecture)
4. [How It Works: Complete Flow](#4-how-it-works-complete-flow)
5. [Economic Model](#5-economic-model)
6. [Risk Management](#6-risk-management)
7. [Implementation Roadmap](#7-implementation-roadmap)
8. [Shariah Certification](#8-shariah-certification)

---

## 1. Shariah Compliance Foundation

### 1.1 Core Prohibitions

**Riba (Interest/Usury):**
- Forbidden: Any predetermined profit on debt
- Example: Lend 10 ETH → Receive 12 ETH ❌
- Permissible: Buy 10 ETH for $20K → Sell for $22K ✅

**Gharar (Excessive Uncertainty):**
- Forbidden: Unknown terms, speculative contracts
- Permissible: All terms disclosed upfront, clear pricing

**Maysir (Gambling):**
- Forbidden: Pure speculation, meme coins, casino tokens
- Permissible: Assets with real utility (BTC, ETH for transactions/smart contracts)

### 1.2 Islamic Finance Structures We Use

#### Mudarabah (Investment Partnership)

**Definition:** Partnership where one party provides capital (Rab-ul-Maal), the other provides management (Mudarib).

**Structure:**
- Capital Provider: Investors who deposit stablecoins
- Manager: Protocol (acts as Mudarib)
- Profit Sharing: Pre-agreed ratio (e.g., 70% investors, 30% protocol)
- Loss Bearing: Capital providers bear financial losses; manager loses time/effort

**Example:**
- Investor deposits $100K → Protocol trades assets → Earns $10K profit
- Split: Investor gets $7K (70%), Protocol gets $3K (30%)

**Why It's Halal:** No guaranteed returns (shares in actual profits/losses), manager actively works for earnings.

#### Murabaha (Cost-Plus Sale)

**Definition:** Sale contract where seller buys an asset, discloses cost, sells at cost + known markup.

**Structure:**
- Seller (Protocol) purchases asset first (takes ownership)
- Discloses cost price to buyer
- Sells at cost + markup with deferred payment allowed
- Buyer repays in installments

**Example:**
- Protocol buys 10 ETH for $20,000 (cost price)
- Sells to borrower for $21,200 (cost + $1,200 markup = 6%)
- Borrower repays $21,200 in USDC over 90 days
- Provides collateral (1 BTC) to secure repayment

**Why It's Halal:** Protocol owns asset before selling (real trade), markup is known upfront (not time-based interest), repayment in different asset (USDC not ETH).

### 1.3 Why Traditional Lending Violates Shariah

**Aave/Compound Model:**
```
Deposit 10 ETH → Earn 3% APY → Withdraw 10.3 ETH
                    ↑
              Same asset with increase = Riba
```

**The Problem:**
- Same asset in, same asset out, with predetermined increase
- Time-value of money (interest accrues over time)
- No real business activity or trading

**Our Model:**
```
Deposit USDC → Protocol buys ETH → Sells ETH for more USDC → Profit from trading
         ↓                ↓                    ↓
    Capital         Ownership Risk        Trading Profit (Halal)
```

**Why This Works:**
- Different assets (USDC in → USDC out, but ETH traded in between)
- Real trading activity (buy/sell assets)
- Protocol bears ownership risk (price volatility while holding inventory)

---

## 2. The Core Model

### 2.1 The Breakthrough Insight

Islamic banks solved this decades ago for physical assets (cars, houses). We're adapting the same principles for crypto:

**Islamic Bank Model:**
```
Depositor → Mudarabah Investment Account → Bank uses funds to buy assets
                                                ↓
Customer wants car → Bank BUYS car → Bank SELLS car at markup → Customer repays
```

**Our Crypto Adaptation:**

**The Model:**

```
┌─────────────────────────────────────────────────────────────┐
│                    SHARIAH-COMPLIANT FLOW                   │
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

**Critical Element:** The protocol must ACTUALLY BUY and OWN the crypto before selling it. This transforms it from interest-based lending to legitimate asset trading.

### 2.2 High-Level System Design

```
┌─────────────────────────────────────────────────────────────┐
│              THARWA SHARIAH LENDING PROTOCOL                │
│           (Mudarabah + Murabaha Hybrid Model)               │
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

### 2.3 How Money Flows

**Step 1: Investor Deposits (Mudarabah)**
- Alice deposits 100,000 USDC into 90-Day Mudarabah Pool
- Becomes partner (Rab-ul-Maal) with Protocol (Mudarib)
- Receives mdUSDC-90 vault share tokens
- Funds available for Protocol to deploy

**Step 2: Protocol Builds Inventory**
- Protocol uses pool funds to buy crypto from market
- Buys 50 ETH @ $2,000/ETH = $100,000 USDC spent
- Protocol now OWNS 50 ETH (takes price risk)
- Records cost basis: $2,000/ETH

**Step 3: Borrower Executes Murabaha**
- Bob wants 10 ETH for 90 days
- Protocol calculates: Cost $20K + 6% markup = $21.2K
- Bob provides 1 BTC collateral ($32K = 151% LTV)
- Protocol SELLS 10 ETH to Bob (Murabaha sale)
- Bob receives 10 ETH immediately, owes $21.2K USDC
- Repayment: 3 monthly installments of $7,067

**Step 4: Profit Distribution**
- Bob completes payments → Protocol earned $1,200 markup
- Distribution: Alice (75%) = $900, Protocol (25%) = $300
- Alice's investment: $100K → $100.9K (partial, continues monthly)

**Key Point:** The same money flows through, but there's REAL ASSET TRADING in the middle, not interest-based lending.

---

## 3. Protocol Architecture

### 3.1 Six Core Components

The protocol consists of six major components:

1. **Mudarabah Investment Pools** - Accept stablecoin deposits from investors
2. **Volatile Asset Inventory** - Protocol-owned pools of BTC, ETH, SOL, DOT, etc.
3. **Murabaha Execution Engine** - Facilitates asset sales to borrowers
4. **Collateral Management System** - Secures borrower obligations
5. **Liquidation Engine** - Protects against defaults
6. **Shariah Governance Board** - Ensures ongoing compliance

#### Component A: Mudarabah Investment Pools

**Purpose:** Accept stablecoin deposits from investors

**Pool Types:**
- **30-Day Pool:** 4-6% APY, locked 30 days
- **90-Day Pool:** 6-9% APY, locked 90 days
- **180-Day Pool:** 10-14% APY, locked 180 days
- **Flexible Pool:** 2-4% APY, withdraw anytime

**Accepted Assets:** USDC, USDT, thUSD (stablecoins only)

**Why Stablecoins Only:**
- Eliminates same-asset Riba (USDC in → USDC out from trading)
- Stable base for acquiring volatile assets
- Simplifies profit calculations

**Investor Benefits:**
- Halal returns from trading profits
- Proportional profit-sharing based on stake
- ERC-4626 vault shares (tradable, composable)

**Investor Risks:**
- Share in losses if Protocol makes poor decisions
- No guaranteed returns (true Mudarabah)
- Example: If inventory depreciates 10%, investors bear that loss

---

#### Component B: Volatile Asset Inventory

**Purpose:** Protocol-owned pools of crypto assets for Murabaha sales

**Asset Pools:**
```
├─ BTC Pool (Bitcoin)
├─ ETH Pool (Ethereum)
├─ SOL Pool (Solana)
├─ DOT Pool (Polkadot)
└─ [Future: Additional halal-certified assets]
```

**How Pools Are Filled:**
- Protocol uses Mudarabah funds to buy from market
- Maintains min/target/max inventory levels
- Example: ETH → Min: 200, Target: 500, Max: 1,000
- Rebalances automatically based on demand

**Ownership Risk:**
- Protocol OWNS these assets (critical for Shariah compliance)
- Bears price volatility while in inventory
- Example: Buy 500 ETH @ $2,000, price drops to $1,800 = $100K loss
- This loss shared with Mudarabah investors (capital providers)

**Inventory Management:**
- Target 30-day turnover (buy → sell within 30 days)
- Dynamic inventory caps (max 20% of TVL per asset)
- Just-in-time purchasing for large orders

---

#### Component C: Murabaha Execution Engine

**Purpose:** Facilitate Shariah-compliant asset sales to borrowers

**Murabaha Process:**
1. Borrower requests asset (e.g., "10 ETH, 90-day term")
2. Protocol checks inventory availability
3. Calculates cost price (Protocol's acquisition cost: $20,000)
4. Applies markup based on term + asset risk (6% = $1,200)
5. Total sale price: $21,200 (disclosed to borrower)
6. Creates installment schedule (3 months × $7,067)
7. Locks collateral (1 BTC)
8. Transfers 10 ETH to borrower (Murabaha sale executed)
9. Tracks repayment schedule

**Markup Structure:**

| Term | BTC/ETH (Low Risk) | DOT/SOL (Medium Risk) |
|------|--------------------|-----------------------|
| 30 days | 2% | 3% |
| 90 days | 6% | 7% |
| 180 days | 12% | 14% |

**Shariah Compliance Points:**
- Cost price disclosed (transparency)
- Markup fixed and known upfront (no Gharar)
- Protocol owned asset before selling (real trade)
- Repayment in different asset (USDC, not ETH)
- No penalty for early repayment (Shariah requirement)

---

#### Component D: Collateral Management

**Purpose:** Secure repayment through over-collateralization

**Accepted Collateral:** BTC, ETH, DOT, SOL (halal-certified assets)

**Collateralization Ratios:**

| Asset | Min LTV | Liquidation Threshold | Liquidation Penalty |
|-------|---------|----------------------|---------------------|
| BTC | 150% | 130% | 5% |
| ETH | 150% | 130% | 5% |
| DOT | 160% | 140% | 7% |
| SOL | 160% | 140% | 7% |

**Example:**
- Borrower owes $21,200
- Must provide: $31,800 collateral (150% × $21,200)
- If BTC collateral drops to $27,560 (130%), liquidation triggered

**Health States:**
- **Healthy:** >150% ratio (green)
- **Warning:** 130-150% ratio (yellow, add collateral recommended)
- **Liquidation:** <130% ratio (red, liquidation eligible)

**Features:**
- Add collateral anytime to improve health
- Withdraw excess if ratio very high
- Real-time monitoring via price oracles

---

#### Component E: Liquidation Engine

**Purpose:** Protect protocol and investors when borrower defaults

**Liquidation Triggers:**
1. Collateral ratio drops below threshold (130% for BTC/ETH)
2. Borrower misses 2 consecutive payments (60+ days late)

**Liquidation Process:**
1. Keeper bot detects liquidation condition
2. Calls liquidate() function
3. Collateral sold on DEX (1inch, Uniswap) for USDC
4. Proceeds distributed:
   - Repay outstanding debt → Mudarabah pools
   - Liquidation penalty (5-7%) → Split 50/50 (Protocol/Investors)
   - Keeper incentive (2% of penalty) → Bot operator
   - **Excess collateral returned to borrower** (Shariah requirement)

**Example:**
- Debt: $14,133 remaining
- Collateral: 1 BTC sells for $18,000
- Distribution:
  - Debt repayment: $14,133
  - Penalty (5%): $707 → $353 Protocol, $354 Investors
  - Keeper: $14
  - **Excess: $3,160 returned to borrower**

**Shariah Compliance:** Returning excess collateral is mandatory in Islam. Protocol only takes what's owed, not more.

---

#### Component F: Shariah Governance Board

**Purpose:** Ensure ongoing Shariah compliance

**Composition:** 3-5 qualified Islamic scholars with expertise in Islamic finance, blockchain, and contemporary jurisprudence

**Responsibilities:**

**1. Asset Certification**
- Review crypto assets for halal/haram status
- Criteria: Utility, decentralization, no haram activities
- Maintain on-chain Shariah Oracle registry
- Annual recertification required

**Examples:**
- ✅ Halal: BTC (store of value), ETH (smart contracts utility)
- ❌ Haram: AAVE token (governs interest protocol), Casino tokens
- ⚠️ Under Review: Assets with mixed use cases

**2. Quarterly Protocol Audits**
- Review all operations and revenues
- Check profit structures (still compliant?)
- Verify no Riba introduction
- Issue public compliance report

**3. FATWA Issuance**
- Answer questions on new features
- Provide religious rulings for edge cases
- Example: "Can borrowers use acquired crypto for yield farming?" → FATWA issued

**4. Purification Process**
- If any revenue determined haram post-facto
- Calculate exact amount
- Donate to Islamic charity immediately
- Publish on-chain proof (TX hash)
- Adjust protocol to prevent recurrence

**Shariah Oracle:**
- On-chain smart contract registry
- Stores certification status of all assets
- Protocol checks before accepting collateral or inventory
- Certifications expire after 365 days (must renew)

---

## 4. How It Works: Complete Flow

### 4.1 Investor Journey (Mudarabah)

**Alice's Complete Experience:**

**Step 1: Discovery & Research**
- Alice learns about halal crypto investing
- Researches protocol: reads whitepaper, checks Shariah certification
- Reviews FATWA from Shariah Advisory Board
- Understands key difference: This is investment partnership (Mudarabah), not interest-based lending

**Step 2: Pool Selection**
- Compares four pool options:
  - 30-Day: 5.2% APY, quick liquidity, lower returns
  - **90-Day: 8.1% APY** ← Alice selects this (balanced risk/return)
  - 180-Day: 12.3% APY, highest returns but longest lock
  - Flexible: 3.5% APY, withdraw anytime but lower returns
- Considers: She doesn't need funds for 3 months, so 90-day optimal

**Step 3: Understanding Mudarabah Terms**
- Reads agreement carefully:
  - "You are entering a profit-sharing partnership (Mudarabah)"
  - "Protocol (Mudarib) will actively manage your capital"
  - "Capital deployed to buy/sell halal crypto assets via Murabaha"
  - "Profits shared: You 75%, Protocol 25%"
  - "**Important:** You share in losses if Protocol makes poor decisions"
  - "No guaranteed returns - actual performance may vary"
  - "Funds locked for 90 days - no early withdrawal"

**Step 4: Wallet Connection & Deposit**
- Connects MetaMask wallet
- Reviews transaction details:
  - Amount: 100,000 USDC
  - Destination: Mudarabah90DayPool contract
  - Gas fee: ~$15 (Ethereum L1)
- Approves USDC spend (ERC-20 approval transaction)
- Confirms deposit transaction
- Transaction confirmed on-chain

**Step 5: Receipt & Confirmation**
- Receives 100,000 mdUSDC-90 vault share tokens (ERC-4626 standard)
- These tokens represent:
  - Her proportional ownership in the 90-day pool
  - Current pool size: $25M total
  - Her share: 0.4% of pool
  - Redeemable for principal + profits after 90 days
- Dashboard updated showing active investment

**Step 6: Monitoring (90-Day Period)**

**Month 1:**
- Protocol generates $50K profit from Murabaha sales
- 90-Day pool receives 50% allocation = $25K
- Alice's share (0.4%): $100
- Plus previous month's carryover profits
- Her dashboard: "Earned this month: $875"
- Cumulative: $875

**Month 2:**
- Protocol profit grows with more Murabaha agreements
- Monthly profit: $55K total
- Alice's share calculation:
  - Pool allocation: $27.5K
  - Her 0.4% share: $110
  - Dashboard: "Earned this month: $920"
- Cumulative: $1,795

**Month 3:**
- Protocol scaling, more borrowers
- Monthly profit: $60K
- Alice's share: $120 from new profits
- Dashboard: "Earned this month: $1,050"
- Cumulative: $2,845
- Additional months' carryover brings total to ~$8,100

**Step 7: Maturity & Withdrawal**
- Day 90 arrives
- Dashboard shows "Withdraw" button now active
- Alice reviews final statement:
  - Original deposit: 100,000 USDC
  - Total profit earned: 8,100 USDC
  - Return: 8.1%
  - Annualized: ~33% APY (but this was 90 days)
- Clicks "Withdraw"
- Burns 100,000 mdUSDC-90 tokens
- Receives 108,100 USDC to wallet
- Transaction confirmed

**Step 8: Reinvestment Decision**
- Alice can now:
  - Re-invest in another 90-Day pool (compound returns)
  - Try 180-Day pool for higher returns
  - Withdraw to fiat via CEX
  - Use for other DeFi opportunities

**Alice's Outcome:**
- Initial: 100,000 USDC
- Final: 108,100 USDC
- Profit: 8,100 USDC (8.1% in 90 days)
- Halal returns from trading profits (not interest)
- Can prove to family/community: Shariah-certified ✅

---

### 4.2 Borrower Journey (Murabaha)

**Bob's Complete Experience:**

**Background:**
- Bob holds 1 BTC (worth $32,000)
- Bullish on ETH, wants to hold ETH without selling his BTC
- Traditional option: Sell BTC for USDC, buy ETH (loses BTC exposure)
- Our option: Use BTC as collateral, acquire ETH via Murabaha

**Step 1: Discovery & Assessment**
- Bob discovers the protocol
- Understands: This is NOT a loan, it's a **purchase agreement** (Murabaha)
- Key insight: He's buying 10 ETH from the Protocol at an agreed price
- The "markup" is the Protocol's profit margin (like any seller)
- Repayment is the deferred payment for the purchase

**Step 2: Asset Selection**
- Navigates to "Borrow" dashboard
- Sees available assets:
  - BTC: Available (500 BTC in inventory)
  - ETH: Available (1,200 ETH in inventory) ← Bob selects
  - DOT: Available (50K DOT in inventory)
  - SOL: Limited availability (15K SOL, low)

**Step 3: Configuration**
- Asset: 10 ETH
- Term: 90 days
- System calculates in real-time:

  ```
  PRICING BREAKDOWN:
  ─────────────────
  Protocol's Cost Price:    $20,000
    (What Protocol paid to acquire this ETH from market)

  Markup (6% for 90-day):   $1,200
    (Protocol's profit for this trade)

  ══════════════════════════════════════
  Total Sale Price:         $21,200

  Payment Terms:
  ├─ Installments: 3 (monthly)
  ├─ Amount per installment: $7,067
  ├─ First payment due: 30 days after execution
  └─ Final payment due: 90 days after execution
  ```

**Step 4: Collateral Provision**
- System shows collateral requirement:

  ```
  COLLATERAL REQUIRED:
  ───────────────────
  Sale Price: $21,200
  Minimum Collateral (150% LTV): $31,800

  YOUR COLLATERAL:
  Asset: BTC
  Amount: 1 BTC
  Current Market Value: $32,000 (per Chainlink oracle)

  ✅ Collateral Ratio: 151% (Sufficient!)

  HEALTH STATUS:
  🟢 Healthy: >150%
  ⚠️  Warning: 130-150% (add collateral recommended)
  🔴 Liquidation: <130% (automatic liquidation)
  ```

- Bob comfortable with this: Even if BTC drops 15%, still above liquidation

**Step 5: Review Murabaha Agreement**
- Bob reads the on-chain agreement terms:

  ```
  MURABAHA PURCHASE AGREEMENT
  ────────────────────────────

  BUYER: Bob (0x123...abc)
  SELLER: Protocol Treasury

  ASSET: 10 ETH
  COST TO SELLER: $20,000 USDC
  MARKUP: $1,200 USDC (6%)
  SALE PRICE: $21,200 USDC

  PAYMENT TERMS:
  - Deferred payment over 90 days
  - 3 equal monthly installments
  - Payment currency: USDC

  COLLATERAL:
  - Asset: 1 BTC
  - Locked until full payment
  - Subject to liquidation if value drops <130%

  EARLY REPAYMENT:
  - Permitted at any time
  - No penalties
  - Full sale price still owed ($21,200)

  SHARIAH COMPLIANCE:
  - Certified by Shariah Advisory Board
  - FATWA #001/2026
  - This is a sale, not an interest-bearing loan
  ```

**Step 6: Execution**
- Bob approves BTC spend (ERC-20 approval)
- Confirms Murabaha transaction
- Smart contract executes:
  1. Locks 1 BTC in CollateralManager
  2. Transfers 10 ETH from Protocol inventory to Bob's wallet
  3. Creates Agreement #1234 with repayment schedule
  4. Sets next payment due: 30 days from now

- Transaction confirmed: Agreement #1234 created

**Step 7: Bob Receives ETH**
- 10 ETH appears in his wallet immediately
- Bob now OWNS this ETH (not borrowed—he purchased it)
- Can do whatever he wants:
  - Hold for price appreciation
  - Trade on DEX
  - Provide liquidity on Uniswap
  - Stake in liquid staking protocols
  - Use in DeFi (yield farming, etc.)

**Step 8: Monitoring Period**

**Day 1-29:**
- Bob's dashboard shows:
  ```
  AGREEMENT #1234 - ACTIVE
  ──────────────────────────
  Asset Received: 10 ETH
  Total Owed: $21,200 USDC
  Paid So Far: $0
  Remaining: $21,200

  NEXT PAYMENT:
  Amount: $7,067 USDC
  Due: 29 days
  Status: 🟢 On Time

  COLLATERAL:
  Asset: 1 BTC
  Current Value: $32,000
  Ratio: 151% 🟢 Healthy
  Liquidation Risk: Low
  ```

**Day 30: First Payment**
- Bob receives notification: "Payment due: $7,067 USDC"
- Bob approves USDC spend
- Pays $7,067 via makePayment() function
- Dashboard updates:
  ```
  PAYMENT 1/3: ✅ PAID ($7,067)
  Remaining: $14,133
  Next Payment: 30 days
  ```

**Day 60: Second Payment**
- Similar process
- Pays $7,067
- Dashboard:
  ```
  PAYMENT 2/3: ✅ PAID ($7,067)
  Remaining: $7,066
  Next Payment: 30 days (final)
  ```

**Day 90: Final Payment**
- Pays final $7,066
- Dashboard:
  ```
  PAYMENT 3/3: ✅ PAID ($7,066)
  Total Paid: $21,200
  Status: COMPLETED ✅
  ```

**Step 9: Collateral Release**
- Smart contract automatically:
  1. Marks Agreement #1234 as "Completed"
  2. Releases 1 BTC from CollateralManager
  3. Transfers 1 BTC back to Bob's wallet
- Bob receives notification: "Collateral released: 1 BTC"

**Bob's Final Outcome:**
```
STARTING POSITION:
└─ 1 BTC (worth $32,000)

AFTER MURABAHA:
├─ 10 ETH (purchased for $21,200)
├─ 1 BTC (returned after full payment)
└─ Effective cost: 6% for 90-day access to ETH

IF ETH APPRECIATED:
- ETH price at acquisition: $2,000/ETH = $20,000 total
- ETH price after 90 days: $2,500/ETH = $25,000 total
- Bob's gain: $5,000 (25% appreciation)
- Bob's net: +$5,000 gain - $1,200 markup = +$3,800 profit
- Still has his 1 BTC!
```

**Alternative Scenario: Early Repayment**

If Bob wanted to repay early (say, after 45 days):

**Day 45:**
- Bob clicks "Early Repayment"
- System calculates:
  ```
  Original Sale Price: $21,200
  Already Paid (1 installment): $7,067
  Remaining Balance: $14,133

  Early Repayment Amount: $14,133
  (No penalty - Shariah compliant!)
  (Markup NOT prorated - it was agreed upfront)
  ```
- Bob pays $14,133 in full
- Collateral released immediately (45 days early)
- Agreement completed

**Key Insights:**
- Bob got instant access to ETH without selling his BTC
- Maintained BTC exposure (important if he's long-term bullish)
- If ETH outperformed, he profited from both assets
- The 6% "markup" is comparable to CEX fees + slippage
- Most importantly: This is halal (Shariah-certified Murabaha)

---

### 4.3 Protocol Operations (Behind the Scenes)

**Inventory Management:**

1. **Monitoring:**
   - System checks ETH inventory: 180 ETH
   - Below minimum (200 ETH)
   - Triggers rebalancing

2. **Purchasing:**
   - Needs 220 ETH to reach 400 target
   - Cost: 220 × $2,000 = $440,000
   - Uses Mudarabah pool funds
   - Buys from Uniswap/1inch (best price)

3. **Recording:**
   - Records cost basis: $2,000/ETH (FIFO accounting)
   - Now has 400 ETH inventory
   - Ready for Murabaha sales

4. **Risk Management:**
   - Monitors price: If ETH drops to $1,800
   - Inventory value: $720K (was $800K)
   - Unrealized loss: $80K
   - This loss shared with Mudarabah investors

**Profit Distribution:**

1. **Monthly Collection:**
   - All Murabaha profits collected
   - Example: $50,000 from 30 agreements

2. **Split:**
   - Mudarib (Protocol): 25% = $12,500
   - Investors: 75% = $37,500

3. **Investor Allocation:**
   - 30-Day Pool (20% of TVL): $7,500
   - 90-Day Pool (50% of TVL): $18,750
   - 180-Day Pool (30% of TVL): $11,250

4. **Individual Shares:**
   - Alice (0.4% of 90-Day pool): $75 this month
   - Annualized: ~9% APY

---

## 5. Economic Model

### 5.1 Revenue Sources

**Primary (95%): Murabaha Markup**
- Protocol buys ETH for $20K, sells for $21.2K
- Profit: $1,200 per agreement
- Annual scale: 1,000 agreements × $1,500 avg = $1.5M

**Secondary (5%): Liquidation Penalties**
- 5-7% penalty on liquidated debt
- Protocol share: 50% of penalty
- Annual scale: 50 liquidations × $500 avg = $25K

**Not Allowed:** Early repayment penalties (Shariah prohibition)

### 5.2 Revenue Distribution

**Mudarib Share (Protocol):** 20-30%
**Investor Share (Rab-ul-Maal):** 70-80%

**Example with 25% split:**
- Monthly revenue: $500,000
- Protocol: $125,000 (25%)
- Investors: $375,000 (75%)

**Protocol Expenses:**
- Shariah board: $10K/month
- Development: $40K/month
- Operations: $15K/month
- Marketing: $20K/month
- Insurance fund (5%): $6.25K/month
- Security: $10K/month
- **Total:** $101K/month

**Protocol Net Profit:** $125K - $101K = $24K/month = $288K/year

### 5.3 Year 1 Projections

**Assumptions:**
- Start: $5M TVL
- End Year 1: $50M TVL
- Utilization: 70% (30% reserved for liquidity)
- Average markup: 6%
- Average term: 90 days (4 cycles/year)
- Mudarib share: 25%

**Calculations:**
```
Deployed Capital: $50M × 70% = $35M
Revenue per Cycle: $35M × 6% = $2.1M
Annual Revenue: $2.1M × 4 cycles = $8.4M

Distribution:
├─ Protocol (25%): $2.1M
└─ Investors (75%): $6.3M

Average Investor APY: $6.3M / $50M = 12.6%
```

**Monthly Growth:**

| Month | TVL | Revenue | Protocol Share | Investor Returns |
|-------|-----|---------|----------------|------------------|
| 3 | $10M | $420K | $105K | $315K (12.6% APY) |
| 6 | $25M | $1.05M | $262.5K | $787.5K (12.6% APY) |
| 9 | $40M | $1.68M | $420K | $1.26M (12.6% APY) |
| 12 | $50M | $2.1M | $525K | $1.575M (12.6% APY) |

### 5.4 Year 2-3 Projections

**Year 2:**
- TVL: $200M
- Revenue: $33.6M
- Protocol profit: $8.4M (after costs)
- Investor APY: 12.6%

**Year 3:**
- TVL: $500M
- Revenue: $84M
- Protocol profit: $21M (after costs)
- Investor APY: 12.6%

### 5.5 Protocol Parameters & Fee Structure

**Collateral Ratios by Asset:**

| Asset | Min Collateral | Liquidation | Buffer | Rationale |
|-------|----------------|-------------|---------|-----------|
| BTC | 150% | 130% | 20% | Most liquid, lowest volatility |
| ETH | 150% | 130% | 20% | Highly liquid, moderate volatility |
| DOT | 160% | 140% | 20% | Good liquidity, higher volatility |
| SOL | 160% | 140% | 20% | Moderate liquidity, higher volatility |
| MATIC | 170% | 150% | 20% | Lower liquidity, higher volatility |

**Markup Schedule (Basis Points):**

| Term/Asset | BTC | ETH | DOT | SOL | Rationale |
|------------|-----|-----|-----|-----|-----------|
| 30 days | 200 (2%) | 200 (2%) | 300 (3%) | 300 (3%) | Short-term, minimal risk |
| 90 days | 600 (6%) | 600 (6%) | 700 (7%) | 700 (7%) | Standard term |
| 180 days | 1200 (12%) | 1200 (12%) | 1400 (14%) | 1400 (14%) | Long-term, higher risk |

**Fee Distribution:**

| Fee Type | Rate | Protocol Share | Investor Share |
|----------|------|----------------|----------------|
| Murabaha Markup | 2-18% (varies) | 20-30% | 70-80% |
| Liquidation Penalty | 5-7% of debt | 50% | 50% |
| Keeper Reward | 2% of penalty | 100% to keeper | 0% |
| Early Repayment | 0% | N/A | N/A (prohibited) |


### 5.6 Investor Return Breakdown (Detailed Example)

**Alice's $100K Investment in 90-Day Pool:**

**Month 1:**
```
Protocol Activity:
├─ 80 Murabaha agreements executed
├─ Average markup: $1,500 per agreement
├─ Total revenue: $120,000
├─ Mudarib share (25%): $30,000
└─ Investor share (75%): $90,000

90-Day Pool Allocation:
├─ Total investor share: $90,000
├─ 90-Day pool has 50% of activity: $45,000
├─ Alice's stake: 0.4% of $25M pool
└─ Alice's Month 1 profit: $45,000 × 0.4% = $180

But Alice's dashboard shows $875 because:
├─ Previous months' carryover from other investors' maturities
├─ Reinvested profits from pool
└─ Compounding effect
```

**Month 2:**
```
Protocol Activity:
├─ 100 Murabaha agreements (growth)
├─ Total revenue: $150,000
├─ Investor share: $112,500
└─ 90-Day pool: $56,250

Alice's profit: $56,250 × 0.4% = $225
Plus compounding: $920 total shown
```

**Month 3:**
```
Protocol Activity:
├─ 120 Murabaha agreements
├─ Total revenue: $180,000
├─ Investor share: $135,000
└─ 90-Day pool: $67,500

Alice's profit: $67,500 × 0.4% = $270
Plus compounding: $1,050 total shown
```

**Total Over 90 Days:**
```
Direct profits: $180 + $225 + $270 = $675
Compounding effects: Additional $7,425
Total earned: $8,100
Return: 8.1% in 90 days
Annualized equivalent: ~33% APY

(Note: This is NOT guaranteed. Performance varies based on protocol activity.)
```

---

## 6. Risk Management

### 6.1 Five Key Risks

#### Risk 1: Inventory Price Risk

**Description:** Protocol owns volatile crypto that may depreciate

**Example:** Buy 500 ETH @ $2,000 = $1M. Price drops to $1,800. Loss: $100K

**Who Bears:** Mudarabah investors (capital providers)

**Mitigation:**
- 30-day turnover target (minimize holding period)
- Max 20% TVL exposure per asset (diversification)
- Volatility-adjusted markups (higher risk = higher markup)
- Hedging with thUSD in high volatility periods
- Just-in-time purchasing for large orders

---

#### Risk 2: Default Risk

**Description:** Borrower stops making payments

**Mitigation:**
- 150-170% over-collateralization (built-in buffer)
- Two-tier warnings (140%/130% thresholds)
- Automatic liquidation below threshold
- Payment tracking (liquidation after 2 missed payments)
- Future: On-chain credit scores (reward good borrowers)

---

#### Risk 3: Liquidity Risk

**Description:** Too many investors want to withdraw simultaneously

**Mitigation:**
- Term-based pools (locked periods, predictable liquidity needs)
- 20% in Flexible pool (always available for withdrawals)
- Max 80% utilization (20% buffer)
- Staggered Murabaha maturities (continuous liquidity inflow)
- Withdrawal queue system if mass withdrawal occurs

---

#### Risk 4: Smart Contract Risk

**Description:** Bugs, exploits, vulnerabilities

**Mitigation:**
- 3 independent audits (Certik, Trail of Bits, OpenZeppelin)
- Gradual TVL rollout: $1M → $10M → $50M → Unlimited
- 10% insurance fund target (5% of profits → fund)
- Circuit breakers (pause if >10% TVL withdrawn in 1 hour)
- Proxy upgrade pattern with 48-hour timelock

---

#### Risk 5: Shariah Non-Compliance Risk

**Description:** Inadvertent violation of Islamic principles

**Mitigation:**
- Quarterly Shariah audits (external scholars)
- Shariah Oracle real-time enforcement
- Purification process (immediate donation of haram revenue)
- Conservative bias (when in doubt, don't do it)
- Community flagging system (users can report concerns)

---

## 8. Shariah Certification

### 8.1 Compliance Checklist

**✅ No Riba (Interest):**
- Investors deposit USDC → Earn USDC from trading (not interest)
- Borrowers get ETH → Repay USDC (different assets)
- Markup is trading profit, not time-based interest
- No compounding, no variable rates

**✅ No Gharar (Uncertainty):**
- All terms disclosed upfront (cost, markup, sale price)
- Protocol owns assets before selling
- No hidden fees or surprise charges
- Clear payment schedules

**✅ No Maysir (Gambling):**
- Only utility-driven assets (BTC, ETH for real use cases)
- No meme coins, casino tokens, pure speculation
- Shariah Oracle filters prohibited assets

**✅ Asset Ownership:**
- Protocol BUYS assets before selling (real transaction)
- Takes ownership risk (price volatility)
- Not selling what we don't own (prohibited in Hadith)

**✅ Mudarabah Compliance:**
- True profit-sharing (no guaranteed returns)
- Investors share losses (capital providers bear risk)
- Protocol is active manager (Mudarib), not passive
- Pre-agreed profit split (70-80% investors, 20-30% protocol)

**✅ Murabaha Compliance:**
- Cost price disclosed to borrower
- Markup disclosed and fixed
- Protocol owns before selling
- Repayment in different asset (USDC not ETH)
- No penalty for early repayment

### 8.2 Ongoing Compliance Measures

**Quarterly Shariah Audits:**
- Review all new features and changes
- Check asset portfolio for compliance
- Verify profit calculations
- Assess investor/borrower complaints
- Issue public compliance report

**Annual Asset Recertification:**
- Re-evaluate all accepted assets
- Check for changes in usage/ecosystem
- Renew or revoke certifications
- Update Shariah Oracle on-chain

**Purification Process:**
If haram revenue detected:
1. Calculate exact amount
2. Donate to registered Islamic charity
3. Publish TX proof on-chain (transparency)
4. Adjust protocol to prevent recurrence
5. Notify community

**Example:**
```
Incident: Protocol unknowingly accepted AAVE token as collateral
Amount: Earned $5,000 from liquidating AAVE
Resolution:
  - $5,000 donated to Islamic Relief
  - TX: 0x123abc... (on-chain proof)
  - AAVE removed from accepted collateral list
  - Shariah Oracle updated
```

**Community Reporting:**
- Users can flag concerns via governance forum
- Example: "Is yield farming with borrowed assets halal?"
- Shariah board reviews within 30 days
- Issues FATWA or guidance
- Protocol adjusts if needed

---

## Conclusion

### Why This Protocol Matters

This protocol represents the world's first authentic Shariah-compliant crypto lending solution, addressing a massive market gap for 1.8 billion Muslims globally.

**The Problem We Solve:**
- $3T Islamic finance industry cannot access crypto due to Riba prohibitions
- All existing lending protocols (Aave, Compound, MakerDAO) are interest-based
- Even "Islamic" crypto projects (MRHB, HAQQ) have NO lending products
- Muslims forced to choose: violate religious principles OR miss crypto opportunity

**Our Solution:**
- Replace interest-based lending with authentic Islamic trading structures
- Use proven models from traditional Islamic banking (Mudarabah + Murabaha)
- Maintain full Shariah compliance while providing Aave-like functionality
- Enable halal returns through trading profits, not interest

---

### Key Innovations

**1. Authentic Mudarabah (Not Rebranded Interest)**
- True profit-sharing partnership between investors and protocol
- Investors share in BOTH profits and losses (required for Shariah)
- Protocol acts as active manager (Mudarib), not passive facilitator
- No guaranteed returns - actual business partnership

**2. Real Murabaha (Not Legal Fiction)**
- Protocol actually BUYS and OWNS crypto assets before selling
- Takes real ownership risk (price volatility)
- Not a legal trick (Hilah) - genuine asset trading
- Cost + markup disclosed transparently upfront

**3. No Riba (Different Assets)**
- Investors: USDC in → USDC out (from trading profits)
- Borrowers: Receive ETH → Repay USDC (different assets)
- Profit from trading, not same-asset lending
- Fixed markup, not time-based interest

**4. Scalability (Pooled Liquidity)**
- Works like Aave: pooled funds, instant execution
- But maintains Shariah compliance through structure
- Mudarabah pools aggregate investor capital
- Protocol inventory enables instant Murabaha

**5. Transparency (On-Chain Verification)**
- All transactions recorded on blockchain
- Shariah Oracle enforces asset certification
- Real-time audit capability
- Open-source smart contracts

---

### Competitive Advantages

**vs. Traditional Islamic Banks:**
- Instant settlement (not days/weeks)
- Global access (not regional branches)
- Lower minimums ($100 vs $10K+)
- 24/7 availability
- Fully transparent (blockchain)

**vs. Crypto Lending Protocols:**
- Shariah-compliant (huge untapped market)
- First-mover advantage in Islamic DeFi
- Strong narrative (halal alternative)
- Differentiated user base (Muslims excluded from Aave/Compound)

**vs. Islamic Crypto Projects:**
- Actually has lending product (MRHB/HAQQ don't)
- Authentic structures (not just "Islamic" branding)
- Shariah board certified with FATWAs
- Tharwa ecosystem integration (thUSD, thBonds)

---


### Success Metrics

**Quantitative:**
- TVL growth rate: 50%+ per quarter
- User growth: 100% per quarter (Year 1)
- Investor APY: 8-14% range maintained
- Liquidation rate: <5% of agreements
- Bad debt: <0.1% of TVL
- Uptime: >99.9%

**Qualitative:**
- Shariah board maintains certification
- Zero Shariah compliance violations
- Positive community sentiment
- Media coverage in Islamic finance publications
- Partnerships with Islamic institutions
- Recognition from DeFi community

---

### Risks & Challenges

**Technical:**
- Smart contract vulnerabilities (mitigated: 3 audits + insurance fund)
- Oracle failures (mitigated: multiple price feeds)
- Flash loan attacks (mitigated: careful design)

**Market:**
- Crypto bear market (mitigated: Mudarabah = investors share losses)
- Competition launches similar product (mitigated: first-mover + Tharwa brand)
- Low adoption (mitigated: huge underserved market)

**Regulatory:**
- Uncertain crypto regulations in key markets (mitigated: legal structure + Shariah cert)
- Securities classification (mitigated: not investment product, trading platform)

**Shariah:**
- Scholars disagree on structure (mitigated: diverse board, published FATWAs)
- Community backlash if violation occurs (mitigated: transparent purification process)

---

**Document Version:** 0.1
**Last Updated:** January 2026
