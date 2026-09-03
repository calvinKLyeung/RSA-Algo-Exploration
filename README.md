# RSA Algorithm Exploration and Implementation

A from-scratch implementation of RSA in Python, built to understand the number theory behind it. No cryptography libraries used.

Everything lives in a single notebook: [`ImplementingRSAAlgorithm.ipynb`](ImplementingRSAAlgorithm.ipynb).

## What's inside

**Toolset**: text to Unicode conversion (and back), decimal to binary expansion, fast modular exponentiation (FME), Euclidean and Extended Euclidean algorithms, primality checks (trial division and Fermat's Little Theorem), random prime pair generation, public key `e` and private key `d` derivation.

**Encode / Decode**: `Encode(n, e, message)` converts each character to its Unicode value and raises it to `e mod n`. `Decode(n, d, cipher_text)` reverses it with the private key. A worked demo walks through key generation, encryption, and decryption step by step.

**Message exchange**: real ciphertexts exchanged with classmates, encoded and decoded with the functions above.

**FME comparison**: three FME implementations (a while-loop version, a textbook binary-string version, and a lookup-table version) timed against naive `b**n % m` and `pow(b, n) % m`. The while-loop version is used throughout, since it has the fewest moving parts, uses the least memory, and runs fastest.

**Code breaking**: because this implementation encrypts one character at a time with small keys, it is breakable. Two attacks are demonstrated:

1. Factoring `n`. Brute-force the smaller prime factor, divide out the larger, recompute `d` with the Extended Euclidean Algorithm, then decrypt. Worked through on 4, 6, 8, and 12 digit `n`, with timings showing how cost grows with key size.
2. Cipher-to-glyph dictionary. With no padding or chunking, encrypting the printable ASCII set under the public key produces a lookup table that decrypts any message without ever recovering `d`.

**Custom additions**: an even-skipping brute-force factorizer, Fermat's factorization method (no speedup here), Pollard's rho (large speedup), and the glyph dictionary attack above.

## Running it

Python 3.12 with Jupyter. Only the standard library (`math`, `secrets`) is used.

```
jupyter notebook ImplementingRSAAlgorithm.ipynb
```

## Note

This is educational code. The keys are small, messages are encrypted character by character, and there is no padding. It is deliberately breakable and should never be used for anything real.
