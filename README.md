# 🧠 Wallet Risk Scoring Engine

A high-performance Python tool to assess and score Ethereum wallet addresses based on on-chain behavior and DeFi interactions.  
This engine uses real-time data from **Compound Protocol (v2 & v3)** and **Etherscan API** to assign a **risk score (0–1000)**, designed to aid in wallet profiling, fraud detection, credit analysis, and DeFi risk modeling.

---

## 📌 Overview

The Wallet Risk Scoring Engine enables you to:
- ✅ Analyze **borrowing and repayment behavior** on Compound
- ✅ Evaluate **transaction history and contract activity**
- ✅ Score wallets on a **non-linear scale** from 0 (low risk) to 1000 (high risk)
- ✅ Process large address batches with optimized throttling
- ✅ Export results in clean CSV format with full statistics

This system is ideal for researchers, risk teams, dApp developers, and analysts looking to measure wallet reliability, trustworthiness, or financial behavior.

---

## 🚀 Key Features

- 🔗 Integration with **The Graph** for Compound data (v2 & v3)
- 🔍 Live **transaction fetching via Etherscan API**
- 📈 Dual scoring system: **Protocol Risk** and **Activity Risk**
- ⚖️ Smart **non-linear final adjustment** for better score separation
- 📁 Batch processing with **TQDM** progress feedback
- 💾 Output includes score statistics and top risk wallet summary

---

## 📂 Project Structure

```
├── Wallet_Risk_Scoring_Engine.ipynb             # Main executable script
├── wallets.csv                  # Input file containing wallet addresses
├── requirements.txt             # Python dependencies
└── README.md                    # Documentation (this file)
```

---

## 🧠 Scoring Algorithm

### 1. **Protocol Risk** (0–600 points)
- Borrow Amount (non-linear scaled)
- Repayment Ratio (penalizes poor repayment)
- Liquidation Count (heavy penalty per event)

### 2. **Activity Risk** (0–400 points)
- Total Transactions (non-linear reward)
- Smart Contract Interactions (heavily weighted)
- Recent Transactions (boosts active wallets)

### Final Score = Adjusted sum of both components:

```python
final_score = min(int(raw_score * (1 + raw_score / 800)), 1000)
```

This helps stretch and separate mid-tier scores more effectively.

---

## 📦 Installation

Make sure you have Python 3.7+ and `pip` installed.

```bash
git clone https://github.com/yourusername/wallet-risk-scoring.git
run Wallet_Risk_Scoring_Engine.ipynb

```

---

## 📄 Input Format

The input file `wallets.csv` should have the following structure:

```csv
wallet_id
0x0039f22efb07a647557c7c5d17854cfd6d489ef3
0x06b51c6882b27cb05e712185531c1f74996dd988
...
```

---

## ▶️ Usage

Run the scoring engine with:

```bash
run Wallet_Risk_Scoring_Engine.ipynb
```

This will:
- Load addresses from `wallets.csv`
- Fetch protocol and transaction data
- Compute risk scores
- Save the results to `wallet_risk_scores_final.csv`
- Display final stats and top 5 riskiest wallets

---

## ✅ Example Output

### Sample from `wallet_risk_scores_final.csv`:

```csv
wallet_id,score
0x0039f22efb07a647557c7c5d17854cfd6d489ef3,600
0x06b51c6882b27cb05e712185531c1f74996dd988,432
...
```

---

## 📊 Real Execution Results

```
Generating scores: 100%|██████████| 103/103 [02:05<00:00,  1.21s/it]

Final Score Distribution:
count    103.000000
mean      67.893204
std      130.295510
min        0.000000
25%       10.000000
50%       15.000000
75%       42.500000
max      600.000000
```

### Top 5 Riskiest Wallets:

| Wallet Address                              | Score |
|---------------------------------------------|-------|
| `0x0039f22efb07a647557c7c5d17854cfd6d489ef3` | 600   |
| `0x96479b087cb8f236a5e2dcbfc50ce63b2f421da6` | 600   |
| `0x70d8e4ab175dfe0eab4e9a7f33e0a2d19f44001e` | 599   |
| `0xa7f3c74f0255796fd5d3ddcf88db769f7a6bf46a` | 512   |
| `0xf340b9f2098f80b86fbc5ede586c319473aa11f3` | 498   |

---

## 🔌 APIs Used

- 🧠 [Compound v2 Subgraph](https://thegraph.com/hosted-service/subgraph/graphprotocol/compound-v2)
- 🧠 [Compound v3 Subgraph](https://thegraph.com/hosted-service/subgraph/compound-finance/compound-v3)
- 🧾 [Etherscan API](https://etherscan.io/apis)

You’ll need to set your `ETHERSCAN_API_KEY` inside the script.

---

## ⚙️ Configuration Options

Inside `risk_scoring.py`:

```python
SCORE_MAX = 1000
BATCH_SIZE = 3
DELAY_SECONDS = 2
ETHERSCAN_API_KEY = "your-api-key"
```

You can customize these to control batch size and API rate limits.

---

## 🧭 Roadmap

- [ ] Add support for Aave and MakerDAO scoring
- [ ] Integrate anomaly detection via ML models
- [ ] REST API for score querying
- [ ] Real-time scoring dashboard with charts

---

## 🤝 Contributing

Contributions are welcome!  
Please fork the repo and submit a pull request, or open an issue to discuss improvements.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Siddhi Patil**  
📧 siddhipatil064@gmail.com  
🎓 B.E. Computer Engineering | DeFi Enthusiast | AI/ML + Blockchain Researcher

