# TriCoME: A Trimodal Dataset for Context-Aware Micro-Expression Recognition

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC_BY--NC_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

TriCoME is an in-the-wild micro-expression dataset built from publicly available recordings of Werewolf social deduction games. It pairs facial micro-expressions with audio and manually transcribed text from the concurrent utterance and preceding conversational context. Context annotations distinguish an interlocutor's utterance from the target speaker's own preceding statement.

The dataset supports the study of subtle facial behavior within conversations, using visual, acoustic, and textual information together with annotations of conversational roles.

This repository documents the dataset introduced in:

> **Trimodal Context-Aware Micro-Expression Recognition in Real-World Conversations: A Dataset and a Hierarchical Fusion Network**  
> Junbo Wang, Yan Zhao, Shigang Wang, Jian Wei, Qiming Zhang, and Yu Wu.

**Availability:** The annotation package will be made available upon request after acceptance of the manuscript. It will be provided following review of a signed access acknowledgment form. See [Data Access](#data-access) for the application procedure.

## Overview

| Item | Description |
| --- | --- |
| Recognition benchmark | 191 micro-expression samples |
| Subjects in the recognition benchmark | 16 |
| Source recordings | Seven publicly available online Werewolf matches |
| Recognition categories | Positive: 56; Negative: 37; Surprise: 98 |
| Additional annotated samples | Eight `others` samples, excluded from the recognition experiments |
| Modalities | Visual information, utterance audio, and manually transcribed text |
| Context roles | Interlocutor utterance and self-statement |
| Current-utterance audio segments | 191 |
| Preceding-context audio segments | 223: 108 interlocutor segments and 115 self-statement segments |
| Text annotation | One manually transcribed text segment per audio segment |
| Source video frame rate | Approximately 30 fps, retaining the native frame rate of the web recordings |
| Micro-expression duration criterion | No more than 500 ms |
| Facial annotation | Independent annotation by two FACS-certified coders |
| Action-unit agreement | 0.89, measured by action-unit set overlap |
| Recognition evaluation | 16-fold leave-one-subject-out cross-validation (LOSO-CV) |

The current-utterance and context-segment counts above refer to the 191-sample recognition benchmark. The 108 interlocutor segments come from 76 samples, some of which contain more than one context segment. The other 115 samples have one self-statement segment each. The eight `others` samples are retained in the annotations for completeness.

## Modalities and Conversational Context

Each recognition sample connects three sources of information:

- **Vision:** Facial micro-expression timing, including onset, apex, and offset, with the associated action units and emotion label.
- **Audio:** The complete utterance spoken when the micro-expression occurs, together with its preceding conversational context. The utterance-level audio is not limited to the brief duration of the facial event.
- **Text:** Manual transcripts of the current utterance and preceding context.

The preceding context is labeled by its conversational role:

| Context role | Description |
| --- | --- |
| Interlocutor utterance | Another player's preceding speech directed at the target subject, treated as a possible external stimulus |
| Self-statement | The target subject's own preceding speech, treated as conversational background |

These labels describe conversational roles and the intended modeling distinction; they do not establish a causal relationship between an utterance and a facial movement.

## Annotation Protocol

Candidate facial events are screened and inspected frame by frame by a FACS-certified coder. Validated micro-expressions receive onset, apex, and offset marks, action-unit annotations, and emotion labels. A second FACS-certified coder independently annotates the events, and remaining disagreements are resolved through discussion.

The manuscript reports action-unit agreement of **0.89**, calculated as:

$$
\frac{2|A_1 \cap A_2|}{|A_1| + |A_2|},
$$

where $A_1$ and $A_2$ are the action-unit sets assigned by the two coders. This value is a set-overlap agreement score, not a correlation coefficient.

## Annotation Package

The planned release includes the annotation information described in the manuscript:

- Micro-expression onset, apex, and offset marks.
- Facial action units and emotion labels.
- Conversational context-role labels.
- Manual transcripts of current utterances and preceding context.
- URLs of the original source recordings, enabling researchers to locate the corresponding visual material.

The recognition benchmark uses the positive, negative, and surprise categories. The additional `others` entries are excluded when reproducing the paper's three-class experiments.

Final filenames, field definitions, and any accompanying evaluation files will be documented with the release.

## Data Access

Applications for the annotation package will open after acceptance of the manuscript. Once applications open:

1. Email **[jbwang24@mails.jlu.edu.cn](mailto:jbwang24@mails.jlu.edu.cn)** with your name, institutional affiliation, and a brief description of your intended research to obtain the access acknowledgment form.
2. Complete the form and sign it by hand.
3. Scan the signed form into PDF format and name it `TriCoME_Agreement_[Your_Name].pdf`.
4. Return the PDF to the same address with the subject line `[TriCoME Data Request] Your Name - Institution`.

The maintainers will review the request and provide the annotation package and source-recording URLs after approval. Researchers and students at academic or non-profit research institutions are welcome to apply for non-commercial research use.

The form administers initial delivery and acknowledgment of the license and source-content notices. It does not add restrictions to the rights granted by CC BY-NC 4.0. Recipients may share or adapt the CC-licensed material for non-commercial purposes under that license.

## Accessing the Source Recordings

**The dataset release does not redistribute raw videos, edited clips, video frames, or audio files.** The annotation package points to publicly available source recordings. Researchers must obtain lawful access to the underlying recordings independently and follow the applicable source-platform terms and rights-holder permissions.

Copyright and related rights in the recordings remain with their respective rights holders. The annotation license does not grant rights in the underlying video, audio, images, or original dialogue reproduced in transcripts.

## Evaluation and Reported Reference Results

The manuscript evaluates three-class recognition using **16-fold LOSO-CV**. In each fold, one subject is held out for testing and the remaining subjects are used for training. Accuracy and unweighted F1 (UF1, macro-averaged across the three emotion classes) are reported.

| Configuration | Input | Accuracy (%) | UF1 (%) |
| --- | --- | --- | --- |
| MMNet (adapted) | Vision only | 82.96 | 77.87 |
| HFFNet with fixed-threshold routing | Vision, audio, text, and role-annotated context | 85.89 | 83.26 |

These are results reported in the accompanying manuscript. **MMNet (adapted)** is the task-adapted visual implementation evaluated in HFFNet's `visual_only` mode. The HFFNet configuration uses a fixed routing threshold of 0.8. Training and evaluation details are given in the manuscript.

HFFNet combines audio-text interaction and sequence compression with context-type embeddings, feature gating, and visual-confidence-based routing to regulate the contribution of conversational information.

## Citation

If you use TriCoME in your research, please cite the accompanying manuscript. A public preprint or publication link will be added when available. Until then, the manuscript can be referenced as:

```bibtex
@unpublished{wang2026tricome,
  title  = {Trimodal Context-Aware Micro-Expression Recognition in Real-World Conversations: A Dataset and a Hierarchical Fusion Network},
  author = {Wang, Junbo and Zhao, Yan and Wang, Shigang and Wei, Jian and Zhang, Qiming and Wu, Yu},
  year   = {2026},
  note   = {Manuscript}
}
```

## License

The contributors' original annotations, metadata, and repository documentation are licensed under **[Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)**, to the extent that the contributors hold the relevant rights. See [LICENSE](LICENSE) for the scope notice and link to the governing legal text.

The license permits non-commercial sharing and adaptation with appropriate attribution, a license reference, and an indication of changes. Non-commercial status depends on the intended use, not simply on the user's institutional affiliation. No permissions are granted for third-party content or privacy and personality rights that the contributors do not control.

## Privacy and Correction Requests

TriCoME includes manually transcribed dialogue and links to identifiable public recordings. Using subject indices does not guarantee anonymity: source faces, voices, dialogue, and recording URLs may remain identifying.

Individuals featured in the source recordings, or relevant rights holders, may contact **[jbwang24@mails.jlu.edu.cn](mailto:jbwang24@mails.jlu.edu.cn)** regarding an annotation, privacy concern, or correction request. Please provide enough information to identify the recording and affected entry.

The maintainers will review substantiated requests and, where appropriate, correct or remove affected entries from future releases and the copies they distribute. This cannot guarantee deletion of copies already obtained by others and does not revoke licenses already validly granted under CC BY-NC 4.0.

## Contact

For dataset access and repository questions: **[jbwang24@mails.jlu.edu.cn](mailto:jbwang24@mails.jlu.edu.cn)**.
