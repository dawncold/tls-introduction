---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
---

# TLS Introduction

---

# What is TLS?

<div grid="~ cols-2 gap-2">

<div>

* TLS is stand for Transport Layer Security
* It provides communication security
* SSL 3.0 -> TLS 1.0 -> TLS 1.1 -> TLS 1.2 -> TLS 1.3
* On the top of TCP
* Can be on UDP
</div>
<div>
    <img src="https://hpbn.co/assets/diagrams/9873c7441be06e0b53a006aac442696c.svg"/>
</div>

</div>

---

# What TLS provides?

* Encryption
* Authentication
* Integrity

---

# Encryption
* Symmetric vs. Asymmetric key
    * AES
    * RSA, ECDHE
* TLS use Asymmetric and Symmetric
    * Key exchange
    * Encrypt application data

---

# TLS handshake
<div grid="~ cols-2 gap-4">
<div>
    This is a RSA certificate TLS handshake
    <img src="https://hpbn.co/assets/diagrams/b83b75dbbf5b7e4be31c8000f91fc1a8.svg"/>
</div>

<div>

* suite [swiːt]
* ClientHello: **supported** TLS version, cipher suite, options
* ServerHello: **selected** TLS version, Cipher suite, etc
* ClientKeyExchange: client generated pre-master secret, **encrypt with server's public key**
* client and server use random and pre-master secret generate **symmetric secret**
* use **symmetric secret** encrypt application data
</div>
</div>

---

# TLS handshake: ECDHE

<div grid="~ cols-2 gap-2">
<div>
<img src="/serverkeyexchange.png"/>
</div>

<div>

* RSA weakness
    * Forward Secrecy
* ServerKeyExchange: 
    * select curve
    * generate ephemeral private key, s
    * calculate public key, sG
    * send to client
* ClientKeyExchange:
    * use selected curve
    * generate ephemeral private key, c
    * calculate public key, cG
    * send to server
* generated same pre-master secret, then generated symmetric key

</div>
</div>
---

# Example: Cipher suite

## TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

* Key exchange: ECDHE
* Certificate: RSA
* Symmetric algorithm: AES_128_GCM
    * encrypt algorithm: AES
    * length: 128
    * mode: GCM
* MAC: SHA256

---

# Authentication: Chain of Trust

<div grid="~ cols-2 gap-2">
<div>

* encrypt
* decrypt
* sign
* verify

</div>
<div>
<img src="https://hpbn.co/assets/diagrams/bb75b8bd469ce5b703b76abb7042e978.svg" />
</div>
</div>

---

# CRL and OCSP

<div grid="~ cols-2 gap-2">
<div>
<img src="/crl.png"/>
</div>
<div>
<img src="/ocsp.png"/>
</div>
</div>

* Certificate Revocation List (CRL)
* Online Certificate Status Protocol (OCSP)
* OCSP stapling

---

# Integrity

<div grid="~ cols-2 gap-2">
<div>
<img src="https://hpbn.co/assets/diagrams/4603275cd98c93aeb8c46b1b1afa0ba6.svg"/>
</div>
<div>

* Message Authentication Code(MAC)
* MAC algorithm being used is the built in MAC provided by the GCM AEAD encryption mode
</div>
</div>