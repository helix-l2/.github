# Helix

Helix is an Ethereum-equivalent L2 rollup stack focused on **high throughput**, **modular architecture**, and **production-ready operations**.

## Highlights

- High-TPS execution path with `helix-reth`
- Typed transaction support: **EIP-1559 / 2930 / 4844**
- Flexible proving with **SGX / SP1**
- End-to-end bridge flow: **deposit / withdraw / verify / claim**
- Local E2E and Docker-based long-run operations

## Architecture

```mermaid
flowchart LR
  U[Users / Apps / Wallets]

  subgraph L2[Helix L2]
    R[helix-reth\nExecution Node]
    S[helix-client Sequencer\nBlock + Batch]
    A[helix-client Aggregator\nProof Coordination]
    P[helix-prover\nSGX / SP1]
    B[helix-bridge-service\nProof + Claim State]
    UI[helix-bridge-ui]
  end

  subgraph L1[Ethereum L1]
    C[helix-contracts\nRollup + Bridge + Verifiers]
  end

  U --> UI
  UI --> B
  U --> R
  S --> R
  S --> C
  A --> P
  A --> C
  B <--> C
  B --> UI
```

## Core Repositories

- `helix-contracts`
- `helix-reth`
- `helix-client`
- `helix-prover`
- `helix-bridge-service`
- `helix-bridge-ui`
