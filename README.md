# 📊 DISPLAI-AI — Predicting PAP from EIT

Transform **Electrical Impedance Tomography (EIT) voltages** into **Pulmonary Artery Pressure (PAP)** using a clean, reproducible pipeline.  
This repo includes synchronization, preprocessing, training, and visualization notebooks tailored for clinical research.

---

## 🚀 Pipeline Overview

```mermaid
graph LR
    A[Raw Voltage EIT and Raw PAP] --> B[Apnea window cut - EitPapSynchronizer]  
    B --> C[Upsample PAP to EIT grid - EitPapSynchronizer]
    C --> D[Voltage filtering and features - VoltaFilterTransformation]
    D --> E[Model training - Displaid_AI_V1]
    B --> F[Diagnostics plots - eit-pap-Tidal_plotter]
    
```

**Step 1.** Synchronize EIT & PAP using apnea times from `clinical_config.json`.
**Step 2.** Upsample PAP to the EIT timeline (same rows as voltage).
**Step 3.** Filter & transform voltages into model-ready tensors.
**Step 4.** Train and evaluate deep-learning models.
**Step 5.** Visualize & validate alignment and filtering.

---

## 📂 Repository Structure

```
DISPLAI_AI/
├─ data_displaid_tidal/                 # clinical data + config
│  └─ clinical_config.json              # apnea_start_time / apnea_end_time per patient
├─ EitPapSynchronizer.ipynb             # trim to apnea window + upsample PAP to EIT grid
├─ VoltaFilterTransformation.ipynb      # denoise, (optional) band-pass, normalize, window
├─ Displaid_AI_V1.ipynb                 # model training & evaluation (PyTorch)
└─ eit-pap-Tidal_plotter.ipynb          # QA/diagnostic plots for alignment & filters
```

---

## 🩺 Clinical Config (apnea-driven sync)

Each patient’s apnea window is defined in seconds in `clinical_config.json`:

```json
{
  "TDL016": {
    "events": {
      "apnea_start_time": 123.0,
      "apnea_end_time": 153.0
    }
  }
}
```

* Both **Voltage** and **PAP** are trimmed to `[start, end)`.
* If `apnea_end_time < apnea_start_time`, the synchronizer raises an error.
* Sampling rates: default `eit_sr = 50.355 Hz`; set `pap_sr` to the true PAP rate if known.

---

## ⚙️ Requirements

* Python **3.9+**
* Jupyter Notebook
* Libraries:
  `numpy`, `pandas`, `matplotlib`, `scipy`, `scikit-learn`, `torch`

---

## 🔧 How to Run

1. **Synchronize & Upsample** → Run `EitPapSynchronizer.ipynb`
2. **Filter Voltages** → Run `VoltaFilterTransformation.ipynb`
3. **Train AI** → Run `Displaid_AI_V1.ipynb`
4. **Visualize** → Run `eit-pap-Tidal_plotter.ipynb`

---

## 🔮 Roadmap

* 🧠 Stronger sequence models (CNN-BiLSTM, Transformers)
* ⚡ Real-time inference for bedside monitoring
* 🔍 Automatic apnea detection (no manual config)
* 📈 Larger datasets for generalization

---

> 📌 *Research use only. Handle patient data according to your IRB/ethics and privacy requirements.*
