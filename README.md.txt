# 🚀 Autonomous BTC Trading Agent

Built for the **Surge x Kraken AI Trading Agents Hackathon** on lablab.ai.

This project is an autonomous crypto trading agent that monitors live Bitcoin (BTC) market data, evaluates conditions using 13 technical indicators, and executes paper trades via the Kraken CLI. It also features Trustless/Web3 integration by registering its agent identity and trade intents on the Base Sepolia testnet using the ERC-8004 standard.

## ✨ Features

- **Algorithmic Trading Engine:** Uses 13 built-in indicators (VWAP, MACD, RSI, Heiken Ashi, Parabolic SAR, EMAs, etc.) to calculate a real-time market score.
- **Kraken CLI Integration:** Automatically executes `[DRY RUN]` paper trades on Kraken when the market score crosses the entry threshold.
- **Web3 Trustless Execution (ERC-8004):** Registers the agent's identity and logs trade intents as on-chain checkpoints on Base Sepolia.
- **Risk Management:** Includes session filters (Tokyo/London/NY bands), 1% risk profiling, and a 3-tranche exit strategy (Stop Loss, Take Profit 1, Take Profit 2).
- **Live Streamlit Dashboard:** A local web UI (`app.py`) to easily start, stop, and monitor the agent's live terminal logs.

## 🛠️ Prerequisites

- Python 3.8+
- [Kraken CLI](https://docs.kraken.com/cli/) installed and configured with a Read-Only API key.
- A Web3 Wallet (MetaMask) with Base Sepolia testnet ETH.
- Pinata / IPFS account for Agent Card URI hosting.

## ⚙️ Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone <your-github-repo-url>
   cd ai_agent_hackathon