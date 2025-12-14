# Automation-Anywhere1A: Computer Vision for Check Understanding & Signature Verification

## Team Members

| Name | GitHub Handle | Contribution |
|------|---------------|--------------|
| Evelyn | @e2sun | Project management, data preparation, coordination |
| Anmol | — | Data preparation, dataset cleaning and validation |
| Angelina | @angelinadegay | Data processing, annotation conversion, dataset restructuring |
| Julia | — | Model training, evaluation, performance analysis |
| Mahi | — | Model training, evaluation, performance analysis |

## Project Highlights

- Developed an end-to-end computer vision pipeline for automated bank check understanding using YOLO-based object detection models.
- Automated detection of key check fields (date, payee, legal amount, courtesy amount) and signature regions.
- Enabled signature verification by distinguishing genuine vs. forged signatures as separate object classes.
- Built scalable data preprocessing and annotation conversion pipelines to prepare the SSBI dataset for training.
- Demonstrated how intelligent document processing can reduce manual check-processing costs and errors for enterprise automation workflows at Automation Anywhere.

## Setup and Installation

### 1. Clone the repository

```bash
git clone https://github.com/angelinadegay/Automation-Anywhere1A.git
cd Automation-Anywhere1A
```

### 2. (Optional) Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch notebooks

```bash
jupyter notebook
```

Open any notebook under the `notebooks/` directory to begin data processing, training, or evaluation.

## Project Overview

This project was developed as part of the **Break Through Tech AI Fellowship – AI Studio**, in collaboration with **Automation Anywhere**.

The objective of this challenge was to explore how computer vision and machine learning can be applied to intelligent document processing, specifically for bank checks, which are visually complex and error-prone when processed manually.

In real-world enterprise settings, manual check processing is expensive, time-consuming, and susceptible to human error. This project demonstrates how automated detection and verification of check fields and signatures can improve accuracy, scalability, and security in financial document workflows.

## Data Exploration

### Dataset Used

**SSBI (Synthetic Signature Bankcheck Images) Dataset**

- 4,360 annotated bank check images
- COCO-style annotations
- Includes genuine signatures, forged signatures, and bounding boxes for all key check fields

**Source:**
Enhanced Bank Check Security: Introducing a Novel Dataset and Transformer-Based Approach for Detection and Verification  
Document Analysis Systems (DAS) Workshop @ ICDAR 2024  
https://doi.org/10.1007/978-3-031-70442-0_3

### Data Processing & EDA

- Removed corrupted and duplicate images
- Validated annotation consistency
- Converted COCO annotations to YOLO format
- Filtered outliers and restructured the dataset for training
- Re-split data into train, validation, and test sets

### Challenges & Assumptions

- High variability in handwriting and signatures
- Cluttered document layouts
- Synthetic data required careful validation to ensure realism

## Model Development

**Model Type:** YOLO object detection models (YOLO11 n/s/m variants)

**Task:** Multi-class object detection for check fields and signature types

**Training Setup:**
- GPU-accelerated training (CUDA recommended)
- Image size: 640×640

**Approach:**
- Detection-based formulation of signature verification
- Modular and extendable training pipeline

## Results & Key Findings

- Successfully detected all major check components with strong localization performance
- Clear separation between genuine and forged signatures at the detection level
- Automated preprocessing significantly reduced manual data preparation effort
- Results demonstrate the feasibility of computer vision–based financial document intelligence

## Next Steps

- Extend the pipeline to real-world scanned checks
- Integrate transformer-based signature verification models
- Perform deeper fairness and bias analysis across handwriting styles
- Integrate OCR for text extraction
- Optimize models for production deployment and latency constraints

## License

This project is licensed under the CC BY-NC 4.0 License unless otherwise specified.  
See the LICENSE file for full details.

## References

- Khan et al., Enhanced Bank Check Security: Introducing a Novel Dataset and Transformer-Based Approach for Detection and Verification, ICDAR 2024.
- Ultralytics YOLO Documentation

## Acknowledgements

We thank Break Through Tech AI for the AI Studio Fellowship, Automation Anywhere for the industry problem context, and our Challenge Advisor and TAs for their guidance and support throughout the project.
