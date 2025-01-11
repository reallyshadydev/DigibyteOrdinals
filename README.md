

Certainly! Here's the updated README with the correct token reference as DGB:

```markdown
# DigibyteOrdinals

A minter and protocol for inscriptions on DigiByte. 

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

Use this wallet for inscribing only! Avoid storing ordinals in DigiByte Core.

Please use a fresh paper wallet to mint to with nothing else in it until proper wallet support for ordinals comes.

This wallet is not meant for storing funds or inscriptions.

## Prerequisites

To use this, you'll need to set up a DigiByte node, clone this repo, and install Node.js on your computer.

### Setup DigiByte Node

Install DigiByte Core from the official DigiByte GitHub: (https://github.com/digibyte/digibyte/releases)

### ⚠️⚠️⚠️ Important ⚠️⚠️⚠️
A configuration file needs to be created before you continue with the sync.

- Stop your node

- Create a `digibyte.conf` file in your DigiByte data folder.

- Copy and paste this to the created file. Set your own username/password. Save it!

```
rpcuser=your_username
rpcpassword=your_password
rpcport=12024
server=1
listen=1
txindex=1
rpcallowip=127.0.0.1
```

- Start your node again

- Wait for your node to sync with the network.

==========

### Install NodeJS

Please head over to (https://nodejs.org/en/download) and follow the installation instructions for your system.

==========

### Setup DigibyteOrdinals

#### Clone DigibyteOrdinals Minter
On your Terminal, type the following commands:
```
cd
git clone https://github.com/reallyshadydev/DigibyteOrdinals.git
```

#### Setup Minter

```
cd DigibyteOrdinals
npm install
cd bitcore-lib-digibyte
npm install
cd ..
```

After all dependencies are resolved, you can configure the environment:

#### Configure Environment

Create a `.env` file with your node information. Set the same username/password used in `digibyte.conf`.

```
NODE_RPC_URL=http://127.0.0.1:12024
NODE_RPC_USER=your_username
NODE_RPC_PASS=your_password
TESTNET=false
```

==========

#### ⚠️⚠️⚠️ Important ⚠️⚠️⚠️
Before proceeding, please make sure your node is fully synced.
Have fun!

### Managing Wallet Balance

Generate a new `.wallet.json` file:

```
node . wallet new
```

Retrieve your private key from `.wallet.json` and import it in DigiByte Core, this can be done from the GUI or the following command

```
digibyte-cli importprivkey <your_private_key> <optional_label> false
```

Then send DGB to the address displayed. Once sent, sync your wallet:

```
node . wallet sync
```

If you are minting a lot, you can split up your UTXOs:

```
node . wallet split <count>
```

When you are done minting, send the funds back:

```
node . wallet send <address> <optional amount>
```

==========

### Minting Ordinals

**Note**: Please use a fresh wallet to mint to with nothing else in it until proper wallet support for ordinals comes. 

**Do not mint to DigiByte Core**

#### Inscribe a File
From file:

```
node . mint <address> <path>
```

From data:

```
node . mint <address> <content type> <hex data>
```

Examples:

```
node . mint DgB1ocks3ozcti7m5a3i2wViSuFAchLm3n digibyte.jpeg
```

```
node . mint DgB1ocks3ozcti7m5a3i2wViSuFAchLm3n "text/plain;charset=utf-8" 52696262697421 
```

#### Deploy DGB-20

```
node . dgb-20 deploy <address> <ticker> <max token supply> <max allowed mint limit>
```

Examples: 

```
node . dgb-20 deploy DgB1ocks3ozcti7m5a3i2wViSuFAchLm3n frog 1000 100
```

#### Mint DGB-20

```
node . dgb-20 mint <address> <ticker> <amount>
```

Examples: 

```
node . dgb-20 mint DgB1ocks3ozcti7m5a3i2wViSuFAchLm3n frog 100
```

### Viewing Ordinals

**Note**: There is currently a bug preventing the preview of some larger ordinal files. Wait for a fix or an ordinals indexer. 

Viewing small inscriptions seems to work. Investigating...

Start the server:

```
node . server
```

And open your browser to:

```
http://localhost:3000/tx/4650300f65470c359c070ae6b88ab7945adad68458c33285968ce0bfa502e52c
```

==========

### Additional Info

#### Protocol

The ordinals protocol allows any size data to be inscribed onto subwoofers.

An inscription is defined as a series of push datas:

```
"ord"
OP_1
"text/plain;charset=utf-8"
OP_0
"Ribbit!"
```

For ordinals, we introduce a couple extensions. First, content may spread across multiple parts:

```
"ord"
OP_2
"text/plain;charset=utf-8"
OP_1
"Ribbit and "
OP_0
"ribbit ribbit!"
```

This content here would be concatenated as "Ribbit and ribbit ribbit!". This allows up to ~1500 bytes of data per transaction.

Second, P2SH is used to encode inscriptions.

There are no restrictions on what P2SH scripts may do as long as the redeem scripts start with inscription push datas.

And third, inscriptions are allowed to chain across transactions:

Transaction 1:

```
"ord"
OP_2
"text/plain;charset=utf-8"
OP_1
"Ribbit and "
```

Transaction 2

```
OP_0
"ribbit ribbit!"
```

With the restriction that each inscription part after the first must start with a number separator, and number separators must count down to 0.

This allows indexers to know how much data remains.

### Troubleshooting

#### I'm getting ECONNREFUSED errors when minting

There's a problem with the node connection. Your `digibyte.conf` file should look something like:

```
rpcuser=your_username
rpcpassword=your_password
rpcport=12024
server=1
listen=1
txindex=1
rpcallowip=127.0.0.1
```

Make sure `port` is not set to the same number as `rpcport`. Also make sure `rpcauth` is not set.

Your `.env file` should look like:

```
NODE_RPC_URL=http://127.0.0.1:12024
NODE_RPC_USER=your_username
NODE_RPC_PASS=your_password
TESTNET=false
```

#### Other issues

Try restarting your DigiByte node.

If still stuck, ask ChatGPT or search online for other solutions.
```

This version uses "DGB-20" for the token references and is tailored for DigibyteOrdinals.

