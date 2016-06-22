## 02 Grundlagen

#### Information security

* **Datensicherheit** Data security
  * Mit Datensicherheit wird der Schutz von Daten hinsichtlich gegebener Anforderungen an deren **Vertraulichkeit, Verfügbarkeit und Integrität** bezeichnet.

* **Datenschutz** Data protection and privacy
  * Datenschutz soll den Einzelnen davor schützen, dass er durch den Umgang mit seinen personenbezogenen Daten in seinem Persönlichkeitsrecht beeinträchtigt wird.

#### Security of ICT Systems

* Part of Information security
* **ICT** information and communication technology
  * **Computer security** Secure storage and processing of data
  * **Network security** Secure exchange of data

#### Schutzziele

|                 | Confidentiality | Integrity | Availability |
| --------------- | --- | --- | --- |
| Threats         | Eavesdropping | Modification, Interception, fake Information Source | Failure of Systems, intentional damage and overloading of resources |
| How to Protect  | Encryption, Information Hiding | Cryptographic checksum, Authentication and Digital signature | Resource Redundancy |

## 03 Terms

* Cryptology
  * Cryptology
  * Cryptanalysis
* Information Hiding
  * Steganography
  * Watermarking

## 04 Classical Cryptography

![](https://dl.dropboxusercontent.com/u/55616012/note/encryption.PNG)

* Symmetric crypto Systems
  * ke = kd
  * keys for n Partners : (n X (n - 1)) / 2
* Assymmetric crypto Systems
  * ke != kd
  * keys for n Partners : n

|                   | Substitution | Caesar      | Vigenère |
| ----------------- | ------------ | ----------- | -------- |
| Letter Frequency  | not changed  | not changed | changed  |
| (max) key length  | 1            | n           | n        |
| key sprace        | 25           | n!          | 26^n     |

* The basic Principles of Classical Cryptography
  * Substituion
    * Substituion
    * Monoalphabetic Substituion (e.g. Caesar)
    * Polyalphabetic Substituion (e.g. Vigenere)
  * Transposition
    * Columnar Transposition
* Information Theoretical Security
  * **Unconditional Security** *can not be broken with infinite computational resources*
    * Key length equal to Plantext
    * key stream is truely random
    * key stream is only used once
  * **Computational Security** *O(n) is very large and known*
  * **Relative Security**
* Strength of crypto Systems
  * **Diffusion** *by Transposition (permutaion)*
  * **Confusion** *by Substituion*

## 05 Symmetrical Cryptography

* Block cipher
  * Structure of block cipher

    ![](https://dl.dropboxusercontent.com/u/55616012/note/block_cipher-1.PNG)
  * Iterative Block cipher
    * Use the same round transformation in all rounds **except of initial or final round**

    ![](https://dl.dropboxusercontent.com/u/55616012/note/block_cipher-2.PNG)
  * Key-alternating block cipher
    * First round key is added before the first round
    * Last round key is added after the last round

    ![](https://dl.dropboxusercontent.com/u/55616012/note/block_cipher-3.PNG)
  * Modes of Operation
    * Electronic codebook (ECB)

    ![](https://dl.dropboxusercontent.com/u/55616012/note/block_cipher-4.PNG)
    * Cipher-Block chaing (CBC)

    ![](https://dl.dropboxusercontent.com/u/55616012/note/block_cipher-5.PNG)
* Stram cipher
  * Less popuar than block cipher
  * Often used in mobole appliacation
  * Generally require fewer resources
  * Encrypt faster than block cipher
* Random Number Generator
  * True Random Number Generator
  * General Pseudo Random Number Generator
  * Cryptographically Secure Pseudo Random Number Generator
* LSFR

  ![](https://dl.dropboxusercontent.com/u/55616012/note/lfsr.png)

* DES
  ![](https://dl.dropboxusercontent.com/u/55616012/note/des.png)
  ![](https://dl.dropboxusercontent.com/u/55616012/note/des_sbox.png)
* AES
  * Data Path
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/AES.svg)
  * Key Expansion
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/AES_key.svg)

## 07 Asymmetric Cryptography

* Kinds of Mathematical Functions
  * One-way function
  * Trapdoor function
* Diffie-Hellman Key Exchange
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/diffe.svg)
  * base on **discrete logarith problem**
  * Primitive root modulo p
    * if g^t for 0 ≤ t ≤ p-2 returns all values from 1 to p-1
* Station-to-Station Protocol
* RSA
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/RSA.svg)
  * base on **factorization problem**
  * multiplicative inverse
    * (e * d) mod n = 1
    * (m^e mod n)^d mod n = m^(e * d) mod n = m  
  * key generation
    1. select **n = p * q**
    2. generate **ϕ = (p - 1) * (q - 1)**
    3. select **(e, d)**, so that **(e * d) mod ϕ = 1**
  * Euclidean Algorithm
  * Extended Euclidean Algorithm
* EIGamal
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/EIGamal.svg)
  * base on Diffie-Hellman Key Exchange

## 08 Hybird Procedures
## 09 Hash Function

* Types of Hash Functions
  * Keyless **Modification Detection (MDC)**
    * One Way Hash Function (OWHF)
      * Preimage Resistance
      * 2nd Preimage Resistance
    * Collosion Resistant Hash Function (CRHF)
      * Collosion Resistance
  * Key-Dependent **Message Authentication (MAC)**
* Requirements
  * Preimage resistance
  * 2nd Preimage Resistance
  * Collosion Resistance
  * Non-correlation
  * Near-collision resistance
  * Partial-preimage resistance
* MD4
  * 3 auxiliary functions
    ```javascript
    // If X = 1, return  Y, else return Z
    var f = function (x, y, z) {
      return ( x == 1 ) ? y : Z;
    };
    // If at least 2 bits are set to 1, G returns 1, else 0
    var g = function (x, y, z) {
      return ( (x + y + z) >= 2 ) ? 1 : 0;
    };
    // x XOR y XOR z
    var h = function (x, y, z) {
      return x ^ y ^ z;
    }
    ```
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/MD4.svg)
  * "+" means here addition modulo 32 Bits
