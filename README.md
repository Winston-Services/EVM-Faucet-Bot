# Faucet Bot Setup

## Basic Setup
Create a folder to put the settings and application in.

`cd ~/`

`mkdir faucet-bot`

`cd faucet-bot`

## Download the Bot Application Executable
For Windows Use :

`wget https://winston.services/bots/Faucet-Bot?download=win`

For Linux Use :

`wget https://winston.services/bots/Faucet-Bot?download=linux`

For MacOs Use :

`wget https://winston.services/bots/Faucet-Bot?download=mac`

For Arm Use :

`wget https://winston.services/bots/Faucet-Bot?download=arm`

Or Download the latest version of the bot from :

`https://winston.services/bots/Faucet-Bot`

Note : In this documentation we make a few assumptions. You may need to adjust your actual input for your OS version.

## Install the Dependencies
You will need to have the latest version of nodejs installed to install this dependancy. You can download it from their website [NodeJS](https://nodejs.org/en/download)
Next we need to install the Sqlite Database Dependencies. Sqlite is used to store the data that keeps track of user balances, transactions, and settings for the bot.

Dependencies : 
Sqlite3
`npm i -G sqlite3`

## Install the ABI's 
Download the ABI's to `/src/json`
We have included a few of the ABI's we find as standard in the following Repository on Github. 

`https://github.com/winston-services/faucet-bot`

It's recommended that you use the ABI's that are for your assets if they are not already included in the repository. You can download them from the blockexplorer. While at the blockexplorer register to get your API keys, so that you can use Ethers Network Provider API's.

[Discord Developer Portal](https://discord.com/developers/applications)
Next you will want to go to Discord Developer Portal to create your bot's credentials. Here's what you will need to do.

![image](https://github.com/Winston-Services/EVM-Faucet-Bot/assets/29209354/673c7ff6-95f1-42f3-aef3-3344896bd9fe)

Under this section you can copy your Discord Application ID.

![image](https://github.com/Winston-Services/EVM-Faucet-Bot/assets/29209354/69c0407e-39f9-4407-a8d9-e59b2cd60d70)

Under the bot section you can get your token for the bot. Click on "Reset Token" to view the token and reset it. Copy it and add it to the .env file as the "DISCORD_TOKEN".

![image](https://github.com/Winston-Services/EVM-Faucet-Bot/assets/29209354/cb870e42-3bd7-4f04-9127-755dc9f05297)

Make sure to enable these two features, so that the bot can get user information and read the content they send.

## Set the Options
Next edit the `.env` file to update the following information.

```.env
OWNER_GUILD_ID=
DISCORD_APPLICATION_ID=
DISCORD_TOKEN=
UPDATE=false
LINK="https://discord.com/api/oauth2/authorize?client_id={{CLIENT_ID}}&permissions=2416266304&scope=bot"
BASE_TOKEN="0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE"
ENABLED=true
STAKING_ENABLED=true
PROVIDER_URL=
NETWORK_DEAD_ADDRESS="0x000000000000000000000000000000000000dEaD"
ROUTER_ADDRESS="0xEfF92A263d31888d860bD50809A8D171709b7b1c"
FACTORY_ADDRESS="0xcA143Ce32Fe78f1f7019d7d551a6402fC5350c73"
PRIMARY_PAIR_ADDRESS="0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2"
SECONDARY_PAIR_ADDRESS="0xdAC17F958D2ee523a2206206994597C13D831ec7"
DO_NOTHING_CHANCE=15
IGNORE_CHANCE=5
CHANGE_COUNT_CHANCE=2
TIMEOUT_USER_CHANCE=1
TIMEOUT_MAX_TIME_SETTING="15m"
```

`nano .env`

#### OWNER_GUILD_ID 

Used to limit the access to the bot to a specific server on discord. Add the server ID you want to whitelist.

#### DISCORD_APPLICATION_ID
The ID of the bot itself, you can get this from discord developer portal. While your there you will need to set these settings.

#### DISCORD_TOKEN
This is the token you will get for your bot on the Discord Developer Portal. Below are the instructions on how to do that.

#### UPDATE
The update option is used to update the Discord Server with the slash-commands for the bot. This only needs to be enabled once, and started. Once you have ran it once enable you can disable it so that it doesnt need to update the commands each time the bot is started.

#### LINK
The link option is the url used to add the bot to the server. Replace {{CLIENT_ID}} with the actual bot's client ID. You can get that from the Discord Developer Portal.

#### BASE_TOKEN
The base token is the asset the faucet will use for its features. Add the contract address for the token to be used in the bots features.

#### ENABLED
The enabled option is used to toggle the Withdraw feature. To enable withdraws from the bot set this to true, to disable them set this option to false.

#### STAKING_ENABLED
This option is used to toggle the staking feature. Set this to true to enable staking, set it to false to disable staking.

#### PROVIDER_URL
The provider url should be the url to the RPC service or one of 
`mainnet`, `bnb`, `matic`, `arb`

#### NETWORK_DEAD_ADDRESS
This should be the dead address for the chain. The standard address is `0x000000000000000000000000000000000000dEaD` if the chain used does not use this address set it to the address that is known as the dead address for that chain.

#### ROUTER_ADDRESS
The router address is the contract address of the dex router used for pricing. UniSwap v2 Contracts or Equevelant should be used.

#### FACTORY_ADDRESS
The factory address is the contract address of the dex factory used to control the pairs. Set this to the UniSwap V2 or compatible Factory Address.

#### PRIMARY_PAIR_ADDRESS 
The primary pair address is the contract to the asset that is the primary pair for the chain. (WETH, WMATIC, WBNB etc.)

#### SECONDARY_PAIR_ADDRESS
The secondary pair address is the contract address to the asset that is the stable coin paired to the base asset.

#### DO_NOTHING_CHANCE
The do nothing chance option is used to change the odds the counter feature will do nothing.

#### IGNORE_CHANCE
The Ignore Chance option is used to change the odds the counter feature will ignore the user.

#### CHANGE_COUNT_CHANCE
The Change Count Chance option is used to change the odds the counter feature will reset the counter to a random number between 0 and its current position.

#### TIMEOUT_USER_CHANCE
The Timeout User Chance option is used to change the odds the counter feature will time the user out for a random duration.

#### TIMEOUT_MAX_TIME_SETTING
The Timeout Max Time Setting option is used to change the max time out period a user can get if they are timedout of the counter feature.


Now let's add the ABI's to interact with these assets.

1) ABI.json Base Token ABI
1) ABI.json Primary Token ABI
1) ABI.json Secondary Token ABI
1) ROUTER.json is the Router ABI for the dex.
1) FACTORY.json is the Factory ABI for the dex.
1) Pair.json is the Pair ABI for the dex pair used to swap the assets for gas.
##### What is an ABI?
ABI stands for `Application Binary Interface`. It is basically a set of interpreter commands to allow external programs to interact with contracts on the blockchain.

