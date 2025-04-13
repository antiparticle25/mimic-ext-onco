# Bridging Clinical and Genomic Data: An Oncology-Focused Subset of MIMIC-IV Aligned with TCGA

## Overview & Workflow

This project comprises a **curated, oncology-focused relational dataset** from the [MIMIC-IV clinical database](https://mimic.physionet.org/), one of the largest publicly available medical datasets that encompass detailed patient-level information at the Beth Israel Deaconess Medical Center. It isolates and structures information relevant to **cancer patients** to support downstream analysis, visualization, or machine learning workflows, and serves as a foundation for bridging clinical data (MIMIC-IV) with molecular profiles (e.g., TCGA).

- Extracted key tables from MIMIC-IV (patients, admissions, diagnoses, ICU stays, prescriptions, labs) in a local **PostgreSQL** setup
  
- Filtered all data to focus on oncology-relevant fields:
  - **Diagnoses** with cancer-related ICD codes (ICD-9/10 neoplasm chapters)
  - **Lab values** (blood counts, liver enzymes, tumor markers)
  - **Medications** relevant to chemotherapy or immunotherapy
  - 
- Defined a **derived oncology cohort** for fast patient filtering based on ICD logic
  
- Built supporting views for treatment timelines and labeled lab tests
  
- Optimized for efficient querying via indexes and materialized views

---

## Core Schema Structure

The dataset is structured using 3 broad types of tables:

| Category              | Description                                                                 | Examples |
|----------------------|-----------------------------------------------------------------------------|----------|
| **Main Tables**       | Core entities: patient demographics, admissions, ICU stays, cohort flag     | `oncology_patients`, `oncology_admissions`, `oncology_icustays`, `oncology_cohort` |
| **Fact Tables**       | Event-level records: diagnoses, labs, prescriptions, EMAR (med admin records) | `oncology_diagnoses`, `oncology_labs`, `oncology_prescriptions`, `oncology_emar_detail` |
| **Reference Tables**  | Dictionaries or derived views for enrichment or summarization                | `oncology_icd_dict`, `oncology_labs_with_labels`, `oncology_emar_detail_with_times`, `oncology_treatment_windows` |

---

Visual representation of the schema:

![Oncology-Focused MIMIC-IV Schema](files/oncology_mimic_schema_updated.png)

---

## Use Cases

- Track cancer patients longitudinally (lab values, medications, ICU stays)
- Model treatment response or outcomes
- Build dashboards or visualizations for clinical metrics
- Practice clinical data engineering and SQL workflows
- Integrate with genomics registries (e.g. TCGA) for multimodal analysis
