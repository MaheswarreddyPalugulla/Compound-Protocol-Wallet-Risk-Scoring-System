# Compound Protocol Wallet Risk Scoring System

A comprehensive risk assessment system that analyzes wallet interactions with Compound V2/V3 protocols to generate risk scores from 0-1000 for DeFi lending decisions.

## 🎯 Overview

This system processes wallet addresses and their historical blockchain transactions to assess lending risk in the Compound ecosystem. Using real-time data from Etherscan API, it analyzes transaction patterns, borrowing behavior, liquidation history, and portfolio composition to generate actionable risk scores.

## 🚀 Features

- **Real-time Data Collection**: Fetches live transaction data from Etherscan API
- **Comprehensive Protocol Coverage**: Monitors all major Compound V2 and V3 contracts
- **Multi-dimensional Risk Assessment**: 8 weighted risk factors for holistic evaluation
- **Production Ready**: Built-in rate limiting, error handling, and scalability
- **Clear Scoring**: Risk scores from 1-1000 with interpretable categories
- **Export Ready**: CSV output format for integration with other systems

## 📊 Results Summary

- **Wallets Processed**: 103/103 (100% success rate)
- **Active Wallets Identified**: 50 (48.5%)
- **Total Compound Transactions**: 598
- **Processing Time**: ~7 minutes
- **Risk Categories**: Low (0-300), Medium (301-600), High (601-1000)

## 🛠 Installation

### Prerequisites
```bash
pip install pandas numpy requests matplotlib seaborn scikit-learn tqdm