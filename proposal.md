# Proposal: Proof-only Transaction Type

## Proposal Overview

This proposal introduces a new transaction type called "**proof-only transaction**" on StarkNet/Madara. The key feature of this transaction type is that it contains only the zk-STARK proof of the transaction, without any specific transaction details. Here’s a detailed breakdown of the proposal:

### Background and Current State

- In the current StarkNet/Madara architecture, user-submitted L2 transactions are processed and executed by a Sequencer, followed by a Prover generating proofs for the batch of transactions.
- While this architecture enhances network scalability, **the transaction contents and execution traces are visible on L2**, lacking complete zero-knowledge privacy.

### Proposal Details

- Introduce the new "**proof-only transaction**" type, where users generate their own zk-STARK proof for their transactions and submit this proof as a proof-only transaction to the Sequencer.
- Upon receiving this transaction, the Sequencer does not need to understand the specific details of the transaction but includes it as a proof in the current transaction batch.

### Advantages and Objectives

- **Privacy Protection**: Proof-only transactions provide full privacy, keeping the specifics of the transactions hidden from others.
- **Ecosystem Growth**: App chains built on Madara can utilize this transaction type to develop more privacy-focused applications, thereby expanding StarkNet's ecosystem.
- **Technical Advantage**: Compared to other general L2 frameworks (like OP Stack), Madara's support for privacy policy can become a significant advantage.

We believe that privacy-centric infrastructure is a crucial future direction for Madara, and this new transaction type aligns with StarkNet’s innovative and forward-thinking philosophy of "keep StarkNet strange". We think proof-only transactions are sufficiently "strange".

### Summary

Generating zk-STARK proofs is currently expensive, but as the ZK technology improves, it's likely to become less costly. 

In essence, this proposal seeks to boost the privacy features of StarkNet/Madara by incorporating proof-only transactions, which will enrich the ecosystem with new technical benefits and innovative features.

## Milestone

The PoC phase aims to experiment with the feasibility of this idea, focusing initially on technical implementation and functionality verification rather than performance and cost. Development and experimentation will be centered around **Madara**, divided into the following phases:

### PoC Phase 1: Mini-Prover generates transaction proof

- **Objective**: Adapt [stone prover](https://github.com/starkware-libs/stone-prover) to support generating proofs for individual transactions.
- **Challenge**: Although relatively simple, it is crucial to ensure the generated proof is correct and valid.

### PoC Phase 2: Madara verifies proof-only transactions

- **Objective**: Design and implement a mechanism for Madara to verify proof-only transactions. This stage involves designing underlying blockchain protocols, which is challenging, but we are confident in our experience in designing public chain protocols.
- **Challenges**:
    - Determine whether users need to provide additional information besides the transaction proof
	    - Determine the specific transaction content Madara needs to verify
    - Design strategies to prevent DoS attacks
    - Design the transaction structure for proof-only transactions
    - Design the batch structure after including proof-only transactions
    - Modify the transaction verification process accordingly

### PoC Phase 3: Madara includes proof-only transactions into batch

- **Objective**: Implement the process of integrating proof-only transactions into the batch.
- **Challenge**: Due to changes in the batch structure, it is necessary to adjust the interface between Madara and the Prover to ensure correct data transmission and processing.

### PoC Phase 4: Prover generates proof for batch

- **Objective**: Implement the Prover to generate proofs for batches containing both regular and proof-only transactions.
- **Challenge**: Significant modifications to the Prover are needed to accommodate the new batch structure and processing requirements, involving intricate zero-knowledge proof technical details and implementation challenges. @zeroqn, with extensive experience in zero-knowledge proofs, will primarily handle this phase.

### PoC Phase 5: Solidity Verifier verifies proof for batch

- **Objective**: Implement the Solidity Verifier to verify the entire batch's proof.
- **Challenge**: While minimal changes are anticipated for this stage, it remains crucial to ensure the Solidity Verifier can effectively verify the new batch structure’s proof and maintain consistent interaction with Ethereum smart contracts.
