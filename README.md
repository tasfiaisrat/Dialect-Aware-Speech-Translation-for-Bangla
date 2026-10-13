# Dialect-Aware Speech Translation for Bangla

Code and notebooks for the work **"Dialect-Aware Speech Translation for Bangla: Acoustic Identification, Recognition and Cross-Dialectal Transfer"** (under review).

The pipeline takes dialectal Bangla speech and carries out four steps:

1. **Dialect identification:** XLS-R-300M classifies the utterance from audio alone.
2. **Speech recognition:** Whisper-small with LoRA adaptation transcribes it.
3. **Translation:** mBART-50 with target-dialect tokens translates the transcript into a variety the user chooses.
4. **Speech synthesis:** MMS-TTS produces the output speech.

If the utterance is already in the requested variety, it skips translation and goes straight to synthesis.

Supported varieties: **Standard Bangla, Chittagong, Mymensingh, Barishal, Sylhet and Noakhali**.


## Notebooks

| Notebook | Purpose | Paper section |
|---|---|---|
| `notebook-a-data-prep.ipynb` | Corpus construction, session-disjoint splits, shortcut probe | 3, 4.1 |
| `notebook-b-identification.ipynb` | XLS-R-300M dialect identification and tier comparison | 4.2 |
| `notebook-c-asr(Version1).ipynb` | Whisper-small (zero-shot and LoRA) recognition | 4.3 |
| `notebook-c-asr(Version2).ipynb.ipynb` | FastConformer baseline, bootstrap CIs, error analysis | 4.3 |
| `mbart-qpain.ipynb.ipynb` | mBART-50 cross-dialectal translation and tag ablation | 4.4 |
| `notebook-d-cascade-evaluation.ipynb` | End-to-end cascade evaluation | 4.5 |

Run them in order: **A → B → C1 → C2 → M → D**. Each notebook reads the outputs of the earlier ones.

## Environment

All notebooks were run on **Kaggle** with a single NVIDIA T4 GPU. Each notebook installs its own packages in its first cells. Translation scores use SacreBLEU (`tokenize="flores101"`) and chrF.

## Datasets

No new data was collected. The notebooks use these public corpora:

- **RegSpeech12**: [[link]](https://www.kaggle.com/datasets/mdrezuwanhassan/regspeech12)
- **Common Voice Bangla**: [https://commonvoice.mozilla.org/bn](https://www.kaggle.com/datasets/rithikdebnath548/bangla-common-voice-validated)
- **Vashantor**: [[link]](https://data.mendeley.com/datasets/bj5jgk878b/2)

Please follow each dataset's own license and terms of use.

## Notes
- `C(Version 1)` and `C(Version 2)` are the same notebook (C). Because the full run takes more than 12 hours, it was run and saved in two parts. The FastConformer install cell in C2 differs from the first version of the notebook. Kaggle moved to Python 3.13, so the original pinned NeMo release could no longer be installed and the cell now installs the current release.

## Contact

Tasfia Israt — tisrat99@gmail.com
