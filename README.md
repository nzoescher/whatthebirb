# WhatTheBird 🐦

Bilderkennung für heimische Vogelarten mit Deep Learning. Das Modell erkennt anhand eines Fotos, welche von sieben in Deutschland häufigen Gartenvögeln zu sehen ist.

![Confusion Matrix](images/confusion_matrix.png)

## Überblick

| | |
| --- | --- |
| **Aufgabe** | Bildklassifikation mit 7 Klassen |
| **Datensatz** | ca. 3.400 Bilder (2.727 Training/Validierung, 704 Test) |
| **Ansatz** | Transfer Learning mit vortrainiertem VGG16 |
| **Testgenauigkeit** | ~75 % |
| **Tech-Stack** | Python, PyTorch, PyTorch Lightning, torchvision, scikit-learn, Matplotlib |

### Erkannte Vogelarten

Amsel · Blaumeise · Buchfink · Erlenzeisig · Feldsperling · Kohlmeise · Rotkehlchen

## Ansatz

**Transfer Learning:** Statt ein Netz von Grund auf zu trainieren, nutzt das Projekt die Faltungsschichten von VGG16, das auf ImageNet vortrainiert wurde. Diese Schichten erkennen bereits allgemeine Bildmerkmale wie Kanten, Texturen und Formen und bleiben beim Training eingefroren. Trainiert wird nur ein eigener Klassifikationskopf aus zwei vollständig verbundenen Schichten (rund 2,1 Mio. von 16,8 Mio. Parametern).

Mit nur einigen tausend Bildern lernt ein Netz von Grund auf deutlich schlechter. Das vortrainierte Netz bringt das nötige Grundwissen über Bilder bereits mit.

**Training:**
- Eingabegröße 128 × 128 Pixel, normalisiert mit den ImageNet-Werten
- Data Augmentation auf den Trainingsdaten (Rotation, Spiegelung, Helligkeit und Kontrast)
- 80/20-Split in Training und Validierung mit festem Seed
- Optimierer Adam, Verlustfunktion Cross-Entropy
- Early Stopping auf dem Validierungsverlust und Speichern des besten Modells per Checkpoint

**Auswertung:** Eine Confusion Matrix zeigt, welche Arten das Modell miteinander verwechselt. [Kurz beschreiben, was auffällt, z. B. welche zwei Arten am häufigsten verwechselt werden und warum das plausibel ist.]

## Ergebnisse

| Metrik | Wert |
| --- | --- |
| Testgenauigkeit | [X] % |
| Epochen bis Early Stopping | [X] |

[Beispielbilder mit Vorhersage einfügen, z. B. `images/beispiele.png`]
```

