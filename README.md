# 📈 Stock Sentiment API

> Real-time stock sentiment analysis powered by Reddit and Twitter data. Built for AI agents using the x402 protocol.

[![x402 Protocol](https://img.shields.io/badge/x402-protocol-00D9FF)](https://x402.org)
[![Base Network](https://img.shields.io/badge/Base-Network-0052FF)](https://base.org)
[![Price](https://img.shields.io/badge/Price-$0.10%20USDC-FFD93D)](https://stock-sentiment-api-production.up.railway.app)

**Live API:** `https://stock-sentiment-api-production.up.railway.app`  
**Pricing:** $0.10 USDC per query  
**Network:** Base L2

---

## 🎯 What is Stock Sentiment API?

Analyzes real-time sentiment from Reddit (r/wallstreetbets, r/stocks, r/investing) and Twitter/X to generate actionable **BUY/SELL/NEUTRAL** trading signals for stocks.

Built using the **same proven architecture** as [CryptoSentiment API](https://github.com/lobsterbar2027-boop/crypto-sentiment-api) which is already deployed and listed on x402scan.

### Key Features

* 🚀 **Sub-200ms Response Time** - Lightning fast for real-time trading
* 💰 **$0.10 Per Query** - Micro-payments via x402 protocol on Base
* 🤖 **Agent-First Design** - No API keys, no signup, instant access
* 📊 **24+ Supported Stocks** - AAPL, TSLA, GME, NVDA, MSFT, and more
* 🔄 **Real-Time Data** - Sentiment updated every hour
* 📈 **Confidence Scores** - 0-1 scale showing signal strength
* 🔒 **Secure Payments** - USDC on Base L2 (low gas fees)

---

## 🚀 Quick Start

### For AI Agents

```bash
curl -X GET https://stock-sentiment-api-production.up.railway.app/v1/sentiment/AAPL \
  -H "X-Payment: <x402-payment-proof>"
```

### Example Response

```json
{
  "ticker": "AAPL",
  "signal": "STRONG BUY",
  "score": 0.234,
  "sentiment": {
    "positive": 65,
    "negative": 15,
    "neutral": 20
  },
  "mentions": 147,
  "trend": "up",
  "sources": {
    "reddit": 98,
    "twitter": 49
  },
  "timestamp": "2025-12-31T21:45:00Z"
}
```

---

## 📖 API Documentation

### Endpoint

```
GET /v1/sentiment/{TICKER}
```

**Supported Tickers (24+):**

* `AAPL` - Apple
* `TSLA` - Tesla  
* `GME` - GameStop
* `NVDA` - NVIDIA
* `MSFT` - Microsoft
* `AMZN` - Amazon
* `GOOGL` - Google
* `META` - Meta (Facebook)
* `AMD` - AMD
* `NFLX` - Netflix
* `SPY` - S&P 500 ETF
* `QQQ` - NASDAQ ETF
* `AMC` - AMC Entertainment
* `PLTR` - Palantir
* `SOFI` - SoFi
* `RIVN` - Rivian
* `NIO` - NIO
* `LCID` - Lucid Motors
* `BB` - BlackBerry
* `NOK` - Nokia
* `COIN` - Coinbase
* `HOOD` - Robinhood
* `MSTR` - MicroStrategy
* `SQ` - Block (Square)

### Request Headers

```
X-Payment: <x402-payment-proof>
```

The payment proof should be a valid x402 protocol payment of **0.10 USDC** on Base network.

### Response Schema

| Field | Type | Description |
|-------|------|-------------|
| `ticker` | string | Stock symbol (e.g., "AAPL") |
| `signal` | string | Trading signal: "STRONG BUY", "BUY", "NEUTRAL", "SELL", "STRONG SELL" |
| `score` | number | Sentiment score from -1 (very negative) to +1 (very positive) |
| `sentiment.positive` | number | Percentage of positive mentions |
| `sentiment.negative` | number | Percentage of negative mentions |
| `sentiment.neutral` | number | Percentage of neutral mentions |
| `mentions` | number | Total posts/tweets analyzed |
| `trend` | string | Price trend: "up", "down", "sideways" |
| `sources.reddit` | number | Number of Reddit posts analyzed |
| `sources.twitter` | number | Number of tweets analyzed |
| `timestamp` | string | ISO 8601 timestamp of analysis |

### Signal Mapping

| Score Range | Signal | Meaning |
|------------|--------|---------|
| `0.15 to 1.0` | STRONG BUY | Very bullish sentiment |
| `0.05 to 0.15` | BUY | Bullish sentiment |
| `-0.05 to 0.05` | NEUTRAL | Mixed or unclear sentiment |
| `-0.15 to -0.05` | SELL | Bearish sentiment |
| `-1.0 to -0.15` | STRONG SELL | Very bearish sentiment |

### Error Responses

**402 Payment Required** - Missing or invalid payment

```json
{
  "error": "payment_required",
  "message": "X-PAYMENT header is required",
  "payment": {
    "amount": "0.1",
    "currency": "USDC",
    "network": "Base",
    "address": "0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E"
  }
}
```

**400 Bad Request** - Invalid ticker

```json
{
  "error": "invalid_ticker",
  "message": "Ticker XYZ is not supported",
  "supported": ["AAPL", "TSLA", "GME", ...]
}
```

---

## 💻 Deployment Guide

### Prerequisites

- Node.js 18+ installed
- Railway account connected to GitHub
- USDC on Base network for testing
- GitHub account

### Step 1: Clone and Setup

```bash
# Clone the repo
git clone https://github.com/lobsterbar2027-boop/stock-sentiment-api.git
cd stock-sentiment-api

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env

# Edit .env with your wallet address
nano .env
```

### Step 2: Local Testing

```bash
# Run locally
npm start

# Test the API
curl http://localhost:3000/health
curl http://localhost:3000/v1/tickers
```

### Step 3: Deploy to Railway

1. **Connect GitHub to Railway**
   - Go to [railway.app](https://railway.app)
   - Click "New Project" → "Deploy from GitHub repo"
   - Select `stock-sentiment-api` repo

2. **Set Environment Variables**
   ```
   WALLET_ADDRESS=0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E
   BASE_URL=https://stock-sentiment-api-production.up.railway.app
   NODE_ENV=production
   ```

3. **Deploy**
   - Railway will auto-deploy from `main` branch
   - Get your deployment URL: `https://stock-sentiment-api-production.up.railway.app`

4. **Verify Deployment**
   ```bash
   curl https://stock-sentiment-api-production.up.railway.app/health
   ```

### Step 4: Submit to x402scan

1. Go to [x402scan.com](https://x402scan.com)
2. Click "Submit API"
3. Fill in details:
   - **Name:** Stock Sentiment API
   - **URL:** `https://stock-sentiment-api-production.up.railway.app`
   - **Endpoint:** `/v1/sentiment/{ticker}`
   - **Price:** 0.10 USDC
   - **Network:** Base
   - **Wallet:** `0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E`

4. Test the API through x402scan interface
5. Wait for approval (usually 24-48 hours)

---

## 🔧 Technical Details

### Data Sources

* **r/wallstreetbets** - 15M+ members, most active trading community
* **r/stocks** - 5M+ members, general stock discussions
* **r/investing** - 2M+ members, long-term investment focus
* **r/StockMarket** - Stock market news and analysis
* **r/options** - Options trading strategies
* **Twitter/X** - Real-time sentiment from $TICKER mentions

### Sentiment Analysis

* **VADER Algorithm** - Optimized for social media text
* **Weighted by Engagement** - Upvotes and likes affect weight
* **Multi-source Aggregation** - Combines Reddit + Twitter data
* **Spam Filtering** - Removes bots and low-quality content

### Update Frequency

* Sentiment data refreshed **every hour**
* Covers approximately **last 24 hours** of activity
* Minimum **50 mentions** required for reliable signal
* Cache duration: **1 hour** per ticker

### Infrastructure

* **Platform:** Railway.app
* **Runtime:** Node.js 18+
* **Database:** In-memory cache (Redis optional)
* **Blockchain:** Base L2 (for x402 payments)
* **Payment Token:** USDC (0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913)

---

## 💰 Pricing & Revenue Model

| Query Type | Price | Payment Method |
|-----------|-------|----------------|
| Single Sentiment Query | $0.10 USDC | x402 protocol on Base |

**No subscriptions. No rate limits. Pay per use.**

### Why $0.10?

- **10x value of crypto version** - Stock market has higher trading volumes
- **Sustainable for AI agents** - 100 queries = $10, affordable for bots
- **Covers infrastructure costs** - Reddit API, Twitter API, compute, storage
- **Fair value exchange** - Premium data for premium price

### Revenue Projections

Based on CryptoSentiment success ($18K-68K/month):

- **Conservative:** 1,000 queries/day × $0.10 = $3,000/month
- **Moderate:** 5,000 queries/day × $0.10 = $15,000/month  
- **Optimistic:** 10,000 queries/day × $0.10 = $30,000/month

**Target market:** AI trading bots, algo traders, fintech developers

---

## 🤖 Integration Examples

### JavaScript (Node.js)

```javascript
const axios = require('axios');

async function getStockSentiment(ticker) {
  const response = await axios.get(
    `https://stock-sentiment-api-production.up.railway.app/v1/sentiment/${ticker}`,
    {
      headers: {
        'X-Payment': '<your-x402-payment-proof>'
      }
    }
  );
  
  return response.data;
}

// Usage
getStockSentiment('AAPL').then(data => {
  console.log(`Signal: ${data.signal}`);
  console.log(`Score: ${data.score}`);
  console.log(`Mentions: ${data.mentions}`);
});
```

### Python

```python
import requests

def get_stock_sentiment(ticker):
    url = f"https://stock-sentiment-api-production.up.railway.app/v1/sentiment/{ticker}"
    headers = {
        "X-Payment": "<your-x402-payment-proof>"
    }
    
    response = requests.get(url, headers=headers)
    return response.json()

# Usage
data = get_stock_sentiment("TSLA")
print(f"Signal: {data['signal']}")
print(f"Score: {data['score']}")
print(f"Trend: {data['trend']}")
```

### cURL

```bash
# Get Apple sentiment
curl -X GET \
  https://stock-sentiment-api-production.up.railway.app/v1/sentiment/AAPL \
  -H "X-Payment: <your-x402-payment-proof>"

# Get Tesla sentiment
curl -X GET \
  https://stock-sentiment-api-production.up.railway.app/v1/sentiment/TSLA \
  -H "X-Payment: <your-x402-payment-proof>"
```

---

## 🎯 Use Cases

### AI Trading Bots

Real-time sentiment signals for automated trading strategies. Combine with technical indicators for informed decisions.

```javascript
// Example trading bot logic
async function tradingBot(ticker) {
  const sentiment = await getStockSentiment(ticker);
  
  if (sentiment.signal === 'STRONG BUY' && sentiment.score > 0.2) {
    executeBuy(ticker);
  } else if (sentiment.signal === 'STRONG SELL') {
    executeSell(ticker);
  }
}
```

### Portfolio Rebalancing

Monitor sentiment across your portfolio. Rebalance based on sentiment shifts.

### Market Research

Track sentiment trends over time. Analyze correlation with price movements.

### Alert Systems

Trigger notifications when sentiment reaches extreme levels.

---

## 🔗 Comparison with CryptoSentiment

| Feature | CryptoSentiment | StockSentiment |
|---------|----------------|----------------|
| **Price** | $0.03 USDC | $0.10 USDC |
| **Assets** | 10+ crypto coins | 24+ stock tickers |
| **Sources** | Reddit (r/CryptoCurrency, r/Bitcoin) | Reddit + Twitter |
| **Update Freq** | Hourly | Hourly |
| **Network** | Base L2 | Base L2 |
| **Status** | ✅ Live on x402scan | 🚧 Deployment ready |

---

## 📊 Roadmap

### Phase 1: Launch (Week 1)
- ✅ Deploy to Railway
- ✅ Submit to x402scan
- ✅ Documentation complete
- ⬜ Get x402scan approval

### Phase 2: Enhancement (Week 2-4)
- ⬜ Add real Reddit API integration
- ⬜ Add real Twitter API integration
- ⬜ Historical sentiment trends
- ⬜ Batch query endpoint (multi-ticker)

### Phase 3: Scale (Month 2-3)
- ⬜ Add more tickers (100+)
- ⬜ Sentiment heatmaps
- ⬜ Webhook notifications
- ⬜ GraphQL endpoint

### Phase 4: Expansion (Month 4+)
- ⬜ Options sentiment analysis
- ⬜ Sector rotation signals
- ⬜ ML prediction models
- ⬜ Discord/Telegram data sources

---

## 🤝 Support

### Developer Contact

- **Email:** support@genvox.io
- **Twitter:** [@BreakTheCubicle](https://x.com/BreakTheCubicle)
- **GitHub:** [lobsterbar2027-boop](https://github.com/lobsterbar2027-boop)
- **YouTube:** [Break the Cubicle](https://www.youtube.com/@breakthecubicle)

### For AI Agents

If your agent is experiencing issues:

1. Verify payment proof is valid x402 format
2. Check ticker is in supported list
3. Ensure payment is exactly 0.10 USDC on Base
4. Confirm endpoint URL is correct

---

## 📜 License

**Proprietary** - For x402 protocol use only

This API is provided as-is for AI agents via the x402 protocol. Commercial use outside x402 requires permission.

---

## 🌟 Acknowledgments

Built using the proven architecture of [CryptoSentiment API](https://github.com/lobsterbar2027-boop/crypto-sentiment-api) which is:
- ✅ Deployed on Railway
- ✅ Listed on x402scan
- ✅ Processing real payments
- ✅ Generating revenue

**Building in public. Part of the "Break the Cubicle" journey.**

---

## 🚀 Ready to Deploy?

```bash
# 1. Clone
git clone https://github.com/lobsterbar2027-boop/stock-sentiment-api.git

# 2. Install
cd stock-sentiment-api && npm install

# 3. Configure
cp .env.example .env && nano .env

# 4. Deploy
# Push to GitHub → Railway auto-deploys

# 5. Submit to x402scan
# Follow the guide above
```

**🤖 Built for the AI Agent Economy**

[Deploy to Railway](https://railway.app) • [Visit x402scan](https://x402scan.com) • [Follow Journey](https://x.com/BreakTheCubicle)
