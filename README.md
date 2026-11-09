# diktier-models

Model artifacts for Diktier, a private local push-to-talk dictation tool (its repository is not public).
The files are published only as **immutable GitHub releases**. Diktier downloads them from the release URLs
recorded in its manifest (`src/models.toml`) and verifies size and SHA-256 of every file.

## Releases

| Tag | Model key | Content |
|---|---|---|
| `model-parakeet-ultra-0.6b-int8-pc-r1` | `parakeet-ultra-0.6b-int8-pc` | Parakeet Ultra (Moondream, based on NVIDIA parakeet-tdt-0.6b-v3), ONNX, int8 per-channel quantized |

Each release contains the runtime files, `NOTICE-parakeet-ultra.md` (provenance, license, changes) and
`SHA256SUMS`. Check after downloading:

```bash
sha256sum -c SHA256SUMS
```

## Provenance and reproduction

NVIDIA `parakeet-tdt-0.6b-v3` → Moondream `parakeet-ultra` (post-training) → ONNX export
`altunenes/parakeet-rs` (revision `4d2a8bc71f5c896ec40faa59732e6716295edaf2`, without the VAD head) →
int8 per-channel quantization with
[`scripts/quantize-ultra.py`](scripts/quantize-ultra.py), which reproduces the files bit-for-bit. The pinned
Python environment is [`scripts/quantize-ultra.requirements.txt`](scripts/quantize-ultra.requirements.txt).
Both files are byte-identical copies from Diktier commit `f6ae94f1bfec55a692f4a4bdf6e473390d3a5ccd`; their
comments mention paths of the Diktier repository (`docs/…`, `models\spike\…`) that do not exist here.
The `NOTICE-parakeet-ultra.md` inside release `r1` is immutable and still links to the now private
Diktier repository; the copy in this repository is current. Details: [NOTICE-parakeet-ultra.md](NOTICE-parakeet-ultra.md).

## License

The model files are licensed under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/), like their sources.
Attribution and the list of changes are in [NOTICE-parakeet-ultra.md](NOTICE-parakeet-ultra.md).
This repository is not affiliated with or endorsed by NVIDIA, Moondream or the author of the ONNX export.
