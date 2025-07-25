# Compound Protocol Wallet Risk Scoring System

This project analyzes Ethereum wallet risk using real Compound protocol data and Etherscan API. It collects transaction data, engineers risk features, calculates a comprehensive risk score, and exports results for further analysis.

## Features
- **Automated Data Collection:** Fetches on-chain transaction and token transfer data for a list of wallets using the Etherscan API.
- **Compound Protocol Focus:** Filters and analyzes interactions with Compound V2 and V3 contracts.
- **Risk Feature Engineering:** Computes activity, liquidation, borrowing, concentration, size, time, balance, and frequency risk factors.
- **Comprehensive Risk Scoring:** Combines features into a 0-1000 risk score using weighted aggregation and normalization.
- **Visualization:** Provides plots and summaries for risk distribution and wallet behaviors.
- **Export:** Outputs main deliverable (`wallet_risk_scores.csv`) and detailed analysis (`detailed_wallet_analysis.csv`).

## Setup Instructions
1. **Clone or Download the Repository**
2. **Install Python 3.8+ and Required Packages**
   - Recommended: Use a virtual environment.
   - Install dependencies:
     ```bash
     pip install pandas numpy requests matplotlib seaborn scikit-learn tqdm
     ```
3. **Obtain API Keys**
   - **Etherscan API Key (Required):**
     - Sign up at https://etherscan.io/apis
     - Create a free API key
     - Replace the placeholder in the notebook (`ETHERSCAN_API_KEY`)
   - **Alchemy API Key (Optional):**
     - For advanced/fast data collection (not required for basic use)
     - Sign up at https://www.alchemy.com/
     - Create an Ethereum Mainnet app and copy the API key

4. **Prepare Input Data**
   - Place your wallet list in a CSV file named `Wallet id - Sheet1.csv` with a column `wallet_id`.

5. **Run the Notebook**
   - Open `code.ipynb` in Jupyter or VS Code.
   - Follow the cell order:
     1. Import libraries and set API keys
     2. Load wallet addresses
     3. Run helper/data collection functions
     4. Collect data (may take time due to rate limits)
     5. Feature engineering and risk scoring
     6. Visualization and export

## Output Files
- `wallet_risk_scores.csv`: Main deliverable with `wallet_id` and `score` columns
- `detailed_wallet_analysis.csv`: Extended analysis for each wallet

## Methodology Summary
- **Data Sources:** Etherscan API (transactions, internal txs, ERC20 transfers)
- **Compound Contracts:** V2 & V3 (see notebook for full list)
- **Risk Factors:** Activity, liquidation, borrowing, concentration, size, time, balance, frequency
- **Scoring:** Weighted sum, normalized to 0-1000
- **Categories:**
  - 0-300: Low risk
  - 301-600: Medium risk
  - 601-1000: High risk

## Troubleshooting
- If you hit rate limits, increase the delay between API calls in the notebook.
- If you get empty results, check your API key and wallet address formatting.
- For large wallet lists, processing may take 20+ minutes.

## License
MIT License

## Author
Maheswarreddy Palugulla

---
For questions or support, see the notebook's API setup instructions or contact the author.

📈 Risk Scoring
Risk Factors (Weighted)

Liquidation History (25%) - Past liquidation events
Activity Level (20%) - Transaction frequency
Borrowing Behavior (15%) - Borrowing patterns
Portfolio Concentration (15%) - Diversification
Balance Patterns (10%) - Supply vs borrow ratio
Transaction Characteristics (25%) - Size, frequency, timing

Score Interpretation

1-300: Low Risk (Conservative users)
301-600: Medium Risk (Moderate activity)
601-1000: High Risk (Aggressive or unknown)

📊 Sample Output
csvwallet_id,score
0xfaa0768bde629806739c3a4620656c5d26f44ef2,732
0x1234567890123456789012345678901234567890,156