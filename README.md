# LayerEdge Light Node Setup Guide


![LayerEdge](image.png)



[![Telegram](https://img.shields.io/badge/Twitter-Join%20Chat-blue)](https://t.me/airdrop3arn)
[![Twitter Follow](https://img.shields.io/twitter/follow/LayerEdge?style=social)](https://twitter.com/flexxrichie)

*A comprehensive guide for setting up and running a LayerEdge Light Node*

[Features](#features) • [Prerequisites](#prerequisites) • [Installation](#installation) • [Configuration](#configuration) • [Troubleshooting](#troubleshooting)

</div>

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [System Requirements](#system-requirements)
- [Installation](#installation)
  - [Installing Dependencies](#installing-dependencies)
  - [RISC0 Installation](#risc0-installation)
  - [LayerEdge Setup](#layeredge-setup)
- [Configuration](#configuration)
- [Running the Node](#running-the-node)
- [Monitoring](#monitoring)
- [Troubleshooting](#troubleshooting)
- [Security Recommendations](#security-recommendations)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)

## Features

- Full Light Node implementation for LayerEdge network
- Merkle tree verification and proof generation
- Dashboard integration for monitoring
- Secure and efficient proof aggregation
- Points tracking system

## Prerequisites

Before you begin, ensure you have the following installed:

- **Operating System**: Ubuntu 20.04+, macOS 12+, or Windows with WSL2
- **Go**: Version 1.18 or higher
- **Rust**: Latest stable version
- **Git**: Latest version
- **CMake**: Version 3.12 or higher
- **Build Essential Tools**

## System Requirements

- **CPU**: 4+ cores recommended
- **RAM**: Minimum 8GB, 16GB recommended
- **Storage**: 50GB+ free space
- **Network**: Stable internet connection

## Installation

### Installing Dependencies

#### Ubuntu/Debian

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install -y build-essential cmake pkg-config libssl-dev clang git curl

# Install Go
wget https://go.dev/dl/go1.21.6.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.21.6.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc

# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

#### macOS

```bash
# Install Homebrew if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install dependencies
brew install go cmake pkg-config openssl git

# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

### RISC0 Installation

```bash
# Add Rust components
rustup component add rustfmt
rustup component add clippy
rustup target add wasm32-unknown-unknown

# Clone RISC0 repository
git clone https://github.com/risc0/risc0.git
cd risc0

# Checkout stable version
git checkout v0.19.1

# Build RISC0
cargo build --release

# Add to PATH
echo 'export PATH=$PATH:'"$HOME/risc0/target/release" >> ~/.bashrc
source ~/.bashrc
```

### LayerEdge Setup

```bash
# Clone LayerEdge repository
git clone https://github.com/Layer-Edge/light-node.git
cd light-node

# Create environment file
cat > .env << EOL
GRPC_URL=34.31.74.109:9090
CONTRACT_ADDR=cosmos1ufs3tlq4umljk0qfe8k5ya0x6hpavn897u2cnf9k0en9jr7qarqqt56709
ZK_PROVER_URL=http://127.0.0.1:3001
API_REQUEST_TIMEOUT=100
POINTS_API=https://light-node.layeredge.io
PRIVATE_KEY='your-private-key'
EOL
```

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| GRPC_URL | LayerEdge gRPC endpoint | 34.31.74.109:9090 |
| CONTRACT_ADDR | Smart contract address | cosmos1ufs... |
| ZK_PROVER_URL | RISC0 prover service URL | http://127.0.0.1:3001 |
| API_REQUEST_TIMEOUT | API timeout in seconds | 100 |
| POINTS_API | Points tracking API endpoint | https://light-node.layeredge.io |
| PRIVATE_KEY | Your wallet private key | - |

## Running the Node

1. **Start the Merkle Service**
```bash
cd risc0-merkle-service
cargo build && cargo run
```

2. **Run the Light Node**
```bash
# In a new terminal
cd light-node
go build ./light-node
./light-node
```

## Monitoring

### Dashboard Integration

1. Visit [dashboard.layeredge.io](https://dashboard.layeredge.io)
2. Connect your wallet
3. Link your CLI node's Public Key

### Logging

The node provides comprehensive logs for:
- Merkle tree operations
- ZK proof generation
- Verification status
- Performance metrics

## Troubleshooting

### Common Issues and Solutions

#### RISC0 Installation Issues

```bash
# If compilation fails
rustup update
cargo clean
cargo build --release

# Missing dependencies
sudo apt install -y libclang-dev  # Ubuntu
brew install llvm  # macOS

# Memory issues
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

#### Node Connection Issues

1. **gRPC Connection Failed**
   - Verify GRPC_URL in .env
   - Check network connectivity
   - Ensure ports are open

2. **Merkle Service Issues**
   - Verify RISC0 installation
   - Check system resources
   - Review service logs

3. **Wallet Connection Issues**
   - Verify PRIVATE_KEY in .env
   - Check wallet balance
   - Ensure correct network configuration

## Security Recommendations

1. **Private Key Management**
   - Store private keys securely
   - Use environment variables
   - Never commit sensitive data

2. **System Security**
   - Keep system updated
   - Use firewall protection
   - Regular security audits

3. **Backup Procedures**
   - Regular configuration backups
   - Secure key storage
   - Document recovery procedures



## 🌐 Connect With Me

[![Twitter](https://img.shields.io/badge/Twitter-%231DA1F2.svg?style=for-the-badge&logo=Twitter&logoColor=white)](https://twitter.com/FlexxRichie)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/FlexxRichie)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Fl3xxRichie)
[![Private Channel](https://img.shields.io/badge/Private_Channel-%23FF5733.svg?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/+GIfY4Pb0Spw5OGZk)
[![Direct Contact](https://img.shields.io/badge/Direct_Contact-%23009688.svg?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/flexxrichie)

