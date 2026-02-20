# XAL - eXplainable Assembly Language

**Implementation of US Patent 63/896,282: "System and Method for Proof-Native Compliance Automation"**

XAL is a low-level execution language for AI systems that produces **court-admissible proof bundles**. Each AI decision generates a tamper-evident audit trail that can be verified without re-executing the AI.

## Patent Alignment

This specification implements the core claims of **US Patent 63/896,282** (filed Oct 9, 2025):

| Patent Layer | XAL Implementation |
|--------------|-------------------|
| **Layer 1: Self-Verification** | Effect types track AI capabilities (`!RemoteInference`, `!Regulatory`) |
| **Layer 2: Cryptographic Signing** | Per-instruction Ed25519 signatures + TPM 2.0 attestation |
| **Layer 3: Temporal Chain** | Merkle tree commitment of execution history |
| **Layer 4: Blockchain Anchoring** | Merkle root ready for on-chain anchoring |

## Core Features

| Feature | Description | Patent Claim |
|---------|-------------|--------------|
| **Per-Instruction Signatures** | Every instruction signed with Ed25519 | Layer 2 |
| **Hardware Attestation** | TPM 2.0 quote binding to silicon root of trust | Layer 2 |
| **Merkle Tree Commit** | Cryptographic commitment to execution history | Layer 3 |
| **Constitutional Halt** | Automatic halt when model disagreement exceeds threshold | Layer 1 |
| **Effect Types** | Compile-time tracking of AI capabilities used | Layer 1 |
| **Multi-Model Consensus** | N-of-M voting with variance-based halt | Layer 1 |

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    XAL Execution Model                      │
├─────────────────────────────────────────────────────────────┤
│  Layer 1: Self-Verification                                 │
│  ├── Effect type checking (!RemoteInference, !Regulatory)  │
│  ├── Constitutional halt (.halt_if variance > threshold)   │
│  └── Regulatory compliance (.check M21-1-R001)             │
├─────────────────────────────────────────────────────────────┤
│  Layer 2: Cryptographic Signing                             │
│  ├── Per-instruction Ed25519 signatures                    │
│  ├── TPM 2.0 hardware attestation                          │
│  └── Public key ledger for verification                   │
├─────────────────────────────────────────────────────────────┤
│  Layer 3: Temporal Verification                             │
│  ├── Merkle tree of all instructions                       │
│  ├── Hash chain with parent references                     │
│  └── Execution receipt bundle                              │
├─────────────────────────────────────────────────────────────┤
│  Layer 4: Blockchain Anchoring                              │
│  ├── Merkle root for on-chain anchoring                   │
│  └── Batch verification support                            │
└─────────────────────────────────────────────────────────────┘
```

## Quick Example: VA Claims Processing

```json
{
  "bundle_id": "XAL-20260219-001",
  "claim_id": "CLM-2026-001",
  "merkle_root": "418107a35f3e367676f8fdbf9478d995a9727eebbe480ffdd323757d740bbd11",
  "effects_used": [
    "!RemoteInference",
    "!TPMQuote",
    "!ConstitutionalHalt{on_variance=0.15}",
    "!Consensus{N,M}",
    "!Regulatory"
  ],
  "hardware_attestation": {
    "silicon_id": "AEVION-TPM-2026-001",
    "tpm_quote": "b547bffb65294e15c4db745e3b01d0ab06bf43bd...",
    "attestation_type": "TPM2.0"
  },
  "constitutional_halt": {
    "votes": [0.92, 0.88, 0.95],
    "variance": 0.07,
    "threshold": 0.15,
    "halted": false
  },
  "verification": {
    "method": "Ed25519",
    "verified_receipts": 23,
    "verified": true
  }
}
```

## Use Cases

- **Veterans Affairs**: M21-1 adjudication with immutable audit trails
- **Elections**: VVSG 2.0 software-independent verification
- **Healthcare**: DSCSA pharmaceutical transaction history
- **Financial Services**: Model governance and regulatory compliance
- **Defense**: AI decision auditability for DoD acquisitions

## Specification

See [SPEC.md](SPEC.md) for the full XAL instruction set and type system.

## License

**CC-BY-4.0** - This specification is an open standard. Implementations may use it freely.

See [PATENTS.md](PATENTS.md) for patent licensing terms.

## Resources

- [Proof Bundle Example](grant_proposal_bundle.json)
- [XAL Interpreter](aevion/xal/interpreter.py)
- [Verification Tools](aevion/xal/xal_verify.py)

## Patent References

- US 63/896,282 - System and Method for Proof-Native Compliance Automation (Filed Oct 9, 2025)
