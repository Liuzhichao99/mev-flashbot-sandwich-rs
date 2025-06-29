# MEV-Flashbot-Sandwich-RS
## 项目介绍
mev-bot 是一个基于 Rust 编写的 **高性能以太坊 MEV（三明治攻击）机器人**。
该项目通过监听以太坊 mempool 中的 pending 交易，捕捉高滑点交易机会，构建前后插队交易（sandwich attack），并通过 Flashbots 中继器私下提交交易 bundle，从而实现链上套利或抢跑收益。

该机器人设计目标是**低延迟、高可靠性、易扩展、可控风险**，适用于研究 MEV 策略、性能优化或主网上实盘测试。

## 技术栈
- **Rust**：安全、高性能、无 GC 停顿，适合编写交易型机器人

- **Tokio**：Rust 的异步运行时，用于高并发事件监听与处理

- **ethers-rs**：以太坊交互库，支持 RPC/WebSocket、多签名、合约调用等

- **WebSocket**：用于实时监听 pending tx，提升响应速度

- **Flashbots** RPC：通过 Flashbots 提交私密交易 bundle，避免抢跑

- **环境配置**：使用 AES-GCM 对私钥加密存储，结合 .env 文件或配置文件安全加载 RPC 和私钥参数

## 项目结构
```plaintext
mev-bot/
├── Cargo.toml
└── src/
    ├── main.rs       // 启动器：初始化 WebSocket + 运行核心策略
    ├── mev.rs        // 核心策略逻辑（如三明治、套利等逻辑）
    ├── mempool.rs    // Mempool 监听模块。监听pending tx 
    └── tx_sender.rs  // 交易模块，用于打包并发送 Flashbots Bundle
```

## 特性亮点
✅ 高并发监听：实时捕捉 mempool 中的目标交易，不错过套利机会

✅ 模块化设计：mev 策略、mempool、交易发送等模块解耦，易于维护和扩展

✅ 私密交易提交：通过 Flashbots 提交，不被普通节点看到，降低被夹风险

✅ 完全本地运行：无中心化依赖，私钥采用 AES-GCM 加密存储并本地解密，既保障私钥安全可控，又兼顾解密后高效签名，确保性能与安全双重优化，最大限度保障资产安全

✅ 可拓展策略：可添加清算、套利、JIT 等其他类型的 MEV 策略
