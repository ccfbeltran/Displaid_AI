
<h3 align="center">
  <a name="readme-top"></a>
  <img
    src="https://img.icons8.com/fluency/240/brain.png"
    height="120"
    alt="DISPLAI AI Logo"
  >
</h3>

<div align="center">

  <a href="#">
    <img src="https://img.shields.io/badge/Status-Internal%20Use%20Only-red" alt="Status">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Python-3.9+-blue" alt="Python Version">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Framework-PyTorch-orange" alt="Framework">
  </a>

</div>

---

# 📊 DISPLAI-AI — Predicting PAP from EIT

**Internal research project** for our startup.  
This pipeline transforms **Electrical Impedance Tomography (EIT) voltages** into **Pulmonary Artery Pressure (PAP)** predictions using synchronization, preprocessing, and deep-learning models.

---

## 🚀 Pipeline Overview

```mermaid
flowchart LR
  A[Raw EIT (voltages)\nRaw PAP] --> B[Apnea window cut\n(EitPapSynchronizer.ipynb)]
  B --> C[Upsample PAP → EIT grid\n(EitPapSynchronizer.ipynb)]
  C --> D[Voltage filtering & features\n(VoltaFilterTransformation.ipynb)]
  D --> E[Model training\n(Displaid_AI_V1.ipynb)]
  B --> F[Diagnostics plots\n(eit-pap-Tidal_plotter.ipynb)]
````

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

## 🔒 Notes

* This repository is **private** and for **internal R\&D use only**.
* Do not redistribute or share externally.
* Handle all patient/clinical data according to internal compliance and privacy protocols.

---

<p align="right">
    <a href="#readme-top">↑ Back to Top ↑</a>
</p>
```

---

⚡ This version:

* Keeps the **professional look** (badges, centered logo).
* Makes it clear it’s **internal use only**.
* Removes stars/contributors/community sections (since it’s not public OSS).

Do you want me to also add a **section at the top with “Quick Start for Team Members”** (like setup + example commands), so new engineers at your startup can onboard faster?
