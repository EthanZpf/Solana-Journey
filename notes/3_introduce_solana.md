要在 Solana 上进行开发，了解 Solana 开发中独特的几个关键概念至关重要。本节涵盖了您在开始 Solana 开发时需要理解的核心概念，包括账户、交易、程序等内容。

账户
Solana 网络上的所有数据都存储在账户中。您可以将 Solana 网络视为一个包含单一账户表的公共数据库。账户与其地址之间的关系类似于键值对，其中键是地址，值是账户。

每个账户都有相同的基本结构，并且可以通过其地址找到。

## Accounts

**Concept:** The diagram illustrates a Key-Value store where an **Address** (Key) maps to a specific **Account** (Value).

### Structure

| Key | Value |
| :--- | :--- |
| Address | Account |
| **Address** | **Account** (Individual Account) |
| Address | Account |

### Code Definition (Rust)

The "Account" value consists of the following structure:

```rust
pub struct Account {
    pub lamports: u64,
    pub data: Vec<u8>,
    pub owner: Pubkey,
    pub executable: bool,
    pub rent_epoch: Epoch,
}