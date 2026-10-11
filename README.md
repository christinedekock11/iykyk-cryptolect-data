# IYKYK: Cryptolect Annotations

Annotated data accompanying the paper:

**[IYKYK: Using language models to decode extremist cryptolects](https://arxiv.org/abs/2506.05635)**
Christine de Kock, Arij Riabi, Zeerak Talat, Michael Sejr Schlichtkrull, Pranava Madhyastha, Eduard Hovy

📄 Paper on Hugging Face: https://huggingface.co/papers/2506.05635

## Content warning

This dataset is drawn from extremist online communities. The target words and model-generated definitions below reference misogynistic, racist, antisemitic and otherwise hateful ideation, including references to real perpetrators of mass violence. It is released to support research on extremist language and automated moderation.

## What's here

This repo contains the **word-level annotations** used for Tasks 1–3 in the paper: expert judgements on whether a candidate term is in-group ("cryptolect") vocabulary for a community, and human-rated model-generated definitions for those terms.

It does **not** include the underlying raw corpus (19.4M posts) or verbatim forum post text used as context during annotation. That corpus is subject to a controlled-access policy under the paper's ethics approval and is available to verified researchers on request (see the paper's Ethics Statement) — the files here contain only target words and annotation labels.

## Communities

- `incels_*` — incels.is (the "incel" / involuntary celibate community)
- `strf_*` — Stormfront (white supremacist forum)

## Files & schema

### `incels_task1_2.json`, `strf_task1_2.json`

Used for **Task 1** (in-group term classification) and **Task 2** (in-context retrieval of in-group terms). One record per candidate term:

```json
{
  "word": "brenton",
  "label": true
}
```

- `word` — candidate term.
- `label` (bool) — whether `word` is valid in-group/cryptolect language for the community. Valid terms include lexical innovations, dogwhistles, linguistic imports/exports, and community-significant names; invalid (`false`) terms include standard language, generic internet slang, spelling errors, non-English text, and usernames.

### `incels_task3.json`, `strf_task3.json`

Used for **Task 3** (definition decoding). One record per target word, with model-generated definitions from four prompting conditions, each paired with a human expert rating:

```json
{
  "word": "wagecel",
  "instructions": ["<model-generated definition>", "correct"],
  "1-example": ["<model-generated definition>", "partial"],
  "10-example": ["<model-generated definition>", "partial"],
  "definition": ["<model-generated definition>", "correct"]
}
```

- `instructions`, `1-example`, `10-example`, `definition` — each a 2-element `[generated_definition, human_rating]` pair, corresponding to a prompting condition evaluated in the paper for definition generation (zero-shot instructions, 1-shot example, 10-shot example, and dictionary-style definition prompting respectively — see the paper for exact prompt templates).
- `human_rating` ∈ `"correct"`, `"partial"`, `"wrong"`, `"NA"` (no answer produced/ratable).

## Citation

```bibtex
@article{dekock2025iykyk,
  title   = {IYKYK: Using language models to decode extremist cryptolects},
  author  = {de Kock, Christine and Riabi, Arij and Talat, Zeerak and Schlichtkrull, Michael Sejr and Madhyastha, Pranava and Hovy, Eduard},
  journal = {arXiv preprint arXiv:2506.05635},
  year    = {2025}
}
```

## License

Released under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), matching the paper's license.
