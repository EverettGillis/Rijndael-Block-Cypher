# Rijndael Block Cypher

**About**
\
\
Visualize encryption with AES implementation in python. 

\
**Introduction**
\
\
The Advanced Encryption Standard (AES) established in FIPS 197 includes specific bit length variants of the Rijndael block cypher (NIST 2001). Here, a python implementation of this method uses ~1500 lines of code to accurately model what is today the standard of encryption in use by the U.S. government (Smid 2021).

\
**Algorithm Overview**
\
\
On a high level, AES-128 takes two-dimensional cyphertext and cypherkey arrays of $Nb=4$ rows of 32 bits. Cyphertext constituting the **state** is combined with the cypherkey before subsequent rounds of substitution and permutation scramble the state and key expansion extends the length of the cypherkey. Each of $Nr=10$ rounds generally sees the same procedures performed on the state:

- SubBytes (substitution):\
Bytes of the state are mapped to values according to a mathematical function. These values are more simply determined with a lookup table (```S_box```).

- ShiftRows (permutation):\
Performs a cyclic shift of the elements in each row of the state by increasing intervals.

- MixColumns (permutation):\
Each state column constituting a **word** of 32 bits is multiplied with a constant vector. A finite field $GF(2^{8})$ restricts the number of elements produced in this multiplication, which is necessary to maintain the magnitdue of information in the state.

- AddRoundKey:\
XORs the state with the last block of the key schedule, a product of key expansion.

MixColumns is not performed in the last round of encrpytion as it adds little additional security there. The inverse cypher sees the above operations generally performed in reverse order, with the constant vector in MixColumns being the inverse matrix of that used in encryption. In cypher block chaining (CBC) mode, blocks of data are procedurally encrypted to generate cypherkeys for subsequent block encryption, and the inverse is performed in decryption.

Detailed mathematical preliminaries and other specifications may be found in NIST (2001) and Wikipedia (2023).

\
**Operation and Intended Use**
\
\
```AES_program_manager.py``` is the interface through which both encryption and decryption files are run. Save all three files to the same folder. Required: Python 3.10, numpy 1.22.3, tkinter 0.1.0.

```algorithm_validation.pdf``` demonstrates the efficacy of the implementation in accurately and reliably encrypting and decrypting data.

This implementation is designed to illustrate the process of encryption in real time, not to perform it quickly and securely. Encryption in professional use is performed in isolation where it is time efficient and less vulnerable to timing and sidechannel attacks.

\
**Citations**
\
\
National Institute of Standards and Technology (2001) Advanced Encryption Standard (AES). J Fed Info Proc Stan Pub 197. https://doi.org/10.6028/NIST.FIPS.197.

Smid, M.E. (2021) Development of the Advanced Encryption Standard. J Res Natl Inst Stan 126:126024. https://doi.org/10.6028/jres.126.024.

Wikipedia (2023) Advanced Encryption Standard. https://en.wikipedia.org/wiki/Advanced_Encryption_Standard.
