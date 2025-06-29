# mev-flashbot-sandwich-rs

mev-bot/
├── Cargo.toml
└── src/
    ├── main.rs       // 启动器
    ├── mev.rs        // 核心逻辑（如三明治、套利）
    ├── mempool.rs    // pending tx 监听
    └── tx_sender.rs  // 发送交易（包含 Flashbots）
