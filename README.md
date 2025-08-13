# Emotional Dynamics in Response to Visual Stimuli

This repository contains the data, code, and results for a psychological research project investigating how individuals emotionally respond to different types of visual stimuli (negative, neutral, and positive images). The study focuses on the dynamics of emotional responses, affective inertia, cross-affect influences, and demographic differences using advanced statistical modeling.

---

## 📊 Project Overview

**Objective:**  
To analyze emotional responses in terms of **negative affect**, **positive affect**, and **arousal** across 105 visual trials per participant, and examine:
- Emotional dynamics (inertia, reactivity)
- Cross-lagged effects between emotional states
- Demographic influences (sex, age, ethnicity)

**Participants:**  
- N = 156  
- Each completed 105 trials  
- Demographics: Diverse ethnic backgrounds  
- Mean age ≈ 20.8 (SD ≈ 2.9), 53% female

---

## 🧠 Research Questions

1. Do emotions exhibit different levels of inertia depending on stimulus type?
2. Do affective states predict one another across time (cross-lagged effects)?
3. Are there systematic differences by **sex**, **age**, or **ethnicity**?
4. Do individuals differ in mean response levels, variability, and reactivity?

---

## 📁 Data Description

**Main Dataset:** `feelings_initial.RData`  

### 1. Long-format Dataset: `dat`

| Variable     | Description                            |
|--------------|----------------------------------------|
| `subj`       | Participant ID                         |
| `trial.num`  | Trial number (1–105)                   |
| `trial.val`  | Type of image (Negative / Neutral / Positive) |
| `sex`        | Gender (Male / Female / Other)         |
| `age`        | Age of participant                     |
| `ethn`       | Ethnicity                              |
| `Ineg`       | Negative affect score                  |
| `Ipos`       | Positive affect score                  |
| `Iaro`       | Arousal score                          |

- **Total Observations:** 16,380 (156 × 105)
- **No missing data or outliers detected**

### 2. Wide-format Matrices

- `Ineg_wide`: Negative scores per trial per participant
- `Ipos_wide`: Positive scores
- `Iaro_wide`: Arousal scores

---

## 🔍 Analyses

### (1) **Affective Inertia Comparison**

- **File:** `feelings_initial.Rmd`, `feelings_initial.pdf`
- **Methods:**
  - Linear Mixed-Effects Models (LME)
  - Autoregressive modeling (lag-1 coefficients)
  - Pairwise t-tests, MANOVA, ANOVA, Bonferroni correction
- **Tools:** `dplyr`, `base R`, `lme4`

#### 🧪 Model Specifications
```R
Ineg ~ trial.val + sex + age + ethn + (1 | subj)
Ipos ~ trial.val + sex + age + ethn + (1 | subj)
Iaro ~ trial.val + sex + age + ethn + (1 | subj)
```

#### 📈 Key Results:
- **Inertia Scores** (Mean):
  - Ineg = 0.143
  - Ipos = 0.137
  - Iaro = 0.414 (highest)
- **By Demographics:**
  - No significant sex or age differences after Bonferroni
  - Minor ethnicity differences did not survive correction

---

### (2) **Cross-Lagged Panel Modeling (CLPM)**

- **File:** `RI-CLPM.Rmd`, `RI-CLPM.pdf`
- **Objective:** Examine how emotional states predict each other over time

#### 🔁 Model Paths
- **Autoregressive:**
  - `Ipos ~ Ipos_lag1`, `Ineg ~ Ineg_lag1`, `Iaro ~ Iaro_lag1`
- **Cross-lagged:**
  - `Ipos ~ Ineg_lag1 + Iaro_lag1`
  - `Ineg ~ Ipos_lag1 + Iaro_lag1`
  - `Iaro ~ Ipos_lag1 + Ineg_lag1`

#### 🔍 Findings:
- **Positive ↔ Negative Affect**: Reciprocal prediction
  - `Ipos_lag1 → Ineg`: β = 0.172***
  - `Ineg_lag1 → Ipos`: β = 0.166***
- **Arousal Suppression:**
  - Negative and Positive emotions suppress arousal (β < 0)
- **Demographic Moderation:**
  - **Sex**: Females have higher arousal inertia
  - **Age**:
    - Older → stronger Ipos_on_Ineg (r = .124***)
    - Older → stronger Ipos_on_Aro (r = .202***)
    - Older → more Aro suppresses Ineg (r = –.215***)

#### 🧪 RI-CLPM Model Variants:
- 3-trial RI-CLPM: Poor fit (CFI ≈ 0, RMSEA ≈ .30)
- Block-based (11 blocks): Better fit (CFI ≈ .73)

---

### (3) **Average, Variability, and Reactivity Analysis**

- **File:** `Avg+SD+Reactivity.Rmd`, `Avg+SD+Reactivity.pdf`
- **Goals:**
  - Compute within-person **mean**, **standard deviation**, and **reactivity**
  - Compare across sex, age, and ethnicity

#### 🧮 Metrics:
- Mean scores: `Ipos_mean`, `Ineg_mean`, `Iaro_mean`
- SDs: `*_sd`
- Reactivity:  
  - `*_reac_pos`, `*_reac_neg` (difference from neutral trials)

#### 🔍 Analysis Pipeline:
1. **MANOVA** (Wilks’ Lambda) on all metrics
2. **Type III ANOVA**: `lm(metric ~ sex + age + ethn)`
3. **Robust regression** (rlm) + FDR correction

#### 📈 Key Findings:
- **Females**: Higher negative affect, more variability, stronger reactivity
- **After FDR**: No significant results survived → small effect sizes

---

## 🧾 Summary of Key Findings

1. **Arousal shows the highest emotional inertia**.
2. **Positive and negative emotions predict each other over time**.
3. **Females**: Stronger negative affect, more within-person variability.
4. **Demographics** showed nuanced but **modest** effects overall.
5. **RI-CLPM** supports emotion reciprocity, but model fit is mixed.

---

## 🛠️ Tools & Packages Used

- `R` (Base functions)
- `dplyr` – Data wrangling
- `lme4` – Linear mixed-effects models
- `lavaan` – Structural Equation Modeling
- `car` – Type III ANOVA
- `MASS` – Robust regression
- `bestNormalize` – Normalizing skewed variables

---

## 📂 Repository Structure

```
📦 Emotional-Dynamics-Study
├── data/
│   └── feelings_initial.RData
├── scripts/
│   ├── feelings_initial.Rmd
│   ├── RI-CLPM.Rmd
│   └── Avg+SD+Reactivity.Rmd
├── outputs/
│   ├── feelings_initial.pdf
│   ├── RI-CLPM.pdf
│   └── Avg+SD+Reactivity.pdf
├── README.md
```

---

## 📌 Citation

If you use this dataset or analysis scripts in your work, please cite the corresponding GitHub repository and credit the original researchers.

---

## 📬 Contact

For questions, feedback, or collaborations, please reach out via [GitHub Issues](https://github.com/your_username/your_repo/issues).

---