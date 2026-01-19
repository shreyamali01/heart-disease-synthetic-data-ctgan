# Synthetic Tabular Data Generation for Heart Disease Prediction

This project explores the use of **Conditional Tabular Generative Adversarial Networks (CTGAN)** to generate realistic synthetic tabular data for heart disease prediction. Using the **UCI Cleveland Heart Disease dataset**, the project addresses challenges related to limited data availability, mixed categorical–continuous features, and privacy-sensitive medical data.

---

## Motivation

Medical datasets are often small and difficult to share due to privacy constraints, which can limit the effectiveness of machine learning models. Synthetic data generation provides a promising alternative by enabling data augmentation and privacy-preserving analysis while maintaining key statistical properties of the original data.

This project investigates the ability of CTGAN to learn complex feature distributions in medical tabular data and produce high-quality synthetic samples suitable for downstream analysis.

---

## Dataset

- **Source:** UCI Machine Learning Repository  
- **Dataset:** Cleveland Heart Disease  
- **Samples after preprocessing:** 297  
- **Number of features:** 14  
- **Target variable:** Binary heart disease indicator  
  - `0` — No heart disease  
  - `1` — Presence of heart disease  

Missing values originally represented by `"?"` were removed during preprocessing.

---

## Methodology

### Data Preprocessing
- Removed records containing missing values  
- Converted all features to numeric format  
- Converted the target variable into a binary classification task  
- Identified categorical and continuous features for CTGAN training  

**Categorical features**
sex, cp, fbs, restecg, exang, slope, ca, thal, target

**Continuous features**
age, trestbps, chol, thalach, oldpeak


---

### Model
- **Architecture:** Conditional Tabular GAN (CTGAN)  
- Designed to model mixed-type tabular data  
- Uses conditional sampling to capture dependencies between features  

**Training configuration**
- Epochs: 800  
- Batch size: 500  

---

### Synthetic Data Generation
- Generated 1000 synthetic samples after training  
- Preserved the original feature schema and data types  

---

## Evaluation

Synthetic data quality was evaluated using **TableEvaluator**, focusing on:
- Feature-wise distribution similarity  
- Correlation structure preservation  
- Categorical value frequency comparison  

The evaluation highlights important trade-offs between data utility, privacy preservation, and evaluation limitations in synthetic medical data generation.

---

## Observation

- The log-scale comparison of feature-wise means and standard deviations shows that most synthetic features lie close to the diagonal, indicating strong agreement between real and synthetic data statistics. This suggests that CTGAN successfully captures the first- and second-order moments of the original data distribution.

![Mean and Std Comparison](results/mean_and_std.png)

- For continuous variables such as age, trestbps, chol, and thalach, the cumulative distribution functions (CDFs) of synthetic data closely follow those of the real data. Minor deviations are observed in the tails, which is expected given the limited size of the original dataset.

!(results/cummulative_sums.png)

!(results/distribution.png)

- The correlation structure of the synthetic dataset closely resembles that of the real dataset,
suggesting that inter-feature dependencies are largely preserved. Minor attenuation of strong
correlations is observed, reflecting a trade-off between realism and privacy preservation.

!(results/distribution2.png)

****

---

## Results

- Synthetic data closely matches real data distributions across most features  
- Correlation patterns are largely preserved  
- CTGAN performs effectively on small, mixed-type medical datasets  
- Results suggest synthetic data can support exploratory analysis and data augmentation

---


