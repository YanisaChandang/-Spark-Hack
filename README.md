# 💧 OneWaterAI

### Environmental water-quality risk monitoring, forecasting, and community action

**Study area:** Ko Sichang (เกาะสีชัง), Chonburi, Thailand  
**Project:** Spark Hack — research prototype  
**Status:** Prototype under development · simulated risk data · not validated for public-health decisions

## Overview

OneWaterAI is a proposed decision-support dashboard that brings together **microbial indicators**, **environmental conditions**, **geographic information systems (GIS)**, and **machine learning** to explore water-quality risk across **12 demonstration areas (B01–B12)** around Ko Sichang.

The aim is to move from *data* to *interpretable risk information* and, eventually, to *locally relevant actions*. The prototype is designed for research, education, and discussion with stakeholders—not as an official water-safety warning system.

**Conceptual workflow**

```text
Environmental + microbial indicators + GIS
                    ↓
       Demonstration risk score (0–100)
                    ↓
  Regression vs neural-network comparison
                    ↓
     Conditional 30-day risk scenarios
                    ↓
   Role-specific suggested actions & feedback
```

## Application pages

| Page | Main functions |
| --- | --- |
| **Home / Dashboard** | Overview map for B01–B12, current illustrative scores and categories, indicator details, and historical trends. |
| **Forecast & Action** | Compare Ridge regression and a multilayer perceptron (MLP) neural network; explore 30-day rainfall-related scenarios; review model metrics and stakeholder-specific tasks. |
| **Risk Simulator** | Change input values, use a trained model to estimate the revised score, and inspect a simple sensitivity analysis. |

The planned interface is in **Thai**, while scientific indicator names remain in English.

## Inputs

- **Human-associated indicators:** HF183, crAssphage, PMMoV.
- **Animal-associated candidate indicators:** C16S, qC160F (assay definitions and host specificity require literature verification).
- **Aquatic biodiversity / eDNA targets:** MiFish, MollCOI253, Ceph16S, Crust16S.
- **Pathogen targets:** human norovirus GI/GII; VP28, YHV-1, AHPND, and NNV for aquatic-animal health contexts.
- **Environmental variables:** rainfall, temperature, dissolved oxygen (DO), and pH, including antecedent-rainfall features.
- **GIS context:** island terrain slope, modeled drainage catchments and flow paths, and exploratory slope-based groundwater screening.

**Scientific distinction:** Biodiversity targets are not equivalent to host-specific microbial source tracking (MST) markers or proof of disease. Detecting a genetic target does not, by itself, demonstrate viable pathogens or health risk.

## Risk scoring and modeling

The current Python demonstration generates reproducible **synthetic daily data** for 12 sites. Microbial target values are **illustrative 0–100 indices**, *not* laboratory concentrations, positive-test results, or sequencing read counts. A transparent, illustrative formula generates a reference score from selected inputs. Thresholds are for demonstration only:

| Score | Demonstration category |
| --- | --- |
| 0 to <35 | Low |
| 35 to <65 | Moderate |
| 65 to 100 | High |

Two models learn to predict this **synthetic score** using comparable predictors:

1. **Ridge regression:** baseline statistical / machine-learning model.
2. **MLP neural network:** nonlinear machine-learning model.

The current prototype uses a **chronological training/test split** and reports **R², MAE, and RMSE**. These metrics indicate how well the models reproduce simulated outcomes; they **do not establish real-world forecasting accuracy**. The 30-day outputs are **conditional scenarios based on assumed future inputs**, not actual rainfall forecasts.

## Ko Sichang GIS data

A separate preliminary R/GIS assessment has examined:

- Terrain slope from elevation data.
- Modeled coastal drainage basins **B01–B12** and flow paths.
- An **unvalidated slope-only** proxy for groundwater infiltration suitability.

The underlying GIS layers should be exported from R (for example, as **GeoJSON** in WGS 84 / EPSG:4326) before they can be used as authentic interactive boundaries in the Python dashboard. A GIS figure or screenshot alone is not a substitute for geospatial source data.

**B01–B12 modeled catchments must not be described as verified field-sampling locations.** Until actual monitoring coordinates and measured values are provided, mapped points and risk results should be labeled as demonstrations.

## Run the prototype in Google Colab

> **Repository note:** The Colab notebook/application source will need to be added to this repository. The repository may not yet contain a runnable notebook.

Once the notebook is available:

1. Open its `.ipynb` file in **Google Colab**.
2. Select **Runtime → Run all**.
3. Let the notebook install dependencies, generate synthetic data, and train the two models.
4. Open the **temporary Gradio public URL** printed by the notebook.
5. Explore the dashboard, forecasting scenarios, and risk simulator.

Main Python packages: `gradio`, `plotly`, `pandas`, `numpy`, and `scikit-learn`.

The web link works **only while the Colab runtime remains active**. Google Colab and the Gradio share link are **not permanent hosting**. Prototype form submissions and uploaded images are stored temporarily in the runtime; they may disappear when it shuts down. **Do not submit personal, confidential, or sensitive data.**

## Planned development

- [x] Define a three-page dashboard and reproducible synthetic-data demonstration.
- [x] Implement an illustrative score and comparison of Ridge regression vs MLP in the development Python code.
- [ ] Publish and test the final Colab notebook in this repository.
- [ ] Integrate original R/GIS catchment polygons, flow paths, and optional terrain layers.
- [ ] Replace synthetic indicators and assumed site locations with quality-controlled field data.
- [ ] Develop and validate risk scoring against an appropriate real-world outcome.
- [ ] Co-design and assess suggested actions with local stakeholders.
- [ ] Design secure, persistent storage and hosting if community use becomes appropriate.

## Limitations and responsible use

**This is a research demonstration, not a validated public-health or environmental warning tool.** Risk scores, thresholds, model results, and mitigation suggestions should not be used to declare that water, seafood, or recreational activities are safe or unsafe. Groundwater-screening outputs are preliminary terrain proxies, not measured groundwater resources. Real-world deployment will require appropriate field observations, assay validation, transparent risk/outcome definitions, model validation, data governance, and local review.

---

*OneWaterAI · Spark Hack research prototype · Ko Sichang, Thailand*
