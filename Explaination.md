# Compound Protocol Wallet Risk Scoring - Methodology Explanation

## Executive Summary

This document details the comprehensive methodology used to assess risk scores (0-1000) for 103 wallet addresses based on their historical interactions with Compound V2 and V3 protocols. The system successfully processed all wallets, identifying 50 active users with 598 total Compound transactions.

---

## 1. Data Collection Method

### 1.1 Data Sources
- **Primary Source**: Etherscan API for comprehensive blockchain transaction data
- **Coverage Period**: Full transaction history from genesis to present
- **API Endpoints Used**:
  - Regular transactions (`txlist`)
  - ERC20 token transfers (`tokentx`)

### 1.2 Protocol Coverage
**Compound V2 Contracts Monitored:**
- cETH (0x4ddc2d193948926d02f9b1fe9e1daa0718270ed5)
- cDAI (0x5d3a536e4d6dbd6114cc1ead35777bab948e3643)
- cUSDC (0x39aa39c021dfbaae8fac545936693ac917d5e7563)
- cUSDT, cWBTC, cBAT, cREP, cZRX
- Comptroller (0x3d9819210a31b4961b30ef54be2aed79b9c9cd3b)

**Compound V3 Contracts Monitored:**
- cUSDCv3 (0xc3d688b66703497daa19211eedff47f25384cdc3)
- cWETHv3 (0xa17581a9e3356d9a858b789d68b4d866e593ae94)
- cWBTCv3 (0x9c4ec768c28520b50860ea7a15bd7213a9ff58bf)

### 1.3 Operation Detection
**Method Signature Analysis:**
- **Supply Operations**: `0xa0712d68` (mint)
- **Withdraw Operations**: `0xdb006a75` (redeem)
- **Borrow Operations**: `0xc5ebeaec` (borrow)
- **Repay Operations**: `0x0e752702` (repayBorrow)
- **Liquidation Events**: `0xf5e3c462` (liquidateBorrow)

### 1.4 Data Quality Assurance
- **Rate Limiting**: 0.25-second delays between API calls to respect Etherscan limits
- **Error Handling**: Comprehensive exception handling with retry logic
- **Data Validation**: Cross-verification between regular transactions and ERC20 transfers
- **Completeness**: 100% success rate (103/103 wallets processed, 0 failures)

---

## 2. Feature Selection Rationale

### 2.1 Primary Risk Indicators (High Weight)

**Activity Risk (20% Weight)**
- **Rationale**: Wallets with no DeFi history represent unknown risk profiles
- **Implementation**: Graduated scoring based on transaction frequency
- **Business Logic**: Lending protocols require track record for risk assessment

**Liquidation Risk (25% Weight)**
- **Rationale**: Historical liquidations are the strongest predictor of future risk
- **Implementation**: Direct penalty system (300 points per liquidation, capped at 100)
- **Business Logic**: Past liquidations indicate poor risk management

### 2.2 Portfolio Risk Indicators (Medium Weight)

**Borrowing Behavior Risk (15% Weight)**
- **Rationale**: High borrowing ratios indicate aggressive leverage strategies
- **Implementation**: Ratio of borrow operations to total operations
- **Thresholds**: >60% = High Risk, 30-60% = Medium Risk, <30% = Low Risk

**Concentration Risk (15% Weight)**
- **Rationale**: Lack of diversification increases portfolio volatility
- **Implementation**: Count of unique Compound contracts used
- **Thresholds**: 1 contract = High Risk, 2-3 = Medium Risk, 4+ = Low Risk

**Portfolio Balance Risk (10% Weight)**
- **Rationale**: Extreme behaviors (only borrowing/only supplying) indicate imbalanced strategies
- **Implementation**: Analysis of supply vs. borrow operation patterns

### 2.3 Behavioral Risk Indicators (Low Weight)

**Transaction Size Risk (5% Weight)**
- **Rationale**: Very large transactions may indicate institutional or whale behavior
- **Implementation**: Average transaction value analysis in ETH

**Account Age Risk (5% Weight)**
- **Rationale**: Very new accounts lack established track records
- **Implementation**: Days between first and last Compound interaction

**Frequency Risk (5% Weight)**
- **Rationale**: Unusual transaction patterns may indicate automated strategies
- **Implementation**: Transaction frequency per day analysis

---

## 3. Scoring Method

### 3.1 Individual Risk Factor Calculation
- **Scale**: Each risk factor scored 0-100 points
- **Direction**: Higher scores indicate higher risk
- **Methodology**: Threshold-based scoring with graduated penalties

### 3.2 Weighted Aggregation