# XAL - eXplainable Assembly Language

**Cryptographically verifiable AI execution format with per-instruction Ed25519 signatures, TPM 2.0 hardware attestation, and constitutional halts.**

## Background

XAL was developed as part of Aevion LLC's verifiable AI infrastructure, protected by **US Patent 63/896,282** ("System and Method for Proof-Native Compliance Automation"), filed Oct 9, 2025.

Published as an open standard under **CC-BY-4.0** to maximize adoption across government and industry.

XAL is a low-level execution language for AI systems that produces **court-admissible proof bundles**. Each AI decision generates a tamper-evident audit trail that can be verified without re-executing the AI.

## Core Features

| Feature | Description |
|---------|-------------|
| **Per-Instruction Signatures** | Every instruction signed with Ed25519 |
| **Hardware Attestation** | TPM 2.0 quote binding execution to silicon root of trust |
| **Merkle Tree Commit** | Cryptographic commitment to execution history |
| **Constitutional Halt** | Automatic halt when model disagreement exceeds threshold |
| **Effect Types** | Compile-time tracking of AI capabilities used |

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
  "verification": {
    "method": "Ed25519",
    "verified_receipts": 23,
    "verified": true
  }
}
```

## Verification

```python
from xal_verify import verify_bundle

result = verify_bundle(bundle)
print(f"Valid: {result.bundle_valid}")
print(f"Signatures: {result.signatures_valid}")
print(f"Merkle: {result.merkle_valid}")
```

## Use Cases

- **Veterans Affairs**: M21-1 adjudication with immutable audit trails
- **Elections**: VVSG 2.0 software-independent verification
- **Healthcare**: DSCSA pharmaceutical transaction history
- **Financial Services**: Model governance and regulatory compliance

## Specification

See [SPEC.md](SPEC.md) for the full XAL instruction set and type system.

## License

**CC-BY-4.0** - This specification is an open standard. Implementations may use it freely.

See [PATENTS.md](PATENTS.md) for patent licensing terms.

## Resources

- [Proof Bundle Example](examples/grant_proposal_bundle.json)
- [XAL Interpreter](aevion/xal/interpreter.py)
- [Verification Tools](aevion/xal/xal_verify.py)
