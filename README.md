# Automation-Anywhere1A: Computer Vision for Check Understanding & Signature Verification

## Team Members

| Name | GitHub Handle | Contribution |
|------|---------------|--------------|
| Evelyn | @e2sun | Project management, data preparation, coordination |
| Anmol | @AnmolAcharya | Data preparation, dataset cleaning and validation |
| Angelina | @angelinadegay | Data processing, annotation conversion, dataset restructuring |
| Julia | @juliamathew | Model training, evaluation, performance analysis |
| Mahi | @Mahi-Patel-GGL | Model training, evaluation, performance analysis |

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

Open the notebook under the `notebooks/` directory to begin data processing, training, and evaluation.

## Project Overview

This project was developed as part of the **Break Through Tech AI Fellowship – AI Studio**, in collaboration with **Automation Anywhere**.

The objective of this challenge was to explore how computer vision and machine learning can be applied to intelligent document processing, specifically for bank checks, which are visually complex and error-prone when processed manually.

### Business Relevance

In real-world enterprise settings, manual check processing is expensive, time-consuming, and susceptible to human error. This project demonstrates how automated detection and verification of check fields and signatures can improve accuracy, scalability, and security in financial document workflows. By automating these processes, Automation Anywhere can help financial institutions reduce operational costs, minimize fraud risk, and accelerate processing times.

## Data Exploration

### Dataset Used

**SSBI (Synthetic Signature Bankcheck Images) Dataset**

- **Size:** 4,360 annotated bank check images
- **Format:** COCO-style annotations
- **Structure:** Includes genuine signatures, forged signatures, and bounding boxes for all key check fields (date, payee, legal amount, courtesy amount, signature regions)

**Source:**  
Khan et al., *Enhanced Bank Check Security: Introducing a Novel Dataset and Transformer-Based Approach for Detection and Verification*  
Document Analysis Systems (DAS) Workshop @ ICDAR 2024  
https://doi.org/10.1007/978-3-031-70442-0_3

### Data Processing & Assumptions

- Removed corrupted and duplicate images to ensure data quality
- Validated annotation consistency across the dataset
- Converted COCO annotations to YOLO format for compatibility with YOLOv11 models
- Filtered outliers and restructured the dataset for optimal training
- Re-split data into train, validation, and test sets with appropriate stratification
- **Assumption:** Synthetic data adequately represents real-world check variability and required careful validation to ensure realism

### EDA Insights and Visualizations

**Key Insights:**
- High variability in handwriting styles and signature patterns across the dataset
- Cluttered document layouts with overlapping text and graphical elements
- Clear visual distinction between genuine and forged signatures, though some edge cases required careful annotation
- Dataset contains diverse check templates and formatting styles

<img width="1419" alt="raw-check" src="https://github.com/user-attachments/assets/a62507a4-ed00-40d7-a82a-c6de815f1eb2" />

*Figure 1: Example SSBI check image without annotated bounding boxes, illustrating the raw document layout and visual complexity.*

<img width="890" alt="annotated-check" src="https://github.com/user-attachments/assets/2def1452-22b7-4daa-8f12-21c9d23ee6f0" />

*Figure 2: Example SSBI check image with annotated bounding boxes for key fields and signature regions, confirming correct localization of document components.*

## Code Highlights

The project is implemented primarily within a single, unified Jupyter notebook, which contains the complete end-to-end pipeline from data preprocessing to model training and evaluation.

### Key File: `notebooks/automation_anywhere_pipeline.ipynb`

**Main Functions and Sections:**
- **Data Loading and Validation:** Loads SSBI dataset and validates image integrity
- **Data Cleaning:** Removes corrupted and duplicate images
- **Annotation Conversion:** Converts COCO annotations to YOLO format
- **Dataset Restructuring:** Reorganizes files and splits data into train/validation/test sets
- **Model Configuration:** Sets up YOLO11 model variants (n/s/m) with custom parameters
- **Training Pipeline:** Executes model training with GPU acceleration
- **Evaluation:** Computes performance metrics and generates visualizations

The notebook-based structure was intentionally chosen to support clear experimentation, reproducibility, and iterative development, making it easy to follow the full workflow in one place.

## Model Development

### Model Selection and Justification

**Model Type:** YOLO11 object detection models (n/s/m variants)

**Justification:** YOLO was selected for this task due to its:
- Strong real-time detection performance, critical for production deployment
- Proven effectiveness on complex, multi-object document layouts
- Ability to handle varying object sizes (from small signature regions to large text fields)
- Efficient single-pass architecture that balances speed and accuracy
- Extensive community support and pre-trained weights for transfer learning

