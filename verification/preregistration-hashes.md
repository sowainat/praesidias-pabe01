# Preregistration Hash Verification

Run these locally against the files at the repository root. No network access required.

```
shasum -a 256 PABE-01-confirmatory-v1.0.md
```

Expected:

```
0e5ad607d671e5c8ed08fb86881fe622978705ae93bb5520efa4b579916a32f4
```

```
shasum -a 256 pabe-01-confirmatory-v1.0.json
```

Expected:

```
d7ed8c38a9f83bd6fbcc91360b7873d2fc6b9505ac3ecfbc9d00128bbc832cba
```

Both hashes above were independently recomputed against the frozen source files during preparation of this package and matched exactly.

## Why the confirmatory manifest is not re-published elsewhere in this repository

`pabe-01-confirmatory-v1.0.json` was committed to this repository, hash-committed, and OpenTimestamps-anchored before any confirmatory trial ran. It is not modified here. It contains a small number of local development-machine path strings from when it was generated (under a `phase8Boundary` field) — these reveal nothing beyond a local folder path and cannot be redacted without changing the file's bytes and invalidating the committed hash and timestamp above. [frozen-hashes.json](frozen-hashes.json) and [sensitive-annex-hashes.json](sensitive-annex-hashes.json) republish the same commitment as hash-only wrapper manifests (no local paths) for convenience.

## Related frozen hashes

| Artifact | SHA-256 |
|---|---|
| Preregistration document | `0e5ad607d671e5c8ed08fb86881fe622978705ae93bb5520efa4b579916a32f4` |
| Confirmatory experiment manifest | `d7ed8c38a9f83bd6fbcc91360b7873d2fc6b9505ac3ecfbc9d00128bbc832cba` |
| Condition-order file | `67475ae24af95c83ae6913a79e1f2f3822ad1f92118083726fe5ee2d7094135f` |
| Scenario v2 | `674455b94ffe5ece74566c3cf7ff6e51ac16f16bbfc86a36606c4706a21c1188` |
| Provider schema | `2421e4a09be22b8413ae616943b19b76198fa4944ab3daa9b63ef4801d7cfb64` |
| Primary model configuration | `43330e6f212450538e8a44234581338d2133aee0be6cda87542c5fcddbda010d` |
| Policy | `e479b196505b6d48603e90bf2c920c2f0e2e3bb036382ab7291d7d3a24082896` |

Machine-readable versions: [frozen-hashes.json](frozen-hashes.json).
