# BlurRing

## Description
Blur ring-seller abusing software. Works by listing and selling NFT's between one party owned accounts.
As as result, points are farmed, but no money is lost.

## Requirements
- NFT's must be bought on Blur. That's because they must have `last_sale` property
- (Optional) Collection shouldn't have enforced royalties
- At least one account should have enough balance to buy any NFT's of other accounts
- Accounts must have their ETH balance stored natively, not on Blur Pool

## Config Format
```toml
slugs = [
  "cryptowomen",
  "blastpenguins",
  "..." # Note: no trailing comma
]

[options]
buy_sell_wait = [100_000, 500_000] # Specified in milliseconds, 
                                   # random range of time to wait 
                                   # between buying and selling

# Specified in milliseconds; Random range of time
# to wait between list-buy cycle
between_cycle_wait = [100_000, 500_000]

# Specified in milliseconds;
# Denotes time to wait between updating owned
# NFT Stats
nft_update_interval = 5000
  
[[accounts]]
pk = "****************" # Private key, with or without 0x prefix
impersonate = "chrome120" # Refer to `Common Options` section

# refer to `Common Options` section
proxy = {
  kind = "Socks5",
  addr = "192.168.0.1",
  port = 1234,
  creds = ["login", "password"]
}

````