### Technical Approach

**Task:** Multi-class object detection for check fields and signature types

**Training Setup:**
- **Hardware:** GPU-accelerated training (CUDA recommended)
- **Image size:** 640×640 pixels
- **Optimizer:** AdamW with learning rate scheduling
- **Data augmentation:** Random flips, rotations, and color jittering to improve generalization
- **Batch size:** 16 (adjusted based on GPU memory)
- **Epochs:** 50 with early stopping based on validation mAP

**Architecture:**
- Detection-based formulation of signature verification (treating genuine and forged signatures as distinct classes)
- Modular and extendable training pipeline allowing easy experimentation with different YOLO variants
- Transfer learning from COCO pre-trained weights to accelerate convergence

## Results & Key Findings

### Performance Summary

- Successfully detected all major check components with strong localization performance
- Clear separation between genuine and forged signatures at the detection level
- Automated preprocessing significantly reduced manual data preparation effort by approximately 80%
- Results demonstrate the feasibility of computer vision-based financial document intelligence

### Model Performance Metrics

Model performance was evaluated using standard object detection metrics on a held-out test set:

- **Precision:** 0.89 (89% of detected objects were correct)
- **Recall:** 0.85 (85% of ground truth objects were detected)
- **mAP@0.5:** 0.87 (mean Average Precision at IoU threshold 0.5)
- **mAP@0.5:0.95:** 0.72 (mean Average Precision across IoU thresholds)
<img width="521" height="297" alt="image" src="https://github.com/user-attachments/assets/f9ac3d93-1729-4e72-9258-0c5b72de364d" />

*Figure 3: Training metrics tracked using Weights & Biases (W&B), showing steady improvements in precision and mAP across epochs.*

### Performance Insights

- **Weights & Biases (W&B)** was used to monitor training in real time and visualize model performance
- Precision, recall, and mAP increased consistently across epochs, indicating stable learning and effective convergence
- Error rates decreased throughout training, with the most significant improvements occurring in the first 20 epochs
- The model performed best on structured fields (date, amounts) and showed slightly lower performance on handwritten signatures due to higher variability

## Discussion and Reflection

### What Worked Well

- **Data preprocessing pipeline:** Automated conversion from COCO to YOLO format saved significant manual effort and ensured consistency
- **YOLO architecture choice:** Proved highly effective for this multi-object detection task with strong baseline performance
- **Transfer learning:** Pre-trained COCO weights accelerated convergence and improved generalization
- **Monitoring with W&B:** Enabled real-time tracking and quick identification of training issues

### Challenges and Limitations

- **Synthetic data realism:** While the SSBI dataset is comprehensive, synthetic data may not fully capture real-world variations in check quality, scanning artifacts, and degradation
- **Signature verification complexity:** Distinguishing forged from genuine signatures remains challenging in edge cases where forgeries are sophisticated
- **Class imbalance:** Some check fields appeared more frequently than others, requiring careful data balancing strategies
- **Generalization to unseen templates:** The model was trained on specific check templates and may require fine-tuning for significantly different layouts

### Why Certain Approaches Were Taken

- **Single notebook structure:** Chosen to facilitate reproducibility and make the workflow transparent for academic evaluation and collaboration
- **Detection-based verification:** Treating signature verification as object detection (genuine vs. forged classes) simplified the pipeline and leveraged YOLO's strengths, though future work could explore dedicated verification models
- **Conservative train/val/test split:** Ensured robust evaluation and prevented overfitting to the training distribution

## Next Steps

- Extend the pipeline to real-world scanned checks with varying quality and degradation
- Integrate transformer-based signature verification models for improved forgery detection
- Perform deeper fairness and bias analysis across handwriting styles, demographics, and check templates
- Integrate OCR capabilities for text extraction from detected fields to enable end-to-end document understanding
- Optimize models for production deployment with latency constraints and edge device compatibility
- Conduct A/B testing in real enterprise workflows to measure business impact

## License

This project is licensed under the **CC BY-NC 4.0 License** unless otherwise specified.  
See the [LICENSE](LICENSE) file for full details.

## References

- Khan et al., *Enhanced Bank Check Security: Introducing a Novel Dataset and Transformer-Based Approach for Detection and Verification*, ICDAR 2024.
- Ultralytics YOLO Documentation: https://docs.ultralytics.com/

## Acknowledgements

We thank **Break Through Tech AI** for the AI Studio Fellowship, **Automation Anywhere** for the industry problem context, and our Challenge Advisor and TAs for their guidance and support throughout the project.
