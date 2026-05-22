# Pricing

## Free tier

No API key required. No signup.

| | |
|---|---|
| **Trails per month** | 1,000 |
| **Verification** | Unlimited — public endpoint, no auth |
| **action_ref derivation** | Unlimited — local, no network call |
| **Cost** | Free |

Start immediately:

```bash
curl -X POST https://argentum-api.rgiskard.xyz/nexus/trail \
  -H "Content-Type: application/json" \
  -d '{
    "action_ref": "<your-action-ref>",
    "service": "my-agent",
    "hash_algo": "sha256",
    "preimage_format": "jcs-rfc8785",
    "preimage": {
      "agent_id": "my-agent-001",
      "action_type": "file:write",
      "scope": "audit",
      "ts": "2026-05-19T12:00:00.000Z"
    }
  }'
```

When you reach 1,000 trails in a calendar month, the API returns:

```json
{
  "error": "monthly_limit_exceeded",
  "limit": 1000,
  "used": 1000,
  "tier": "free",
  "upgrade": "https://argentum-api.rgiskard.xyz/docs#payg"
}
```

## Pay-as-you-go (PAYG)

**$0.003 per trail.** No monthly commitment.

| | |
|---|---|
| **Price** | $0.003 / trail |
| **Minimum purchase** | 1 trail |
| **Maximum purchase** | 10,000 trails per invoice |
| **Payment** | Lightning (sats) · USDC on Arbitrum |
| **Credits** | Added within 24h of on-chain confirmation |

**Get started in two steps:**

```bash
# 1. Create your PAYG account
curl -X POST "https://argentum-api.rgiskard.xyz/payg/account?agent_id=my-agent-001"

# 2. Get a USDC deposit address for N trails
curl -X POST https://argentum-api.rgiskard.xyz/payg/topup/usdc \
  -H "Content-Type: application/json" \
  -d '{"api_key": "<your-api-key>", "trails": 500}'
```

## Enterprise

Volume pricing and SLA guarantees. [Open an issue](https://github.com/giskard09/argentum-core/issues) to discuss.

---

*Verification (`/trails/verify`) is always free and unauthenticated — for anyone,
including auditors who never submitted a trail.*
