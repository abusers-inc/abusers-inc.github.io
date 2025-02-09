# Invisible Hand
> **Status**: Active debugging
## Description
Market maker and price manipulator for PumpFun and Raydium pools.

## Requirements
- Solana private keys with enough amount of sol
- Solana RPC Node URL

## Getting Started
First, you need to create a `config.toml` file. This file will contain the necessary configuration for the bot to operate.

### Configuration File
The `config.toml` file should be placed in the root directory of the project. Here is an example of what the file should look like:

```toml
# filepath: /path/to/config.toml
# Configuration for Invisible Hand bot

# List of Solana private keys
accounts = [
    "your_private_key_1",
    "your_private_key_2",
    "your_private_key_3"
]

# Solana RPC Node URL
rpc_url = "https://api.mainnet-beta.solana.com"
```

## Running the Bot
Once you have configured the `config.toml` file and chosen the command to execute, you can run the bot using the following command:

```sh
solanamm
```

# Launch token
This command allows you to launch and buy out a percentage of the supply of a token.

```
Enter percent of supply you want to buy out (from 0 to 100): 50
Enter delay between supply buyout in seconds: 10
Enter BPS of allowed slippage: 10
Enter token name: MyToken
Enter token symbol: MTK
Enter token URI: https://example.com/token-uri
```

# Manipulate Price
This command allows you to manipulate the price of a token in a specified AMM pool.

```
Enter AMM PubKey of target pool: <AMM_PUBKEY>
Enter BPS amount of price manipulation (100 bps = 1%): 100
Enter amount of seconds to sleep (minimum): 5
Enter amount of seconds to sleep (maximum): 10
Enter acceptable slippage BPS (100 bps = 1%): 10
```

# Maintain Price
This command allows you to maintain the price of a token within a specified range.

```
Enter AMM PubKey of target pool: <AMM_PUBKEY>
Enter token mint PubKey: <TOKEN_MINT_PUBKEY>
Enter minimum price: 1.0
Enter maximum price: 2.0
Enter maximum price change percentage per timeframe: 5
Enter acceptable slippage BPS (100 bps = 1%): 10
```



The bot will prompt you to choose a command and enter the necessary parameters. Follow the prompts to execute the desired command.

## Troubleshooting
If you encounter any issues while running the bot, check the following:

- Ensure that your `config.toml` file is correctly formatted and contains valid Solana private keys and RPC URL.
- Verify that your Solana accounts have enough SOL to perform the desired actions.
