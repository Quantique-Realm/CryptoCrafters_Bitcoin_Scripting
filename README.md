# CryptoCrafters_Bitcoin_Scripting
# Bitcoin Scripting Project

## Team Details

- **Team Name:** CryptoCrafters
- **Team Members:**
  - Abhiraj Kumar(mc230041001)
  - Harsh Bhati(mems230005017)
  - Bhalchandra Kalyani Buradkar(cse230001017)

---

## Overview

This project explores Bitcoin scripting and transaction creation using Python. It focuses on comparing Legacy (P2PKH) and SegWit (P2SH-P2WPKH) address formats, highlighting their differences in transaction size, structure, and efficiency. The implementation demonstrates the process of creating, signing, broadcasting, and validating Bitcoin transactions while extracting key components like ScriptPubKey and ScriptSig.

### Key Objectives:
- Understand the process of creating Bitcoin transactions programmatically.
- Compare transaction sizes and efficiencies between Legacy and SegWit formats.
- Analyze the scripting mechanisms (ScriptPubKey and ScriptSig) used in Bitcoin transactions.

---

## Features

- **Wallet Management:** Create or load a wallet and generate Bitcoin addresses.
- **Funding Transactions:** Mine initial blocks to fund a specific address.
- **Transaction Creation:** Create raw transactions, extract scripts, and decode them.
- **Transaction Signing:** Sign transactions using private keys.
- **Broadcasting Transactions:** Send transactions to the Bitcoin network.
- **UTXO Management:** Fetch UTXO details for addresses after transactions.
- **Validation:** Validate extracted scripts using the Bitcoin Debugger.

---

## Implementation Details

### Workflow:

1. **Wallet Setup:**
   - Create or load a wallet and generate three addresses: A, B, and C.

2. **Funding Address A:**
   - Mine initial blocks to fund address A with UTXOs.
   - Display the UTXO balance of address A.

3. **Transaction A → B:**
   - Prompt the user for an amount to transfer from A to B (ensuring it satisfies `0 < Amount ≤ UTXO(A) - Mining fee`).
   - Create a raw transaction transferring coins from A to B.
   - Decode the raw transaction to extract the challenge script (ScriptPubKey).
   - Display the transaction size in virtual bytes (vbytes).

4. **Signing and Broadcasting Transaction A → B:**
   - Sign the transaction using A's private key.
   - Broadcast the transaction on the network.
   - Display the transaction ID and size.

5. **Fetching UTXO Details for Address B:**
   - Retrieve UTXO details for address B after the transaction A → B.

6. **Transaction B → C:**
   - Create a new transaction from B to C funded by B's UTXO balance.
   - Follow similar steps as in transaction A → B:
     - Create, sign, broadcast, decode, and extract response script (ScriptSig).
     - Display the transaction ID and size in vbytes.

7. **Validation of Scripts:**
   - Validate extracted scripts using the Bitcoin Debugger (`btcdeb`).

8. **Wallet Unloading:**
   - Unload the wallet at the end of execution.

---

## Customizations

### 1. User Credentials:
The `bitcoin.conf` file contains default credentials (`user = admin`, `password = admin`). You can update these credentials:
- Modify `rpcuser` and `rpcpassword` fields in `bitcoin.conf`.
- Update the `get_rpc_connection()` function in Python scripts accordingly.

### 2. Number of Initial Blocks Mined:
By default, 101 blocks are mined to fund address A. You can change this number by modifying:
conn.generatetoaddress(101, address_A)

### 3. Transaction Fee:
A default transaction fee of 0.00001 BTC is set for transactions. You can adjust this fee by modifying the `fee` variable in Python scripts.

---

## How to Run

### Prerequisites:
1. Install Bitcoin Core software on your system.
2. Install Python along with required libraries (`json`, `requests`, etc.).

### Step-by-Step Instructions:

1. **Configure Bitcoin Core:**
   - Navigate to `C:\Users\<username>\AppData\Roaming\Bitcoin` on Windows (replace `<username>` with your actual username).
   - Place the provided `bitcoin.conf` file in this directory.

2. **Launch Bitcoin Core in Regtest Mode:**
   Open Command Prompt and execute:
cd "C:\Program Files\Bitcoin\daemon"
bitcoind.exe -regtest

3. **Run Python Scripts:**
- Execute `Legacy_1.py` to create transaction A → B and extract ScriptPubKey.
- Run `Legacy_2.py` for transaction B → C and extract ScriptSig.

4. **Run SegWit Scripts:**
Before running SegWit scripts (`SegWit.py`), delete previous regtest data:
- Close Command Prompt.
- Delete the `regtest` directory inside `C:\Users\<username>\AppData\Roaming\Bitcoin`.

5. Execute `SegWit.py` to create similar transactions using SegWit address formats.

---

## Validating Extracted Scripts

To validate extracted scripts:

1. Connect to the Bitcoin Debugger server:
 ```
 ssh guest@10.206.4.201
 ```
 Password: `root1234`

2. Run validation commands:
 ```
 btcdeb -v '<ScriptSig><ScriptPubKey>'
 ```
 Replace `<ScriptSig>` with the response script and `<ScriptPubKey>` with the challenge script (concatenated without spaces). If valid, you'll see "valid script" in the output; otherwise, "invalid script."

---

## Example Outputs

### Legacy Format:

- Transaction Size (A → B): XX vbytes  
- ScriptPubKey Size: XX vbytes  
- Transaction Size (B → C): XX vbytes  
- ScriptSig Size: XX vbytes  

### SegWit Format:

- Transaction Size (A → B): XX vbytes  
- ScriptPubKey Size: XX vbytes  
- Transaction Size (B → C): XX vbytes  
- ScriptSig Size: XX vbytes  

---

## Key Differences Between Legacy and SegWit Formats

1. **Transaction Size:** SegWit transactions are smaller due to optimized signature storage.
2. **Efficiency:** SegWit reduces malleability issues and improves scalability.
3. **Script Structure:** 
 - Legacy uses ScriptPubKey for challenge scripts and ScriptSig for response scripts.
 - SegWit separates witness data into a dedicated structure outside of standard inputs/outputs.

---

## Troubleshooting

1. Ensure Bitcoin Core is running in regtest mode before executing Python scripts.
2. If you encounter issues with regtest data during SegWit execution, delete the `regtest` directory as described above.
3. Validate extracted scripts using `btcdeb` if you suspect invalid outputs.

---

## Acknowledgements
We would like to thank:
- Prof. Subhra Mazumdar for introducing us to Bitcoin scripting concepts and addressing formats.
- The helpful GitHub documentation on accessing Bitcoind with Python, which guided our implementation process.
---

