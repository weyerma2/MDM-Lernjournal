# Lernjournal 3 ONNX

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| ONNX Modell für Analyse (Netron) | https://github.com/onnx/models/tree/main/Natural_Language_Processing/bert_Opset17_transformers |
| onnx-image-classification Fork (EfficientNet-Lite) | https://github.com/weyerma2/lernjournal3 |

## Dokumentation ONNX Analyse
### Modellarchitektur

# Input-Tensoren
input_ids (int64, [batch_size, sequence_length])
attention_mask (int64, optional)
token_type_ids (int64, optional)

# Kernstruktur
Ein klassisches BERT Encoder-Stack, bestehend aus:
Mehreren LayerNorm, MatMul, Add, Softmax, Reshape, Transpose
Multi-Head Attention Blöcken
Feedforward-Netzen mit GELU-Aktivierung
Residual Connections

# Output-Tensor
last_hidden_state oder pooled_output, je nach Verwendung (z. B. Klassifikation oder Token-Level-Tasks)

### Modellkomplexität
Die Visualisierung zeigt eine tiefe Transformer-Architektur mit geschätzten 12 Layern (Encoder Blocks)
Jede Schicht enthält typische Komponenten eines Transformer-Modells:
Selbst-Attention
Feedforward-Netz
Layer-Normalisierung

Das Modell bert_Opset17_transformers repräsentiert eine vollständige Implementierung des BERT-Encoders mit allen wesentlichen Subkomponenten für Sprachverarbeitung. Die Analyse mit Netron erlaubt ein detailliertes Verständnis der internen Struktur, besonders hilfreich zur Optimierung oder zur Konvertierung für die ONNX-Runtime.

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/lernjournal3-onnx/images/netron.jpeg" />


## Dokumentation onnx-image-classification

# Das Ziel dieses Experiments war es, die Klassifikation eines Bildes mithilfe dreier Varianten des EfficientNet-Lite4-Modells durchzuführen
EfficientNet-Lite4
EfficientNet-Lite4-int8
EfficientNet-Lite4-qdq

Dabei wurde geprüft, wie sich die Modellvarianten (Original, quantisiert, quantisiert+QDQ) auf die Analyseergebnisse auswirken.

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/lernjournal3-onnx/images/frontend.jpeg" />

# Vergleich der Modellantworten
Modell	Top-1 Label	Wahrscheinlichkeit
EfficientNet-Lite4	beach wagon / station wagon / wagon	85.99 %
EfficientNet-Lite4-int8	beach wagon / station wagon / wagon	94.34 %
EfficientNet-Lite4-qdq	beach wagon / station wagon / wagon	86.10 %

Zweit- und Drittklassifikationen variierten leicht:

grille, radiator grille: 8.70 % bis 10.86 %

car wheel: 0.55 % bis 1.69 %

# Interpretation
Alle Modelle identifizierten das Auto konsistent als Station Wagon (Kombi).
Unterschiede in den Wahrscheinlichkeiten zeigen leichte Einflüsse durch Quantisierung (int8) und zusätzliche **QDQ (Quantize-Dequantize) Transformationen.
Das int8-Modell zeigt die höchste Top-1-Wahrscheinlichkeit, vermutlich durch reduzierte Modellkomplexität bei stabiler Generalisierung.

Die App wurde erfolgreich erweitert, um drei ONNX-Modelle parallel auszuführen. Das ermöglicht einen quantitativen Vergleich zwischen Modellvarianten bzgl. ihrer Vorhersagen.