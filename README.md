<!-- Animated Header -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a1b27,100:161b22&height=200&section=header&text=Street_07&fontSize=50&fontColor=58a6ff&animation=fadeIn&fontAlignY=35&desc=Autonomous%20BTC%20Trading%20Agent&descSize=18&descColor=8b949e&descAlignY=55" />

<div align="center">

[![Python](https://img.shields.io/badge/Python_3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Kraken](https://img.shields.io/badge/Kraken_CLI-5741D9?style=for-the-badge&logo=kraken&logoColor=white)](https://docs.kraken.com/cli/)
[![Base](https://img.shields.io/badge/Base_Sepolia-0052FF?style=for-the-badge&logo=coinbase&logoColor=white)](https://base.org)
[![License](https://img.shields.io/badge/License-MIT-444444?style=for-the-badge)](LICENSE)

<br/>

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=18&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&width=600&lines=13-Indicator+Confluence+Strategy;ERC-8004+On-Chain+Trustless+Logging;Built+for+Surge+%C3%97+Kraken+Hackathon" alt="Typing SVG" />

</div>

---

## ▸ Overview

**Street_07** is an autonomous crypto trading agent that monitors live Bitcoin market data, evaluates trading conditions using a 13-indicator confluence strategy, and executes trades via the Kraken CLI. It features on-chain trustless execution by registering its agent identity and logging trade intents on Base Sepolia using the **ERC-8004** standard.

---

## ▸ Features

<table>
  <tr>
    <td width="25%" align="center"><strong>Confluence Engine</strong></td>
    <td>13 technical indicators — VWAP, MACD, RSI, Heiken Ashi, Parabolic SAR, EMAs, and more. Calculates a real-time composite market score before any position entry.</td>
  </tr>
  <tr>
    <td align="center"><strong>Kraken Execution</strong></td>
    <td>Automatically places <code>[DRY RUN]</code> paper trades via Kraken CLI when the confluence score crosses the entry threshold.</td>
  </tr>
  <tr>
    <td align="center"><strong>On-Chain Logging</strong></td>
    <td>Registers agent identity and logs every trade intent as an immutable ERC-8004 checkpoint on Base Sepolia.</td>
  </tr>
  <tr>
    <td align="center"><strong>Risk Management</strong></td>
    <td>Session filters (Tokyo/London/NY bands), 1% risk profiling, and a 3-tranche exit strategy (Stop Loss → TP1 → TP2).</td>
  </tr>
  <tr>
    <td align="center"><strong>Live Dashboard</strong></td>
    <td>Streamlit web UI to start, stop, and monitor the agent's live terminal output and indicator states.</td>
  </tr>
</table>

---

## ▸ Architecture

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#0d1117',
    'primaryTextColor': '#c9d1d9',
    'primaryBorderColor': '#30363d',
    'lineColor': '#58a6ff',
    'secondaryColor': '#161b22',
    'tertiaryColor': '#21262d'
  }
}}%%
graph LR
    classDef data fill:#1f2428,stroke:#58a6ff,stroke-width:2px,color:#fff,rx:8,ry:8
    classDef brain fill:#4a1e4e,stroke:#bc8cff,stroke-width:2px,color:#fff,rx:8,ry:8
    classDef logic fill:#003d2e,stroke:#2ea043,stroke-width:2px,color:#fff,rx:8,ry:8
    classDef action fill:#4a2c00,stroke:#d29922,stroke-width:2px,color:#fff,rx:8,ry:8
    classDef onchain fill:#0e2d5c,stroke:#3b82f6,stroke-width:2px,color:#fff,rx:8,ry:8
    classDef db fill:#161b22,stroke:#58a6ff,stroke-width:2px,color:#fff

    subgraph Inputs["📡 Market Feeds"]
        A["📈 Kraken WebSockets"]:::data
    end
    
    subgraph Core["🧠 Autonomous Engine"]
        B{"🤖 Agent Core"}:::brain
        C["📊 13-Indicator Confluence"]:::logic
        H["🖥️ Streamlit Dashboard"]:::data
    end
    
    subgraph Execution["⚡ Execution Layer"]
        D["💸 Kraken CLI (Execute Trade)"]:::action
        E["🛑 Hold / Monitor"]:::action
    end
    
    subgraph Blockchain["⛓️ Web3 Logging"]
        F["🔐 ERC-8004 Logger"]:::onchain
        G[("🌐 Base Sepolia Testnet")]:::db
    end

    %% Flow
    A -->|Live Tickers| B
    H <-->|Control/Monitor| B
    B -->|Tick Data| C
    
    %% Logic branching
    C -->|Score >= Threshold| D
    C -->|Score < Threshold| E
    
    %% Blockchain logging
    B -.->|Trade Intent| F
    F ==>|Immutable Checkpoint| G
```

---

## ▸ Indicators

<details>
<summary><strong>View all 13 indicators used in the confluence engine</strong></summary>
<br/>

| # | Indicator | Signal Type |
|---|---|---|
| 1 | **VWAP** | Volume-weighted average price |
| 2 | **MACD** | Trend momentum + signal crossover |
| 3 | **RSI** | Overbought / oversold detection |
| 4 | **Heiken Ashi** | Smoothed candlestick patterns |
| 5 | **Parabolic SAR** | Trend direction + trailing stop |
| 6 | **EMA 9** | Short-term exponential moving average |
| 7 | **EMA 21** | Medium-term exponential moving average |
| 8 | **EMA 50** | Long-term trend filter |
| 9 | **Bollinger Bands** | Volatility + mean reversion |
| 10 | **Stochastic RSI** | Momentum oscillator |
| 11 | **ADX** | Trend strength measurement |
| 12 | **OBV** | On-balance volume flow |
| 13 | **ATR** | Average true range for position sizing |

Each indicator votes ±1. The composite score determines entry/exit signals.

</details>

---

## ▸ Prerequisites

- **Python 3.8+**
- **Kraken CLI** — configured with a Read-Only API key ([docs](https://docs.kraken.com/cli/))
- **Web3 Wallet** — loaded with Base Sepolia testnet ETH
- **Pinata / IPFS** — for Agent Card URI hosting

---

## ▸ Setup

```bash
git clone https://github.com/shashankrpatil077-ctrl/Street_07.git
cd Street_07
pip install -r requirements.txt
```

Create a `.env` file in the root directory:

```env
KRAKEN_API_KEY=your_kraken_api_key
KRAKEN_PRIVATE_KEY=your_kraken_private_key
WEB3_WALLET_PRIVATE_KEY=your_wallet_private_key
RPC_URL=your_base_sepolia_rpc_url
PINATA_API_KEY=your_pinata_api_key
PINATA_SECRET_API_KEY=your_pinata_secret_key
```

---

## ▸ Usage

**Dashboard mode:**
```bash
streamlit run app.py
```

**Direct execution:**
```bash
python agent.py
```

---

## ▸ License

MIT License — see [LICENSE](LICENSE) for details.

<!-- Animated Footer -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:161b22,50:1a1b27,100:0d1117&height=120&section=footer" />
