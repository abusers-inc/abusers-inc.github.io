# BlurRing

## Description
Blur ring-seller abusing software. Works by listing and selling NFT's between one party owned accounts.
As as result, points are farmed, but no money is lost.

## Requirements
- NFT's **must be bought** on Blur. That's because they must have `last_sale` property
- (Optional) Collection shouldn't have enforced royalties
- At least one account should have enough balance to buy any NFT's of other accounts
- Accounts must have their ETH balance stored natively, not on Blur Pool

## Algorithm
First of all, bot loads all accounts and their NFT's. 
Then, it parses ETH balance of each accounts.
If some NFT from any accounts priced higher than maximum balance across all accounts, it will be excluded from search.

After that, bot will choose random account and random NFT to buy.
Then, it will list this NFT for sale with price + collection royalty to compensate if somebody else will buy it.
After that, bot will wait for random time and then will buy this NFT back from some random accounts, but only if it has enough balance.
Then, bot will wait for random time and repeat the cycle.

In short:
1. Choose seller and NFT
2. Choose buyer
3. List NFT for sale
4. Wait for random time
5. Buy NFT back
6. Wait for random time


## Config Format
```toml
slugs = [
  "cryptowomen",
  "blastpenguins",
  "..." # Note: no trailing comma
]

# Optional field. Remove '#' if you want to set custom RPC
# rpc = "https://rpc.blast.io"

[options]
buy_sell_delay = [100_000, 500_000] # Specified in milliseconds, 
                                   # random range of time to wait 
                                   # between buying and selling

# Specified in milliseconds; Random range of time
# to wait between list-buy cycle
between_cycle_delay = [100_000, 500_000]

# Specified in milliseconds;
# Denotes time to wait between updating owned
# NFT Stats
nft_update_interval = 5000
  
[[accounts]]
pk = "****************" # Private key, with or without 0x prefix
impersonate = "chrome120" # Refer to `Common Options` section

# refer to `Common Options` section
[accounts.proxy]
kind = "Socks5",
addr = "192.168.0.1",
port = 1234,
creds = ["login", "password"] # Remove this entire line if not authentication is needed

[[accounts]]
pk = "****************" # Private key, with or without 0x prefix
impersonate = "chrome119" # Refer to `Common Options` section

# refer to `Common Options` section
[accounts.proxy]
kind = "Socks5",
addr = "172.168.0.1",
port = 1234,
creds = ["login", "password"]
````

## How to get slug
1. Go to some collection (Note: it must be blast collection)
2. Look at the url
3. Extract all symbols after last "/"

### Example
`https://blur.io/collection/azuki`
> Slug here is: `azuki`
![Slug Illustration](blur_slug.png)

## Config Example
[config.toml](blurring_assets/config.toml) <br/>
[config_no_proxy.toml](blurring_assets/config_no_proxy.toml)