## Invite the bot
`https://discord.com/api/oauth2/authorize?client_id={{CLIENT_ID}}&permissions=2416266304&scope=bot`

Replace CLIENT_ID with the ID of the Discord Bot.
Follow the link to invite the bot to the Discord server.

## Bot Slash Commands
#### /balance
Get the bot and users balances.

#### /info
Get detailed information about the assets used in the bot. Including pricing and balance information.
#### /faucet
Claim a portion of the available faucet balance.
#### /deposit
Deposit funds to the faucet bot. This is a donation to the bot's faucet balance.
#### /stake
Stake an amount of assets held in the users wallet.
#### /unstake
Un-stake all balances staked or locked in the bot.

#### /withdraw
Withdraw funds from the bot to an external wallet.

#### /help
Get general bot help information.

## Bot Settings

### Channel Settings
#### /set counter-channel
Set the channel to lock the counting feature to. This will set the bot to only allow counting in this channel.

#### /set faucet-channel
Set the channel to lock the faucet feature to. This will set the bot to only allow users to claim the faucet in this channel.

#### /set staking-rewards-channel
Set the channel to show the staking reward payouts. This should be a locked channel that others can read buy not write in.

### Role Settings
#### /set faucet-role
Set the faucet role to limit who can use the faucet by their roles.

### Clear Channels and Roles
#### /set clear-faucet-role
Clear the existing Faucet Role limit.
#### /set clear-faucet-channel
Clear the existing Faucet Channel limit.
#### /set clear-counter-channel
Clear the existing Counter Channel limit. 
## Bot Admin Features and Settings
#### /set min-withdraw
Set the minimal withdraw amount. This will require users to have a balance higher than or equal to this amount.

#### /set claim-interval
Set the interval in which users can claim the faucet. Use time patterns like 1h 5m or 15s.
#### /set fee
Set the fee the bot will charge for withdrawing funds from the bot.
#### /set correct
Add missed transaction by the blocknumber. Enter the blocknumber of the transaction that was not caught by the bot's deposit process.
#### /set reconcile
You will need to run the reconcile feature if and only if you have ran the `/set correct` feature to add a missing transaction. This will correct the bots balances and insure the bot is calculating the right amount of assets.
#### /set allow-ignore
Enable this feature to allow the bot to ignore users when they are counting. The enables the random process of ignoring users while they count.
#### /set allow-change-count
Enable this feature to allow the bot to reset the counter randomly to a number between 0 and its current count.

