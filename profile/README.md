# Helix

Helix is a production-oriented Ethereum Layer 2 rollup stack built for **performance, compatibility, and operational simplicity**.

It combines a customized execution layer, modular rollup services, and bridge infrastructure into one cohesive system that can be deployed, tested, and scaled with predictable behavior.

## What Makes Helix Stand Out

- **Ethereum-equivalent execution**
  - Designed for strong EVM compatibility and smoother migration of existing applications.

- **High-throughput architecture**
  - Built around efficient block production and batch sequencing pipelines.
  - `helix-reth` is optimized for high TPS rollup workloads and stable long-running operation.

- **Modern transaction support**
  - Batch encoding/decoding supports typed transactions including **EIP-1559 / EIP-2930 / EIP-4844**.

- **Flexible proof system**
  - `helix-prover` supports **SGX / SP1** proving paths (with native execution support in the stack).
  - Supports staged proving workflows for better performance and scalability.

- **Reliable cross-chain UX**
  - End-to-end bridge flow: **deposit -> verify -> claim** and **withdraw -> verify -> claim**.
  - Event-driven synchronization with reorg-aware processing.

- **Operator-friendly tooling**
  - Local full E2E scripts, Docker Compose long-run environment, and practical debugging surfaces.

## System Modules

### `helix-contracts`
Core L1/L2 smart contracts for rollup sequencing, proof verification, bridge operations, and Global Exit Root management.

### `helix-reth`
Customized execution node based on Reth:
- High TPS execution path for rollup scenarios
- Cancun-compatible behavior with Helix-specific protocol handling
- System transaction support required by Helix workflows

### `helix-client`
Rollup service layer:
- **Sequencer**: builds L2 blocks, assembles batches, handles force-batch logic, submits to L1
- **Aggregator**: tracks unverified ranges, requests proofs, submits verification transactions

### `helix-prover`
Proof generation service:
- Supports **SGX / SP1** proving backends
- API-driven integration with aggregator
- Designed for scalable proving pipelines

### `helix-bridge-service`
Cross-chain backend for bridge operations:
- Event synchronization and state indexing
- Merkle proof query services
- Claim lifecycle tracking (`ready_for_claim`, claimed, reorg rollback)

### `helix-bridge-ui`
Frontend interface for users to:
- Submit deposit/withdraw transactions via wallet
- Track transfer history and status
- Execute claim operations when proofs are ready

## Typical End-to-End Flow

1. User submits transaction/bridge action.
2. Sequencer produces L2 blocks and submits batches.
3. Aggregator coordinates proof generation and verification on L1.
4. Bridge service marks claim readiness and serves proof data.
5. User completes claim on destination chain.

Helix is built to deliver a practical path to high-performance rollup operation without sacrificing modularity, observability, or developer velocity.
