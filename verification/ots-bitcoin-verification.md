# OpenTimestamps / Bitcoin Verification

## Chronology

| Event | Timestamp |
|---|---|
| Public preregistration commit (`7edc8b0`) | 2026-08-31T07:27:45Z |
| OpenTimestamps Bitcoin attestation | 2026-08-31T07:46:57Z |
| First confirmatory trial (C01) started | 2026-08-31T08:50:02.453Z |

The preregistration document was committed to this public repository, and its OpenTimestamps proof achieved Bitcoin attestation, both **before** the first confirmatory trial began. The preregistration was frozen ahead of confirmatory testing, not after it.

## Bitcoin attestation

- Result: `BITCOIN_ATTESTATION_VERIFIED`
- Target file: `PABE-01-confirmatory-v1.0.md`, SHA-256 `0e5ad607d671e5c8ed08fb86881fe622978705ae93bb5520efa4b579916a32f4`
- Block height: `964846`
- Block hash: `0000000000000000000234c97a0225edbb6a66b3a63e6ae88f3932318dd4004e`
- Block timestamp: `2026-08-31T07:46:57.000Z`
- Confirmations at verification time: `6`

Verification was performed by upgrading the OpenTimestamps receipt, parsing the resulting `BitcoinBlockHeaderAttestation`, independently fetching the raw block header from two unrelated public sources (blockstream.info and mempool.space), locally recomputing the block hash via double-SHA256 of that header, and confirming the OTS receipt's Merkle root matches the block's Merkle root from both sources. Both public sources agreed on the block hash, header bytes, Merkle root, and best-chain status. Full raw verification record: [ots-bitcoin-finality-raw.json](ots-bitcoin-finality-raw.json).

## What this does and does not prove

An OpenTimestamps Bitcoin attestation proves that the exact byte content of `PABE-01-confirmatory-v1.0.md` existed no later than the timestamp of block 964846, and that this commitment is independently checkable against the public Bitcoin blockchain by anyone, indefinitely. It does not prove anything about the correctness of the document's contents, and it does not by itself prove that no later document with the same filename was substituted — that assurance comes from combining the OTS proof with the SHA-256 hash check in [preregistration-hashes.md](preregistration-hashes.md) and the Git commit history of this repository.

## A note on the published `.ots` file

The `.ots` file currently committed at the repository root (`PABE-01-confirmatory-v1.0.md.ots`) is the pending-calendar receipt created at commit time, before the Bitcoin attestation above was confirmed. It is a valid OpenTimestamps proof, but a fully self-contained, calendar-independent version that embeds the completed Bitcoin Merkle path (as verified above) exists only in the private experiment record and was not substituted into this already-committed file, to avoid altering a file whose hash is part of the public, timestamped commitment chain. Re-running `ots upgrade` against the published `.ots` file, or querying the calendar servers named in the receipt, will complete the same verification shown here.
