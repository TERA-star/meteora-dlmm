
# DLMM Chain Pool Liquidity Management System
## Project Overview

The DLMM Chain Pool Liquidity Management System is an automated management tool designed specifically for DLMM (Discrete Liquidity Market Maker) pools on the Solana blockchain.
The system continuously monitors and maintains the liquidity distribution across multiple chained pools in real time, ensuring that the liquidity conforms to the BidAsk model for optimized trading efficiency and reduced slippage.

When the market price changes and crosses different position ranges, the system automatically detects and adjusts any positions that do not comply with the BidAsk model, ensuring that market liquidity always remains in an optimal state.
This automated management greatly reduces the operational burden for liquidity providers while improving overall market efficiency.

## Core Features
### 1. Dynamic Pool Management

- Automatic Pool Discovery – The system automatically scans and identifies all DLMM pool positions owned by the user on startup, without requiring manual configuration.

- Chained Pool Management – Supports simultaneous management of multiple DLMM liquidity pools in a chain, ensuring coordinated operation.

- Real-Time Position Analysis – Continuously collects and analyzes bin data and liquidity distribution for each position.
 
### 2. BidAsk Model Compliance Check

- Liquidity Distribution Validation – Checks whether each position’s liquidity distribution meets the BidAsk model requirements.

- Ascending/Descending Distribution Detection – Ensures that liquidity above the current price is distributed in ascending order, and liquidity below the current price is in descending order.

- Compliance Report – Generates detailed reports showing specific reasons for non-compliance.


### 3. Automatic Adjustment Strategy

- Liquidity Removal – Automatically removes 100% of liquidity from positions that do not conform to the BidAsk model.

- Re-Adding Liquidity – Re-adds liquidity using the correct BidAsk strategy to ensure compliance.

- Gradual Adjustment – Adjusts one position at a time for a smooth and stable process.

### 4. Real-Time Price Monitoring

- Active Bin Monitoring – Continuously tracks changes in the active bins of each pool.

- Price Movement Detection – Detects real-time price changes of the X/Y tokens.

- Pool Crossing Detection – Automatically triggers compliance checks when prices move across position ranges.

### 5. Security & Private Key Management

- Encrypted Private Key Storage – Supports password-encrypted private keys for enhanced security.

- Multi-Level Private Key Loading – Allows loading private keys from encrypted or configuration files.

- User Authentication – Prompts user verification before performing critical operations.

### 6. Transaction Optimization

- Priority Fee Configuration – Allows users to set transaction priority fees to improve success rates.

- Automatic Retry Mechanism – Automatically retries failed transactions up to 5 times in case of temporary errors.

- Compute Unit Optimization – Configurable compute unit limits for optimized transaction execution.

### 7. Visualization & Logging

- Real-Time Terminal Display – Displays pool states and adjustment progress in real time.

- Detailed Logging – Records every system operation for troubleshooting.

- Status Updates – Visually indicates current system state and progress.

## System Architecture

The DLMM Chain Pool Liquidity Management System adopts a simplified modular design, divided into several main components:

dlmm-chain-pools-manager/
├── src/
│   ├── models.ts         # Data model definitions
│   ├── services.ts       # Core business logic
│   ├── utils.ts          # Utility functions
│   ├── logger.ts         # Logging module
│   ├── display.ts        # Display and visualization
│   ├── config.ts         # Configuration file
│   └── index.ts          # Main program entry
├── package.json          # Project dependencies
└── tsconfig.json         # TypeScript configuration


## Core Module Descriptions

### 1 Data Models (models.ts)

- Defines key data structures such as pools, positions, and pool chains.

- Contains data handling and validation logic.

- Implements foundational functions for BidAsk model compliance checks.

### 2 Service Functions (services.ts)

- Centralizes all core business logic.

- Includes connection management, wallet service, pool discovery, and price monitoring.

- Implements key algorithms for liquidity adjustments.

- Handles all interactions with the blockchain.

### 3 Utility Functions (utils.ts)

- Provides general-purpose helper utilities and algorithms.

- Implements retry logic, data formatting, time, and computation utilities.

### 4 Logging Module (logger.ts)

- Manages system-wide logging.

- Supports multiple log levels (DEBUG, INFO, WARNING, ERROR).

- Provides structured and formatted log output.

### 5 Display Module (display.ts)

- Handles terminal interface and user interaction.

- Visualizes pool status and operational progress.

### 6 Provides color-coded status indicators.

- Configuration (config.ts)

- Centralizes all system settings and parameters.

- Includes network, monitoring, and adjustment strategy configurations.

### 7 Main Program (index.ts)

- Entry point of the system.

- Coordinates all modules and implements the main workflow.

- Handles startup, continuous execution, and graceful shutdown.


## Installation Guide
### 1 Prerequisites

- Node.js v14.0.0 or higher

- npm v6.0.0 or higher

- A valid Solana wallet (for managing liquidity)

### 2 Installation Steps

