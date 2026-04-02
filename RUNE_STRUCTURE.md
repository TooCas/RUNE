# RUNE Decrypted Structure Example

This is what the JSONL inside a `.rune` file looks like after decryption.
Each line is a separate JSON object.

---

## Line 1: Header

```json
{
  "header": true,
  "format": "rune-v4.1",
  "schema_version": "4.1.0",
  "created_by": "claude-opus-4-6",
  "created_at": "2026-04-01T12:00:00Z",
  "owner": "Jane Example",
  "line_roles": {
    "line_1": "header",
    "line_2": "identity_kernel",
    "line_3_plus": "memory_ledger"
  },
  "scoring_spec": {
    "key_match": 4.5,
    "text_match": 3.0,
    "group_match": 2.2,
    "section_match": 1.7,
    "open_loop_bonus": 0.25
  },
  "encryption_spec": {
    "method": "sha256-xor-v1",
    "encoding": "base64"
  },
  "merge_policy": "append-only",
  "entry_count": 2
}
```

## Line 2: Identity Kernel

```json
{
  "identity_kernel": true,
  "version": 1,
  "who": {
    "name": "Jane Example",
    "location": "Vancouver, BC",
    "domains": ["machine learning", "data engineering"],
    "people": [{"name": "Alex", "relation": "co-founder"}],
    "hardware": ["MacBook Pro M4"],
    "tools": ["Python", "PyTorch", "VS Code"]
  },
  "how": {
    "directness": 0.9,
    "humor": 0.6,
    "depth": 0.85,
    "formality": 0.3,
    "never": ["talk down to me", "over-explain basics"],
    "always": ["give code examples", "be direct"]
  },
  "arc": ["ML pipeline optimization", "startup MVP", "investor pitch prep"],
  "beliefs": ["open-source-first", "ship-fast-iterate"],
  "relationship": {
    "trust": 0.8,
    "sessions": 12,
    "style": "technical-peer"
  }
}
```

## Lines 3+: Memory Entries

```json
{
  "id": "entry-001",
  "entry_version": 1,
  "type": "session",
  "source_model": "claude-opus-4-6",
  "session_id": "sess-2026-04-01",
  "created_at": "2026-04-01T14:30:00Z",
  "title": "ML pipeline refactor",
  "summary": "Refactored the data ingestion pipeline to use async processing. Replaced the synchronous CSV loader with an async Parquet reader, reducing startup time from 45 seconds to 8 seconds. Decided to use DuckDB for intermediate queries instead of Pandas. Jane wanted to keep the old loader as a fallback, so both paths are maintained behind a config flag.",
  "why_it_matters": "Core infrastructure change that affects every downstream model training job.",
  "entities": ["DuckDB", "Parquet", "Pandas"],
  "topics": ["data-pipeline", "performance", "refactoring"],
  "project": "ml-platform",
  "importance": 4,
  "confidence": 0.95,
  "open_loop": false,
  "supersedes": null,
  "integrity_hash": "a1b2c3d4e5f6..."
}
```

```json
{
  "id": "entry-002",
  "entry_version": 1,
  "type": "open_loop",
  "source_model": "claude-opus-4-6",
  "session_id": "sess-2026-04-01",
  "created_at": "2026-04-01T15:45:00Z",
  "title": "GPU memory issue on large batches",
  "summary": "Hit an OOM error when batch size exceeds 64 on the new pipeline. Tried gradient checkpointing but it slowed training by 40%. Need to investigate mixed precision training or model sharding as alternatives. Jane wants to benchmark both approaches before deciding.",
  "why_it_matters": "Blocking issue for training the production model at full scale.",
  "entities": ["PyTorch", "gradient-checkpointing", "mixed-precision"],
  "topics": ["GPU", "memory", "training"],
  "project": "ml-platform",
  "importance": 5,
  "confidence": 0.9,
  "open_loop": true,
  "supersedes": null,
  "integrity_hash": "f7e8d9c0b1a2..."
}
```
