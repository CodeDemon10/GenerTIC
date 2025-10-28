# 🔷 RetroC - Solidity Contract Generator

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![VS Code](https://img.shields.io/badge/VS%20Code-1.60+-purple.svg)
![Solidity](https://img.shields.io/badge/Solidity-0.8+-orange.svg)

**RetroC - Lightning-fast Solidity smart contract templates at your fingertips**

[Installation](#installation) • [Features](#features) • [Usage](#usage) • [Templates](#templates) • [Contributing](#contributing)

---

</div>

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Available Templates](#available-templates)
- [Command Palette](#command-palette)
- [Configuration](#configuration)
- [Testing](#testing)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

**RetroC** is a VS Code extension designed to supercharge your smart contract development workflow. Generate production-ready contract templates with a single command, complete with best practices, security patterns, and optional test scaffolds.

### Why Use This Extension?

- ⚡ **Speed**: Generate complete contracts in seconds
- 🛡️ **Security**: Built-in best practices and security patterns
- 🎨 **Customization**: Easy placeholder replacement for your needs
- 🧪 **Testing**: Optional test file generation with Hardhat/Foundry support
- 📚 **Standards Compliant**: ERC20, ERC721, ERC1155, and more

---

## ✨ Key Features

### 🎨 Template Generation

Generate industry-standard smart contract templates instantly:

- **ERC20 Tokens** - Fungible token implementation
- **ERC721 NFTs** - Non-fungible token contracts
- **ERC1155** - Multi-token standard
- **DAO Contracts** - Governance and voting systems
- **Multisig Wallets** - Multi-signature wallet contracts
- **Staking Contracts** - Token staking mechanisms
- **Vesting Contracts** - Token vesting schedules

### ⚙️ Smart Placeholders

All templates include intelligent placeholders:

```solidity
contract {{CONTRACT_NAME}} is ERC20 {
    string public constant NAME = "{{TOKEN_NAME}}";
    string public constant SYMBOL = "{{TOKEN_SYMBOL}}";
    uint8 public constant DECIMALS = {{TOKEN_DECIMALS}};
}
```

### 🧪 Test Scaffolding

Automatically generate test files for:
- **Hardhat** (JavaScript/TypeScript)
- **Foundry** (Solidity)
- Pre-configured test cases for common scenarios

### 🎯 Command Palette Integration

Quick access through VS Code's command palette:
- `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac)
- Type: `> Generate [Template Type]`

---

## 🛠️ Tech Stack

<div align="center">

### Core Technologies

| Technology | Purpose | Version |
|:----------:|:-------:|:-------:|
| ![VS Code](https://img.shields.io/badge/VS_Code_API-Extension_Framework-007ACC?style=for-the-badge&logo=visual-studio-code) | Extension Framework | Latest |
| ![TypeScript](https://img.shields.io/badge/TypeScript-Language-3178C6?style=for-the-badge&logo=typescript&logoColor=white) | Development Language | 4.9+ |
| ![Solidity](https://img.shields.io/badge/Solidity-Smart_Contracts-363636?style=for-the-badge&logo=solidity) | Template Language | 0.8+ |
| ![Node.js](https://img.shields.io/badge/Node.js-Runtime-339933?style=for-the-badge&logo=node.js&logoColor=white) | Runtime Environment | 16+ |

### Development Tools

| Tool | Purpose |
|:----:|:-------:|
| **Webpack** | Bundle and optimize extension |
| **ESLint** | Code quality and linting |
| **Prettier** | Code formatting |
| **Jest** | Unit testing framework |
| **VS Code Test Runner** | Extension testing |

</div>

---

## 📦 Installation

### From VS Code Marketplace (Coming Soon)

1. Open VS Code
2. Press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (Mac)
3. Search for "RetroC"
4. Click **Install**

### From VSIX File

```bash
# Download the latest .vsix file from releases
code --install-extension retroc-1.0.0.vsix
```

### From Source

```bash
# Clone the repository
git clone https://github.com/yourusername/retroc.git

# Navigate to directory
cd retroc

# Install dependencies
npm install

# Build the extension
npm run compile

# Package the extension
npm run package
```

---

## 🚀 Quick Start

### 1. Open Your Solidity Project

Open your smart contract project in VS Code:

```bash
cd your-solidity-project
code .
```

### 2. Generate Your First Template

**Using Command Palette:**

1. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac)
2. Type: `> Generate ERC20 Template`
3. Enter token details when prompted:
   - Token Name: `MyToken`
   - Token Symbol: `MTK`
   - Initial Supply: `1000000`
   - Decimals: `18`

**Result:** A complete ERC20 contract will be created at `contracts/MyToken.sol`

### 3. Generate Test Files

1. With your contract open, run: `> Generate Test File`
2. Choose your testing framework:
   - Hardhat (JavaScript)
   - Hardhat (TypeScript)
   - Foundry (Solidity)

**Result:** Test file created at `test/MyToken.test.js` (or `.ts`/`.sol`)

---

## 📚 Available Templates

### ERC20 Token

<details>
<summary><strong>Click to expand ERC20 details</strong></summary>

**Features:**
- ✅ Mintable
- ✅ Burnable
- ✅ Pausable
- ✅ Access Control (Ownable/AccessControl)
- ✅ Permit (EIP-2612)

**Generated Structure:**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract {{TOKEN_NAME}} is ERC20, Ownable {
    constructor() ERC20("{{TOKEN_NAME}}", "{{TOKEN_SYMBOL}}") {
        _mint(msg.sender, {{INITIAL_SUPPLY}} * 10 ** decimals());
    }
}
```

**Command:** `> Generate ERC20 Template`

</details>

### ERC721 NFT

<details>
<summary><strong>Click to expand ERC721 details</strong></summary>

**Features:**
- ✅ Enumerable
- ✅ URI Storage
- ✅ Burnable
- ✅ Royalty Support (EIP-2981)
- ✅ Batch Minting

**Generated Structure:**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";

contract {{NFT_NAME}} is ERC721, ERC721URIStorage {
    uint256 private _tokenIdCounter;
    
    constructor() ERC721("{{NFT_NAME}}", "{{NFT_SYMBOL}}") {}
}
```

**Command:** `> Generate ERC721 Template`

</details>

### ERC1155 Multi-Token

<details>
<summary><strong>Click to expand ERC1155 details</strong></summary>

**Features:**
- ✅ Multiple token types
- ✅ Batch operations
- ✅ URI management
- ✅ Supply tracking

**Command:** `> Generate ERC1155 Template`

</details>

### DAO Contract

<details>
<summary><strong>Click to expand DAO details</strong></summary>

**Features:**
- ✅ Proposal creation
- ✅ Voting mechanism
- ✅ Timelock execution
- ✅ Quorum requirements
- ✅ Token-based governance

**Command:** `> Generate DAO Template`

</details>

### Multisig Wallet

<details>
<summary><strong>Click to expand Multisig details</strong></summary>

**Features:**
- ✅ Multiple signers
- ✅ Transaction proposals
- ✅ Approval threshold
- ✅ Emergency functions

**Command:** `> Generate Multisig Template`

</details>

### Staking Contract

<details>
<summary><strong>Click to expand Staking details</strong></summary>

**Features:**
- ✅ Token staking
- ✅ Reward distribution
- ✅ Lock periods
- ✅ Emergency withdrawal

**Command:** `> Generate Staking Template`

</details>

---

## 🎮 Command Palette

All commands are accessible via the VS Code Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`):

| Command | Description |
|---------|-------------|
| `> Generate ERC20 Template` | Create ERC20 token contract |
| `> Generate ERC721 Template` | Create ERC721 NFT contract |
| `> Generate ERC1155 Template` | Create ERC1155 multi-token |
| `> Generate DAO Template` | Create DAO governance contract |
| `> Generate Multisig Template` | Create multisig wallet |
| `> Generate Staking Template` | Create staking contract |
| `> Generate Vesting Template` | Create vesting contract |
| `> Generate Test File` | Generate test scaffold |
| `> Generate All Tests` | Generate tests for all contracts |

---

## ⚙️ Configuration

Configure the extension in your VS Code settings (`settings.json`):

```json
{
  "retroc.defaultSolidityVersion": "0.8.20",
  "retroc.defaultLicense": "MIT",
  "retroc.openZeppelinVersion": "5.0.0",
  "retroc.autoGenerateTests": true,
  "retroc.testFramework": "hardhat",
  "retroc.contractsDirectory": "contracts",
  "retroc.testsDirectory": "test",
  "retroc.useTypeScript": true
}
```

### Configuration Options

| Setting | Default | Description |
|---------|---------|-------------|
| `defaultSolidityVersion` | `"0.8.20"` | Default Solidity compiler version |
| `defaultLicense` | `"MIT"` | Default SPDX license identifier |
| `openZeppelinVersion` | `"5.0.0"` | OpenZeppelin contracts version |
| `autoGenerateTests` | `true` | Auto-generate test files |
| `testFramework` | `"hardhat"` | Preferred testing framework |
| `contractsDirectory` | `"contracts"` | Output directory for contracts |
| `testsDirectory` | `"test"` | Output directory for tests |
| `useTypeScript` | `true` | Use TypeScript for tests |

---

## 🧪 Testing

### Running Extension Tests

```bash
# Run all tests
npm test

# Run specific test suite
npm test -- --testPathPattern=erc20

# Run with coverage
npm run test:coverage
```

### Manual Testing

1. Press `F5` in VS Code to launch Extension Development Host
2. Open a sample Solidity project
3. Test commands from Command Palette
4. Verify generated files

---

## 💻 Development

### Project Structure

```
retroc/
├── src/
│   ├── extension.ts          # Extension entry point
│   ├── commands/              # Command implementations
│   │   ├── generateERC20.ts
│   │   ├── generateERC721.ts
│   │   └── generateTests.ts
│   ├── templates/             # Contract templates
│   │   ├── erc20.template.sol
│   │   ├── erc721.template.sol
│   │   └── dao.template.sol
│   ├── utils/                 # Utility functions
│   │   ├── fileWriter.ts
│   │   └── placeholderReplacer.ts
│   └── test/                  # Test files
├── package.json
├── tsconfig.json
└── README.md
```

### Building from Source

```bash
# Install dependencies
npm install

# Compile TypeScript
npm run compile

# Watch mode for development
npm run watch

# Package extension
npm run package
```

### Adding New Templates

1. Create template file in `src/templates/`
2. Add command in `src/commands/`
3. Register command in `src/extension.ts`
4. Update `package.json` contributions
5. Add tests in `src/test/`

---

## 🤝 Contributing

We welcome contributions! Here's how to get started:

### Contribution Guidelines

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Development Setup

```bash
# Clone your fork
git clone https://github.com/yourusername/retroc.git

# Add upstream remote
git remote add upstream https://github.com/originalauthor/retroc.git

# Create branch
git checkout -b feature/new-template

# Make changes and test
npm run compile && npm test

# Submit PR
```

### Code Style

- Use TypeScript
- Follow ESLint rules
- Add tests for new features
- Update documentation

---

## 📝 Roadmap

- [ ] Additional template support (DeFi protocols)
- [ ] Interactive template customization UI
- [ ] Integration with Hardhat/Foundry configs
- [ ] Gas optimization suggestions
- [ ] Security pattern checks
- [ ] Template marketplace
- [ ] Multi-file project scaffolding
- [ ] Smart contract upgradeability patterns

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- OpenZeppelin for secure contract libraries
- VS Code team for excellent extension API
- Solidity community for best practices
- All contributors and users

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/retroc/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/retroc/discussions)
- **Twitter**: [@yourhandle](https://twitter.com/yourhandle)
- **Discord**: [Join our community](https://discord.gg/yourserver)

---

<div align="center">

**Made with ❤️ by the Solidity Community**

**RetroC** - Retro Contracts, Modern Speed

⭐ Star us on GitHub — it helps!

[Report Bug](https://github.com/yourusername/retroc/issues) · [Request Feature](https://github.com/yourusername/retroc/issues) · [Documentation](https://github.com/yourusername/retroc/wiki)

</div>
