# sBTC YieldAgent - Stacks x402 API

Real-time sBTC yield opportunities from top Stacks DeFi protocols via x402 payment protocol.

## 🚀 Live Service

**Endpoint:** `https://yieldagent402.pages.dev/`

## 📊 What It Does

sBTC YieldAgent aggregates real-time yield data for sBTC across Stacks DeFi protocols:

- **Velar** - 6.8% APY
- **ALEX** - 5.2% APY  
- **Arkadiko** - 7.1% APY
- **Zest Protocol** - 8.5% APY
- **Hermetica** - 6.3% APY

Get all sBTC yield opportunities in one API call. No subscriptions. No API keys. Just pay-per-use with STX.

## 💰 Pricing

- **Cost:** 0.5 STX per request
- **Network:** Stacks Mainnet
- **Payment Asset:** STX
- **Payment Address:** `SP2F0VC55JT6ND29YHF9VZE1Q5DM137VXQY93GPW5`

## 🔧 How to Use

### 1. Discovery (Check Price)
```bash
curl https://yieldagent402.pages.dev/x402-info
```

Returns payment requirements:
```json
{
  "x402Version": 1,
  "accepts": [{
    "scheme": "exact",
    "network": "stacks",
    "maxAmountRequired": "0.5",
    "payTo": "SP2F0VC55JT6ND29YHF9VZE1Q5DM137VXQY93GPW5",
    "asset": "STX"
  }]
}
```

### 2. Make Payment

Send 0.5 STX to `SP2F0VC55JT6ND29YHF9VZE1Q5DM137VXQY93GPW5` on Stacks network.

### 3. Access Data
```bash
curl https://yieldagent402.pages.dev/ \
  -H "X-Payment: {\"txHash\": \"0xYOUR_TX_HASH\", \"amount\": 0.5}"
```

### 4. Get Response
```json
{
  "success": true,
  "data": {
    "opportunities": [
      {
        "id": 1,
        "protocol": "Velar",
        "apy": "6.8%",
        "risk": "Low",
        "tvl": "$25M",
        "asset": "sBTC"
      },
      ...
    ],
    "network": "Stacks",
    "lastUpdated": "2026-02-02T19:30:00.000Z"
  }
}
```

## 🌐 Web Interface

Visit the service directly in your browser:

👉 **https://yieldagent402.pages.dev/**

Features:
- Interactive payment interface
- One-click address copy
- Real-time sBTC yield data
- Mobile-friendly design

## 🛠️ For Developers

### Integration Example (JavaScript)
```javascript
async function getSBTCYieldData(txHash) {
  const response = await fetch('https://yieldagent402.pages.dev/', {
    method: 'GET',
    headers: {
      'X-Payment': JSON.stringify({
        txHash: txHash,
        amount: 0.5
      })
    }
  });
  
  if (response.ok) {
    const data = await response.json();
    return data.data.opportunities;
  } else {
    throw new Error('Payment verification failed');
  }
}
```

### Integration Example (Python)
```python
import requests
import json

def get_sbtc_yield_data(tx_hash):
    headers = {
        'X-Payment': json.dumps({
            'txHash': tx_hash,
            'amount': 0.5
        })
    }
    
    response = requests.get(
        'https://yieldagent402.pages.dev/',
        headers=headers
    )
    
    if response.ok:
        return response.json()['data']['opportunities']
    else:
        raise Exception('Payment verification failed')
```

## 📋 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Main API (requires payment) |
| `/x402-info` | GET | Discovery endpoint (free) |
| `/.well-known/x402` | GET | x402 protocol discovery |
| `/health` | GET | Health check |

## ⚡ Response Format
```typescript
interface YieldOpportunity {
  id: number;
  protocol: string;
  apy: string;
  risk: "Low" | "Medium" | "High";
  tvl: string;
  asset: string;
}

interface ApiResponse {
  success: boolean;
  data: {
    opportunities: YieldOpportunity[];
    network: string;
    lastUpdated: string;
  }
}
```

## 🪙 About sBTC

sBTC is a decentralized, 1:1 Bitcoin-backed asset on Stacks. It enables Bitcoin holders to earn yield in DeFi while maintaining Bitcoin exposure.

Learn more: [sBTC Documentation](https://docs.stacks.co/sbtc)

## 🔒 Security

- Payment verification on Stacks blockchain
- CORS enabled for web applications
- No personal data collection
- Open-source clarity contract verification

## 📝 Protocol

This service implements the **x402 protocol** - a standard for micropayment-gated HTTP APIs.

Learn more: [x402 Protocol Specification](https://github.com/x402-protocol/spec)

## 🤝 Support

- **Issues:** Open an issue on GitHub
- **Email:** support@base402.dev
- **Discord:** [Join Stacks Discord](https://discord.gg/stacks)

## 📜 License

MIT License - See LICENSE file for details

---

**Built for Stacks • Powered by x402 Protocol • sBTC Native**
