# COMPLY Token Deployment Guide

## Prerequisites

Before you begin, ensure you have:

- **Node.js** 16 or higher
- **Solana CLI** installed
- **Rust** 1.65+ (for smart contract compilation)
- An **SPL token wallet** with SOL for fees

### Quick Setup

```bash
# Install Solana CLI
curl https://release.solana.com/v1.18.0/install

# Verify installation
solana --version
```

## Step 1: Setup Your Environment

### 1.1 Clone the Repository

```bash
git clone https://github.com/AngelTruth/comply-token.git
cd comply-token
npm install
```

### 1.2 Configure Your Wallet

```bash
# Copy environment template
cp .env.example .env

# Edit .env with your wallet configuration
# You'll need:
# - PRIVATE_KEY: Your wallet's private key
# - NETWORK: testnet or mainnet-beta
```

### 1.3 Fund Your Wallet

**For Testnet (Free):**
```bash
# Switch to testnet
solana config set --url testnet

# Request free SOL (faucet)
solana airdrop 2 <your-wallet-address>
```

**For Mainnet:**
You'll need real SOL (~$0.50 worth for deployment)

## Step 2: Deploy to Testnet (Recommended First)

```bash
# Set network to testnet
solana config set --url testnet

# Check balance
solana balance

# Deploy (free on testnet)
npm run deploy:testnet
```

## Step 3: Create Token Mint

```bash
# Run token creation script
ts-node scripts/create-token.ts

# Script will:
# 1. Create token mint on Solana
# 2. Initialize supply (1 billion COMPLY)
# 3. Setup buyback treasury
# 4. Output token address
```

## Step 4: Verify Deployment

```bash
# Check token on testnet explorer
# https://explorer.solana.com/address/YOUR_TOKEN_ADDRESS?cluster=testnet

# Verify all components
ts-node scripts/verify-deployment.ts
```

## Step 5: Deploy to Mainnet

⚠️ **WARNING: This costs real SOL (~$1-2)**

```bash
# Update configuration
solana config set --url mainnet-beta

# Verify wallet has sufficient SOL
solana balance

# Deploy to mainnet
npm run deploy:mainnet
```

## Cost Breakdown

### Testnet (Free)
- Program deployment: Free (test SOL from faucet)
- Token creation: Free

### Mainnet
- Program deployment: ~0.5 SOL
- Token creation: ~0.01 SOL
- Liquidity pool: ~1 SOL
- **Total: ~$50-100**

## Troubleshooting

### Build Fails
```bash
# Update Rust
rustup update

# Clear cache and rebuild
anchor clean
anchor build
```

### Insufficient Funds
```bash
# Get more SOL from faucet (testnet only)
solana airdrop 2

# Or transfer from exchange
```

### Transaction Timeout
```bash
# Increase timeout
export SOLANA_RPC_TIMEOUT_DEFAULT=30

# Retry
npm run deploy:mainnet
```

## Next Steps

1. ✅ Deploy and test
2. ✅ Create liquidity
3. ✅ Announce on X
4. ✅ Build community
5. ✅ Execute first buyback

---

**Questions?** Open an issue: https://github.com/AngelTruth/comply-token/issues