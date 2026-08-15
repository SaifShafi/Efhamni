# Efhamni (افهمني — "Understand Me")

A Saudi Sign Language recognition application that translates isolated SSL gestures into
Arabic text and speech.

Published, peer-reviewed:

> Al Khuzayem, L.; **Shafi, S.**; Aljahdali, S.; Alkhamesie, R.; Alzamzami, O.
> *Efhamni: A Deep Learning-Based Saudi Sign Language Recognition Application.*
> **Sensors** 2024, 24(10), 3112. [doi.org/10.3390/s24103112](https://doi.org/10.3390/s24103112)

BSc Computer Science project, King Abdulaziz University.

---

## The problem

Deaf and hard-of-hearing people in Saudi Arabia have limited options for communicating
with hearing people who do not sign. Existing sign language tooling largely targets ASL;
Saudi Sign Language is a distinct language with its own vocabulary and grammar, and is
substantially under-served.

## Approach

Isolated gesture recognition over video, trained on the KSU-SSL dataset.

**Pipeline:** video → pose and hand keypoint extraction → sequence classification → Arabic
text → speech.

- **Feature extraction** — MobileNetV2 for pose estimation and face detection, SSD for
  hand detection. Keypoints rather than raw pixels, which keeps the sequence model small
  enough to serve at interactive latency.
- **Classification** — CNN feeding a **BiLSTM**. Bidirectional because a sign's meaning
  frequently depends on how it resolves, not only how it starts, so the sequence is read
  forwards and backwards.
- **Serving** — Flask inference API deployed on AWS EC2, called by the mobile client.

## Results

| | |
|---|---|
| Accuracy | **94.46%** |
| Vocabulary | 80 signs |
| End-to-end translation | ~6 seconds |
| Dataset | KSU-SSL |

Evaluated with deaf, hard-of-hearing, and hearing participants — not only offline
against a held-out split.

## Application features

- Translate SSL from live-recorded or uploaded video
- Written **and** spoken Arabic output
- Chat between users
- Personal library of saved videos for fast re-translation

---

## What is in this repository

The Flutter/Dart application layer and interface screenshots:

- `main.dart` — application entry point
- `TranslationDeaf.dart` — translation flow
- `1.png`–`10.png` — interface screens

The training code, the trained model, and the Flask inference service are not published
here. The full method, architecture, and evaluation are in
[the paper](https://doi.org/10.3390/s24103112), which is open access.

## Stack

Flutter · Dart · MobileNetV2 · SSD · CNN-BiLSTM · Flask · AWS EC2
