
# MEV-Flashbot-Sandwich-RS

## Project Introduction  
mev-bot is a **high-performance Ethereum MEV (sandwich attack) bot** written in Rust.  
The project listens to pending transactions in the Ethereum mempool, captures high-slippage trading opportunities, constructs front-running and back-running transactions (sandwich attacks), and privately submits transaction bundles via the Flashbots relay, achieving on-chain arbitrage or frontrunning profits.

The bot is designed for **low latency, high reliability, easy extensibility, and controlled risk**, suitable for MEV strategy research, performance optimization, or live mainnet deployment.

## Technology Stack  
- **Rust**: Safe, high-performance, no GC pauses, ideal for building trading bots  
- **Tokio**: Rust's asynchronous runtime, used for high-concurrency event listening and processing  
- **ethers-rs**: Ethereum interaction library supporting RPC/WebSocket, multisignature wallets, and contract calls  
- **WebSocket**: Used for real-time pending transaction monitoring to improve response speed  
- **Flashbots RPC**: Submits private transaction bundles via Flashbots, avoiding frontrunning  
- **Environment Configuration**: Uses AES-GCM to encrypt private keys, securely loading RPC and key parameters from `.env` files or config  

## Project Structure  
```plaintext
mev-bot/
├── Cargo.toml
└── src/
    ├── main.rs       // Entry point
    ├── mev.rs        // Core logic (e.g., sandwich, arbitrage)
    ├── mempool.rs    // Pending transaction listener
    └── tx_sender.rs  // Transaction sender (including Flashbots)
```

## Key Features
✅ High-concurrency listening: Real-time capture of target transactions in the mempool, never missing arbitrage opportunities

✅ Modular design: Decoupled MEV strategy, mempool listener, and transaction sender modules for easy maintenance and extension

✅ Private transaction submission: Submits transactions via Flashbots, invisible to regular nodes, reducing sandwich attack risk

✅ Fully local operation: No reliance on centralized services; private keys encrypted with AES-GCM and decrypted locally, ensuring secure key management and efficient signing for optimal security and performance

✅ Extensible strategies: Supports adding liquidation, arbitrage, JIT, and other MEV strategy types