1. Clone the project
   git clone https://github.com/yourusername/dlmm-chain-pools-manager.git
   cd dlmm-chain-pools-manager

2. Install dependencies
   ```bash
    npm install
   ```

3. Configure the system
   // Basic configuration
   export const CONFIG = {
   RPC_ENDPOINT: "https://api.mainnet-beta.solana.com",
   REFRESH_INTERVAL_MS: 10000,
   DISPLAY_ENABLED: true,
   LOG_LEVEL: "info",
   };

   // Wallet configuration
   export const WALLET_CONFIG = {
   PRIVATE_KEY: "your-private-key", // Base58 encoded
   };

   // Transaction configuration
   export const TRANSACTION_CONFIG = {
   ENABLE_PRIORITY_FEE: true,
   PRIORITY_FEE_MICROLAMPORTS: 200000,
   };

4. Build the project
   ```bash
   npm run build
   ```
## Usage
### 1 Development Mode
   ```bash
      npm run dev
   ```         

### 2 Production Mode
   ```bash
      npm run build
      npm start
   ```

### 3 Exit Program
   Press Ctrl + C to safely exit.

## Workflow

### 1 Initialization

- Load configuration.

- Connect to the Solana network.

- Initialize wallet.

- Scan and discover all DLMM positions.

### 2 Monitoring

- Periodically poll for active bin and price changes.

- Trigger pool crossing detection on bin change.

- Verify whether adjacent positions comply with the BidAsk model.

### 3 Adjustment

- Remove liquidity from non-compliant positions.

- Re-add liquidity according to the BidAsk model.

- Refresh position data to ensure changes are applied.

### 4 Display

- Update terminal view with current status.

- Record detailed logs for future analysis.


## Configuration Parameters.
| 配置项                     | 说明                           | 默认值                              |
| -------------------------- | ------------------------------ | ----------------------------------- |
| RPC_ENDPOINT               | Solana RPC endpoint            | https://api.mainnet-beta.solana.com |
| REFRESH_INTERVAL_MS        | Data refresh interval (ms)     | 10000                               |
| DISPLAY_ENABLED            | Enable terminal display        | true                                |
| LOG_LEVEL                  | Logging level                  | info                                |
| PRIORITY_FEE_MICROLAMPORTS | Priority fee (microLamports)） | 200000                              |
| MAX_RETRIES                | Maximum transaction retries    | 5                                   |

## BidAsk Model Explanation

The BidAsk model optimizes liquidity distribution by following these principles:

### 1 Above current price (Ask side): Liquidity is distributed in ascending order

e.g., bin 100 = 10 tokens, bin 101 = 20 tokens, bin 102 = 30 tokens...

### 2 Below current price (Bid side): Liquidity is distributed in descending order

e.g., bin 99 = 30 tokens, bin 98 = 20 tokens, bin 97 = 10 tokens...

This structure concentrates liquidity around the most likely trading price ranges, improving capital efficiency.

## Private Key Encryption

To enhance security, the system supports encrypted private key storage to avoid saving plain-text keys in configuration files.

### 1 Steps to Encrypt Private Key
1. Run encryption command
   ```bash
   npm run encrypt-key
   ```

2. Follow prompts
   Enter private key (Base58 format): <your key>
   Set encryption password: <password>
   Confirm password: <password>

3. Verify encrypted file creation
   After success, a .key file is created in the project root, and the configuration file is updated automatically:

   export const WALLET_CONFIG = {
      USE_ENCRYPTED_KEY: true,
      PRIVATE_KEY: "",
      KEY_FILE_PATH: "./.key",
   };

### 4 Using Encrypted Private Key
   When launching with encryption enabled (USE_ENCRYPTED_KEY: true), the program will prompt for a password: 
   ```bash
   npm start
   ```
   Prompt: Please enter password to unlock private key:

   Once entered correctly, the key is decrypted and loaded.

###Security Recommendations

- Use a strong password with mixed characters.

- Rotate passwords and keys regularly.

- Never share or commit .key files to version control.

- Add .key to .gitignore.

## Troubleshooting
### 1 Common Issues

1. Connection Error

- Check your RPC endpoint configuration.

- Verify network connectivity.

- Try an alternative RPC endpoint.

2. Transaction Failed

- Increase the priority fee.

- Ensure wallet balance is sufficient.

- Review logs for detailed errors.

3. Configuration Load Error

- Ensure config.ts exists and is correctly formatted.

- Check file permissions.

## Security Recommendations

### 1 Private Key Security

- Never store plain keys in configs.

- Prefer environment variables.

- Regularly replace keys.

### 2 Permission Control

- Use a dedicated wallet for liquidity management.

- Do not store large funds in it.

### 3 Network Security

- Use reliable RPC endpoints.

- Avoid running on insecure networks.

## License

This project is licensed under the MIT License.


### 📞 Telegram: [manchatz](https://t.me/manchatz)   
https://t.me/sven.dev

### 📞 X: [SvenDotDev](https://x.com/SvenDotDev)
https://x.com/SvenDotDev