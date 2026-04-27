# V2V-Authentication-framework-ITS
# Formal Verification of CAT and CLAT Authentication Protocols for Secure Intelligent Transportation Systems(ITS)

This repository contains the Scyther/SPDL models for the authentication protocols designed for ITS:

**"Secure and Privacy-Aware Vehicular Authentication Scheme Using Trusted Execution Environments for ITS"**

---

## Overview

This work proposes two secure authentication protocols for Vehicle-to-Vehicle (V2V) communication in Intelligent Transportation Systems (ITS):

- CAT – Certificate-based Authentication Protocol for Post-Quantum V2V with Trusted Execution Environment 
- CLAT – Certificateless Authentication Protocol for Post-Quantum V2V with Trusted Execution Environment

Both protocols:
- Integrate post-quantum cryptography
- Use Trusted Execution Environments (TEE) for secure key protection
- Are formally verified using the Scyther tool

The goal is to achieve secure, privacy-preserving, and scalable authentication under both classical and quantum-capable adversaries.

---

## Key Features

- Mutual Authentication between vehicles  
- Secure Session Key Establishment (Hybrid PQ + Classical)  
- Forward Secrecy  
- Replay Attack Resistance  
- Privacy Preservation via Pseudonyms  
- Hardware-assisted security using TEE  
- Reduced communication overhead (CLAT improves efficiency over CAT)


---

## System Model

The protocols operate in an ITS environment with the following entities:

- Vehicle (V) with On-Board Unit (OBU) and TEE  
- Trusted Authority (TA/CA) for CAT
- Key Generation Centre (KGC) for CLAT 

All critical cryptographic operations (key generation, signing, KEM, HKDF) are executed inside the TEE, ensuring protection against software-level attacks.

---

## Threat Model

The protocols are analyzed under a combined Dolev-Yao (DY) and CK adversary model, where the attacker can:

- Intercept, modify, and replay messages  
- Perform impersonation and MITM attacks  
- Control the communication channel  

However:
- Cryptographic primitives are assumed secure  
- Secrets inside TEE remain protected  

---

## Repository Structure


CAT/
├── CAT_protocol.spdl
├── CAT_claims.spdl
└── CAT_scenario.spdl

CLAT/
├── CLAT_protocol.spdl
├── CLAT_claims.spdl
└── CLAT_scenario.spdl

results/
├── CAT_results.txt
└── CLAT_results.txt


---

## Tool & Environment

- Tool: Scyther v1.1.3  
- Language: SPDL (Security Protocol Description Language)  
- Verification Model: Symbolic analysis under Dolev-Yao  

Experimental setup:
- AMD Ryzen 7 processor  
- 16 GB RAM  
- Windows 11  

---

## How to Run

1. Install Scyther  
2. Run the following commands:

```bash
scyther CAT_protocol.spdl
scyther CLAT_protocol.spdl
The tool verifies all security claims automatically.
Security Properties Verified

The following claims are formally validated using Scyther:

-Alive
-Secrecy of session keys and long-term keys
-Non-injective agreement (Niagree)
-Non-injective synchronization (Nisynch)
-Weak agreement
-Commitment
-Forward secrecy
-Key confirmation
-Replay protection
-Privacy and non-traceability

✔ No attacks were found for any claims during verification.

## Formal Verification Summary

Both CAT and CLAT protocols:

- Successfully satisfy all defined security claims- Resist replay, impersonation, and MITM attacks
- Maintain confidentiality and authentication guarantees
- Ensure secure key derivation and agreement
- CLAT protocol additionally eliminates certificate overhead and improves scalability

## Protocol Highlights
- CAT Protocol
Certificate-based authentication via CA
Uses hybrid PQ cryptography (Kyber + Dilithium)
Provides strong accountability
- CLAT Protocol
Certificateless design using KGC + local secrets
Prevents key escrow using TEE
Offers better scalability and efficiency

## Notes on Modelling
- Cryptographic primitives are modelled symbolically
- TEE is abstracted as a trusted oracle
- Nonces and timestamps ensure freshness
- AEAD ensures integrity and confidentiality
