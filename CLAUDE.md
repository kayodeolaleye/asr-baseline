# asr-baseline — Working Agreement

## What this repo is
Minimal end-to-end ASR pipeline: ingest → preprocess → finetune → evaluate → quantize → serve.
One command runs the Spine on FLEURS Yoruba (whisper-tiny) and prints a WER number.
Success = a working loop and a baseline WER. Not a good WER.

## Zones — governs all code here
COLD (assistant writes freely): Dockerfiles, CI YAML, argparse, logging, config loading,
I/O, HF Trainer setup, dataloader wrapping, test scaffolding, glue.

HOT — the Core, typed by hand:
1. src/spine/preprocess.py — feature extraction, tokenization, collation, padding, attention masks
2. src/spine/evaluate.py — WER/CER alignment computation
3. src/spine/quantize.py — layer selection and precision choice

Cycle 1 is the only cycle where the assistant writes Core reference implementations.
From cycle 2 the Core is marked `# CORE` and left empty. Never filled. Never copied across repos.

## Adaptation rule
New corpus / sample rate / manifest format / script: predict what breaks and why,
name the assumptions that no longer hold, stop. Do not produce corrected code.

## Debugging
First response to a break is a question about what has already been checked. Never a diagnosis.

## Review
Nothing merges unread. Branch per unit of work, atomic commits, PR before merge.

## Constraints
CPU-only (Latitude 7420, i7). GPU on Kaggle, 12h cap, always checkpoint. Zero budget.

## Conventions
Python 3.11, .venv, pinned requirements.txt.
Audio is 16 kHz mono float32 everywhere, no exceptions.
artifacts/ is gitignored — models live on HF Hub, not in git history.
Configs are YAML in configs/. No hardcoded paths.

## Vocabulary
"Spine" = the pipeline (src/spine/). "Baseline" = the cycle 1 WER number. Never interchangeable.
