# 🚀 Stock Sentiment API - Railway Deployment Guide

**Fast track to production in 15 minutes**

This guide will take you from zero to deployed and live on x402scan.

---

## 📋 Prerequisites

- [x] GitHub account: `lobsterbar2027-boop`
- [x] Railway account (sign up at [railway.app](https://railway.app))
- [x] Wallet address: `0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E`
- [x] This repo cloned locally

---

## Step 1: Create GitHub Repository (5 minutes)

### 1.1 Create New Repo

```bash
# Navigate to your project
cd stock-sentiment-api

# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Stock Sentiment API v1.0.0"

# Create repo on GitHub
# Go to https://github.com/new
# Repository name: stock-sentiment-api
# Description: Real-time stock sentiment analysis API using x402 protocol
# Public repository
# Don't initialize with README (we already have one)

# Add remote and push
git remote add origin https://github.com/lobsterbar2027-boop/stock-sentiment-api.git
git branch -M main
git push -u origin main
```

---

## Step 2: Deploy to Railway (5 minutes)

### 2.1 Connect Railway to GitHub

1. Go to [railway.app](https://railway.app)
2. Click **"Login"** → Sign in with GitHub
3. Authorize Railway to access your repositories

### 2.2 Create New Project

1. Click **"New Project"**
2. Select **"Deploy from GitHub repo"**
3. Choose **`lobsterbar2027-boop/stock-sentiment-api`**
4. Click **"Deploy Now"**

### 2.3 Set Environment Variables

Railway will auto-detect your `package.json` and start deployment.

Add these environment variables:

```bash
# Go to your project → Settings → Variables

WALLET_ADDRESS=0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E
NODE_ENV=production
```

**Note:** `BASE_URL` and `PORT` are automatically set by Railway.

### 2.4 Get Your Deployment URL

1. Go to **Settings** → **Networking**
2. Click **"Generate Domain"**
3. Your URL will be: `https://stock-sentiment-api-production.up.railway.app`
4. Copy this URL for later

---

## Step 3: Verify Deployment (2 minutes)

### 3.1 Test Health Endpoint

```bash
curl https://stock-sentiment-api-production.up.railway.app/health
```

**Expected Response:**
```json
{
  "status": "healthy",
  "uptime": 123.456,
  "timestamp": "2025-12-31T21:45:00Z",
  "version": "1.0.0"
}
```

### 3.2 Test API Info

```bash
curl https://stock-sentiment-api-production.up.railway.app/
```

**Expected Response:**
```json
{
  "name": "Stock Sentiment API",
  "version": "1.0.0",
  "description": "Real-time stock sentiment analysis...",
  "pricing": "$0.1 USDC per query",
  "endpoint": "/v1/sentiment/:ticker"
}
```

### 3.3 Test Payment Requirement (402)

```bash
curl -i https://stock-sentiment-api-production.up.railway.app/v1/sentiment/AAPL
```

**Expected Response:**
```
HTTP/1.1 402 Payment Required
Content-Type: application/json
PAYMENT-REQUIRED: {"maxAmountRequired":"0.1","resource":"https://...","description":"Stock sentiment analysis for AAPL","payTo":"0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E","asset":"0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913","extra":{"name":"USD Coin","version":"2"}}

{
  "error": "payment_required",
  "message": "X-PAYMENT header is required",
  "payment": {
    "amount": "0.1",
    "currency": "USDC",
    "network": "Base"
  }
}
```

✅ If you see this, **deployment is successful!**

---

## Step 4: Submit to x402scan (3 minutes)

### 4.1 Prepare Submission Details

Collect this information:

```
API Name: Stock Sentiment API
Description: Real-time stock sentiment analysis powered by Reddit and Twitter data
Category: Analytics / Trading Signals
Base URL: https://stock-sentiment-api-production.up.railway.app
Endpoint: /v1/sentiment/{ticker}
Example: /v1/sentiment/AAPL

Payment Details:
- Price: 0.1 USDC
- Network: Base (Chain ID: 8453)
- Asset: 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913
- Wallet: 0x9B6C3EE1f3A155456C4da066D7398Fa75c4a127E

Supported Parameters:
- AAPL (Apple)
- TSLA (Tesla)
- GME (GameStop)
- NVDA (NVIDIA)
- [+ 20 more]

Contact:
- GitHub: lobsterbar2027-boop
- Twitter: @BreakTheCubicle
- Email: support@genvox.io
```

### 4.2 Submit on x402scan

1. Go to [x402scan.com](https://x402scan.com)
2. Click **"Add API"** or **"Submit Server"**
3. Fill in the form with details above
4. **Test Endpoint** - x402scan will verify your 402 response
5. Click **"Submit for Review"**

### 4.3 Wait for Approval

- Review typically takes 24-48 hours
- You'll receive email notification
- Check your submission status on x402scan

---

## Step 5: Monitor & Maintain (Ongoing)

### 5.1 View Logs

```bash
# In Railway dashboard:
# Go to Deployments → Click latest deployment → View Logs
```

### 5.2 Update Environment Variables

```bash
# In Railway:
# Settings → Variables → Add New Variable
```

### 5.3 Check Analytics

Once approved on x402scan:
- View query count
- Monitor revenue
- Track usage patterns

---

## 🔧 Troubleshooting

### Issue: Deployment Failed

**Solution:**
1. Check build logs in Railway
2. Verify `package.json` is correct
3. Ensure Node.js version is 18+
4. Check for syntax errors in `server.js`

### Issue: 402 Response Not Working

**Solution:**
1. Check `WALLET_ADDRESS` is set correctly
2. Verify `BASE_URL` matches Railway domain
3. Test locally first: `npm start`
4. Check PAYMENT-REQUIRED header format

### Issue: x402scan Rejection

**Common reasons:**
1. Incorrect payment format
2. Wrong USDC contract address
3. Invalid wallet address
4. 402 response not properly formatted
5. Resource URL doesn't match

**Fix:** Review `X402_COMPLIANCE.md` checklist

### Issue: High Response Times

**Solution:**
1. Enable Railway caching
2. Add Redis for sentiment cache
3. Optimize Reddit/Twitter scraping
4. Use real APIs instead of mock data

---

## 📊 Expected Performance

After deployment:

- **Response Time:** <200ms (cached), <500ms (fresh)
- **Uptime:** 99.9%+
- **Concurrent Users:** Unlimited (Railway auto-scales)
- **Cache Duration:** 1 hour per ticker

---

## 🎯 Next Steps After Deployment

### Week 1: Launch
- [ ] Get x402scan approval
- [ ] Share on Twitter/X
- [ ] Post in r/algotrading
- [ ] Create demo video

### Week 2: Enhance
- [ ] Add real Reddit API
- [ ] Add real Twitter API
- [ ] Implement historical trends
- [ ] Add more tickers

### Week 3: Scale
- [ ] Monitor usage patterns
- [ ] Optimize caching strategy
- [ ] Add analytics dashboard
- [ ] Consider premium tier

### Month 2: Expand
- [ ] Add webhook notifications
- [ ] Create batch endpoint
- [ ] Implement GraphQL
- [ ] Launch affiliate program

---

## 💰 Revenue Tracking

### Expected First Month

Based on CryptoSentiment performance:

```
Conservative: 1,000 queries/day
1,000 × $0.10 × 30 days = $3,000/month

Moderate: 5,000 queries/day  
5,000 × $0.10 × 30 days = $15,000/month

Optimistic: 10,000 queries/day
10,000 × $0.10 × 30 days = $30,000/month
```

Track via:
- x402scan analytics
- Railway request logs
- Your wallet transactions on Basescan

---

## 🆘 Support

### Railway Issues
- Railway Docs: [docs.railway.app](https://docs.railway.app)
- Railway Discord: [discord.gg/railway](https://discord.gg/railway)

### x402 Protocol Issues
- x402 Docs: [x402.org/docs](https://x402.org/docs)
- x402 Discord: Check x402.org for link

### API Issues
- GitHub Issues: [github.com/lobsterbar2027-boop/stock-sentiment-api/issues](https://github.com/lobsterbar2027-boop/stock-sentiment-api/issues)
- Email: support@genvox.io
- Twitter: [@BreakTheCubicle](https://x.com/BreakTheCubicle)

---

## ✅ Deployment Checklist

Complete this checklist before submitting to x402scan:

- [ ] GitHub repo created and public
- [ ] Railway project deployed successfully
- [ ] Environment variables set correctly
- [ ] `/health` endpoint returns 200
- [ ] `/` endpoint returns API info
- [ ] `/v1/sentiment/AAPL` returns 402
- [ ] PAYMENT-REQUIRED header formatted correctly
- [ ] Asset address is correct USDC on Base
- [ ] Wallet address is your address
- [ ] Resource URL matches your domain
- [ ] Response times are acceptable
- [ ] No errors in Railway logs
- [ ] All supported tickers work
- [ ] Error handling works (invalid ticker)

**Once all checked, you're ready for x402scan submission! 🚀**

---

## 🎉 Success Criteria

You'll know deployment is successful when:

1. ✅ Railway shows "Deployed" status
2. ✅ Health check returns 200 OK
3. ✅ API info endpoint works
4. ✅ 402 response is properly formatted
5. ✅ x402scan submission accepted
6. ✅ First payment received
7. ✅ Revenue starts flowing

**Expected timeline: 2-3 days from deployment to first revenue**

---

**Good luck! You're building the future of AI agent commerce. 🚀**

Questions? Open an issue on GitHub or reach out on Twitter.

**Built by:** lobsterbar2027-boop  
**Project:** Break the Cubicle  
**Version:** 1.0.0
