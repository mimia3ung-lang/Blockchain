# COMP842 Individual Technical Assessment Portfolio

**Course:** COMP842 – Applied Blockchains and Cryptocurrencies  
**Assessment:** Individual Technical Assessment Portfolio  
**Student:** ME ME AUNG  
**Student ID:** 25293849  
**University:** Auckland University of Technology (AUT)  

This repository contains the Python source code used for **Exercises 1, 2 and 3** of the COMP842 Individual Technical Assessment Portfolio.

The exercises cover:

- Blockchain structure and tamper detection
- Proof of Work mining, difficulty and probability
- Elliptic Curve Cryptography (ECDSA) and public-key compression

> This repository is for academic assessment and learning purposes.

---

# Exercise 1 – Blockchain Structure and Tamper Detection

## Objective

Exercise 1 implements a simple blockchain in Python to demonstrate:

- SHA-256 hashing
- Merkle Roots
- Block linking using `previous_hash`
- Genesis block creation
- Blockchain validation
- Detection of transaction tampering

## Main Features

The implementation includes:

- `hash_data()` – generates SHA-256 hashes
- `create_merkle_root()` – calculates a Merkle Root from transaction data
- `Block` class – stores:
  - block height
  - timestamp
  - previous block hash
  - transactions
  - Merkle Root
  - block hash
- `Blockchain` class – supports:
  - automatic genesis block creation
  - adding new blocks
  - displaying the blockchain
  - validating the complete chain
  - reporting the first invalid block

## Experiment

The program creates a blockchain containing **10 blocks**, including the genesis block.

The original blockchain is validated first.

Then the first transaction in **Block 5** is changed from:

```text
Grace pays Helen $40
```

to:

```text
Grace pays Helen $4000
```

The stored Merkle Root and block hash are intentionally not recalculated.

## Expected Result

Before tampering:

```text
Blockchain valid: True
Result: The blockchain is valid.
```

After tampering:

```text
Blockchain valid: False
First invalid block: 5
Reason: Transaction data does not match the stored Merkle Root.
```

This demonstrates how changing transaction data can be detected by recalculating and comparing the Merkle Root.

## Python Libraries

Exercise 1 uses Python standard libraries only:

```python
import hashlib
import pickle
import time
```

---

# Exercise 2 – Proof of Work: Mining, Difficulty and Probability

## Objective

Exercise 2 implements a simple Proof-of-Work miner using SHA-256.

The program repeatedly changes a nonce until the generated hash begins with the required number of leading zeros.

The following difficulty levels are tested:

- Difficulty 2
- Difficulty 3
- Difficulty 4
- Difficulty 5

For each difficulty level, the program mines **30 blocks**.

## Main Features

The implementation includes:

- `create_block()` – creates different block data for each mining test
- `mine_block()` – increments the nonce until a valid hash is found
- `run_experiment()` – mines 30 blocks for one difficulty level
- `calculate_metrics()` – calculates performance results
- `display_summary_table()` – prints the final comparison table

## Metrics Recorded

For each difficulty level, the program records and calculates:

- mining time
- valid hash
- nonce
- number of hash attempts
- average mining time
- minimum mining time
- maximum mining time
- standard deviation
- hashes per second
- average measured attempts
- theoretical expected attempts
- percentage difference

The theoretical expected number of attempts is:

```text
16 ^ difficulty
```

because each hexadecimal digit has 16 possible values.

## Experimental Results

| Difficulty | Average Time (s) | Measured Attempts | Theoretical Attempts |
|---|---:|---:|---:|
| 2 | 0.000426 | 245.53 | 256 |
| 3 | 0.006813 | 4,192.53 | 4,096 |
| 4 | 0.089421 | 64,065.03 | 65,536 |
| 5 | 1.234673 | 1,256,375.83 | 1,048,576 |

The results show that computational effort increases approximately exponentially as mining difficulty increases.

## Python Libraries

Exercise 2 uses:

```python
import hashlib
import pickle
import secrets
import statistics
import time
```

All of these are included in the Python standard library.

---

# Exercise 3 – Elliptic Curve Cryptography

## Objective

Exercise 3 demonstrates Elliptic Curve Digital Signature Algorithm (ECDSA) operations using the **secp256k1** curve.

The program:

- generates an ECDSA private/public key pair
- displays keys in PEM and hexadecimal form
- compares private and public key sizes
- compresses the public key
- calculates storage reduction
- reconstructs the compressed public key
- signs a short message
- verifies the signature using the reconstructed public key

## Main Results

Raw key sizes:

| Key Type | Size | Hex Characters |
|---|---:|---:|
| Private key | 32 bytes | 64 |
| Uncompressed public key | 65 bytes | 130 |
| Compressed public key | 33 bytes | 66 |

Public-key compression reduces the size from **65 bytes to 33 bytes**.

Storage reduction:

```text
((65 - 33) / 65) × 100 = 49.23%
```

## Public-Key Compression

The standard uncompressed public key contains:

```text
04 + X coordinate + Y coordinate
```

The compressed form contains:

```text
02 + X coordinate   # if Y is even
03 + X coordinate   # if Y is odd
```

Because the Y coordinate can be reconstructed from X and the parity prefix, the full public key does not need to be stored.

## Verification

The program reconstructs the compressed public key and checks that it matches the original uncompressed key.

Expected output:

```text
Decompression successful: True
```

The following message is signed:

```text
COMP842 Blockchain Security
```

The signature is then verified with the reconstructed public key.

Expected result:

```text
Signature Verification: VALID
```

## Python Library

Exercise 3 requires the `cryptography` package.

Install it with:

```bash
pip install cryptography
```

The main imports are:

```python
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.primitives import serialization, hashes
```

---

# How to Run

## Requirements

- Python 3.x
- `cryptography` package for Exercise 3

Check Python:

```bash
python --version
```

Install the required package:

```bash
pip install cryptography
```

## Run an Exercise

From the repository folder, run the relevant Python file.

Example:

```bash
python exercise1_blockchain.py
```

```bash
python exercise2_pow.py
```

```bash
python exercise3_ecc.py
```

If your filenames are different, replace the names above with the actual filenames in your repository.

---

# Notes

- Exercise 1 demonstrates blockchain integrity and tamper detection.
- Exercise 2 demonstrates the probabilistic and computational behaviour of Proof of Work.
- Exercise 3 demonstrates ECDSA key generation, public-key compression and digital signature verification.
- The private key generated in Exercise 3 is a temporary educational key created only for this assessment. It should not be reused for any real cryptocurrency wallet or production system.

---

# References

The implementation was developed with reference to the COMP842 course tutorials and assessment instructions provided by Auckland University of Technology.


