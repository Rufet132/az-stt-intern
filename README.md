# 🎙️ Whisper Azerbaijani ASR: Baseline vs Fine-Tuning

Bu layihə, Azərbaycan dili üçün nitqin mətnə çevrilməsi (Automatic Speech Recognition - ASR) sisteminin qurulması və optimallaşdırılması məqsədini daşıyır. Layihə çərçivəsində OpenAI-ın **Whisper-small** modeli həm ilkin (zero-shot), həm də fine-tune edilmiş versiyada müqayisə olunub.

## 🚀 Layihənin İzahı
Layihə iki əsas hissədən ibarətdir:
1.  **Hissə A (Baseline):** Hazır Whisper-small modelinin heç bir təlim görmədən Azərbaycan dilindəki performansı ölçülüb.
2.  **Hissə B (Fine-tuning):** Model, Mozilla Common Voice 17.0 (az) datasetinin kiçik bir hissəsi ilə fine-tune edilərək yerli dil strukturuna adaptasiya olunub.

## 🛠️ Model və Parametrlər
*   **Base Model:** `openai/whisper-small`
*   **Dataset:** Mozilla Common Voice 17.0 (az)
*   **Təlim Parametrləri:**
    *   **Steps:** 50 steps
    *   **Learning Rate:** 5e-6
    *   **Batch Size:** 8
    *   **Optimizer:** AdamW
    *   **Strategiya:** `load_best_model_at_end=True` (Validasiya WER göstəricisinə əsasən ən yaxşı checkpoint-in seçilməsi).

## 📊 WER və CER Nəticələri
Modelin inkişafı aşağıdakı cədvəldə əks olunub:

| Model | WER (Word Error Rate) | CER (Character Error Rate) | Qeyd |
| :--- | :---: | :---: | :--- |
| **Whisper-small (Baseline)** | 49.0% | 25.0% | Zero-shot (İlkin hal) |
| **Whisper-small (Fine-tuned)** | 29.4% | 12.3% | 50 steps Fine-tuning |

> **Analiz:** Fine-tuning prosesindən sonra xəta dərəcələri (WER və CER) əhəmiyyətli dərəcədə azalıb. CER-in WER-dən aşağı olması modelin hərfləri/səsləri uğurla tanıdığını, lakin bitişdirici dil strukturuna görə şəkilçilərdə təkmilləşməyə ehtiyacı olduğunu göstərir.

## ⚙️ Quraşdırma və İşə Salma

### 1. Kitabxanaları yükləyin:
```bash
pip install transformers datasets jiwer accelerate evaluate librosa
