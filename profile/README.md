<p align="center">
  <img src="./assets/helix-icon-v4-chip.svg" alt="Helix" width="140" />
</p>

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

## How Helix Compares

| Dimension | Optimistic Rollups | Polygon zkEVM-style Stack | Helix |
|---|---|---|---|
| EVM equivalence | Typically not positioned as Type 1 | zkEVM compatibility with zk-driven constraints | **Type 1 EVM target (execution-equivalent path)** |
| Finality model | Fraud-proof challenge window | ZK proof verification | **Fast verification pipeline with SGX/SP1 options** |
| Throughput architecture | Good, but challenge model tradeoffs | Good, often prover-bound in practice | **High-TPS execution path + modular proving** |
| Proof strategy flexibility | Fraud-proof model | Primarily zk proving | **Multi-path proving: SGX + SP1 (zk proving path)** |
| Developer/Operator workflow | Mature but fragmented across stacks | Powerful but heavy zk operational surface | **One-command local deployment + E2E + Docker long-run workflow** |

Helix is built for teams that want **Type 1 EVM-level compatibility**, **high throughput**, and **proof-system flexibility** without being locked into a single proving path.
