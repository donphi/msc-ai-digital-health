---
title: Multi PRS Models (Note)
source: https://chatgpt.com/c/672805d1-a278-8002-b029-3c6a6de9a75a
---

# Multi PRS Models (Note)

#### You:
[Unsupported Content]

#### You:
<time datetime="2024-11-03T23:22:57.746Z" title="11/3/2024, 11:22:57 PM">23:22</time>

What are multi PRS models

#### ChatGPT:
<time datetime="2024-11-03T23:23:02.222Z" title="11/3/2024, 11:23:02 PM">23:23</time>

Multi-PRS (Polygenic Risk Score) models are analytical tools that integrate multiple PRS calculations across different genetic markers or traits to predict complex diseases or traits more accurately. Instead of relying on a single PRS, these models combine multiple PRS related to different genetic risk factors or traits, potentially increasing predictive power and accuracy by accounting for the polygenic nature of many diseases.

The advantage of multi-PRS models is that they allow for a more nuanced understanding of genetic risk by layering multiple risk scores, which may capture different aspects of genetic susceptibility. For instance, in predicting cardiovascular disease risk, a multi-PRS model might incorporate PRS for cholesterol levels, blood pressure, inflammation markers, and other relevant traits.

Multi-PRS models are especially useful in precision medicine, where they can aid in assessing an individual’s likelihood of developing certain diseases based on a broader range of genetic influences.


#### You:
<time datetime="2024-11-03T23:24:44.911Z" title="11/3/2024, 11:24:44 PM">23:24</time>

So how would I even set tthis up in python, is how do I calculate even a single PRS, and how is this setup, what data do I need, do I need updated SNPs that contribute to disease, 

#### ChatGPT:
<time datetime="2024-11-03T23:25:13.095Z" title="11/3/2024, 11:25:13 PM">23:25</time>

To set up and calculate a Polygenic Risk Score (PRS) in Python, especially if you’re looking into multi-PRS models, there are several key steps and data requirements. Here’s a structured outline of what you’d need:

### 1. **Data Requirements**

- **Genotype Data:** You’ll need a list of single nucleotide polymorphisms (SNPs) for each individual, typically from a dataset like a `.vcf` or `.bam` file, or an array of SNP values in a structured file format.
- **List of SNPs Contributing to Disease:** This is crucial for a meaningful PRS. You need a list of SNPs associated with the disease of interest and their effect sizes (typically from genome-wide association studies, or GWAS). Effect sizes can be odds ratios or beta coefficients and are usually found in public resources like the NHGRI-EBI GWAS Catalog or recent relevant publications.
- **Phenotype Data (Optional):** For multi-PRS models, you might want phenotype data to validate or calibrate your scores against actual disease outcomes or trait values.

### 2. **Calculating a Single PRS**

A PRS is generally calculated as the sum of effect sizes for risk alleles weighted by the number of risk alleles an individual has. Here’s a simplified step-by-step approach:

- **Step 1: Load Genotype and SNP Data**
  Load the individual’s genotype data and SNP effect sizes.

- **Step 2: Align SNPs with Effect Sizes**
  Match the SNPs in your genotype data with the effect sizes in your SNP list, ensuring they’re on the same strand orientation.

- **Step 3: Score Calculation**
  For each SNP, multiply the number of risk alleles by the effect size. Sum up these weighted values to get a single PRS.

Here’s a simple Python example to compute a single PRS:

```python
import pandas as pd

# Load genotype and effect size data
genotype_data = pd.read_csv("genotype_data.csv")  # Your genotype data with SNP and allele count
effect_sizes = pd.read_csv("effect_sizes.csv")  # SNP, effect size columns

# Merge data on SNP column
prs_data = pd.merge(genotype_data, effect_sizes, on="SNP")

# Calculate PRS
prs_data['weighted_score'] = prs_data['allele_count'] * prs_data['effect_size']
prs_score = prs_data['weighted_score'].sum()
print("Single PRS Score:", prs_score)
```

This is a basic approach; in reality, you may need to account for dosage data, imputed SNPs, or quality control steps.

### 3. **Setting Up a Multi-PRS Model**

Multi-PRS models involve layering or combining multiple PRS calculations. Here are the steps:

- **Step 1: Define Traits/Diseases for PRS**
  Determine the multiple traits or disease-associated PRS scores you need to calculate. For example, if you’re studying cardiovascular disease, you might calculate separate PRS for blood pressure, cholesterol, and inflammation markers.

- **Step 2: Repeat Single PRS Calculation for Each PRS**
  For each trait or disease, repeat the PRS calculation process. You can store each calculated PRS in a dictionary or a new DataFrame column for further analysis.

- **Step 3: Combine Scores**
  Combine these individual PRS scores using a weighted average, sum, or even through a machine learning model if you’re developing a more complex multi-PRS prediction.

Here’s a simplified Python example:

```python
# Suppose prs_data_dict is a dictionary where each key is a trait, and each value is a DataFrame for that trait's PRS data.
prs_scores = {}
for trait, data in prs_data_dict.items():
    data['weighted_score'] = data['allele_count'] * data['effect_size']
    prs_scores[trait] = data['weighted_score'].sum()

# Combine scores, example with a weighted sum
combined_prs_score = sum(prs_scores[trait] * weight for trait, weight in trait_weights.items())
print("Combined Multi-PRS Score:", combined_prs_score)
```

### 4. **Validating and Testing Your PRS**

You might also want to validate your PRS or multi-PRS model by testing it against known cases/controls or trait values. This can involve using a sample set with known phenotypes to compare predicted risk with observed outcomes.

### 5. **Considerations on SNPs and Data Updates**

Since SNP-disease associations evolve with research, it’s essential to:

- **Stay Updated on Relevant SNPs** by regularly checking for new GWAS findings, which may introduce new SNPs or refine effect sizes.
- **Use Filters** to ensure that SNPs you include meet quality thresholds, such as minor allele frequency and imputation accuracy if you’re using imputed data.

### Useful Libraries for PRS Calculations

- **pandas:** For data manipulation.
- **scikit-allel:** For handling genetic data (if you need to process `.vcf` files directly).
- **Hail or PySnpTools:** For larger datasets and more complex genetic data handling.

Would you like a more specific example for a particular trait, or do you have specific data formats you’d like help with?


#### You:
<time datetime="2024-11-03T23:28:30.143Z" title="11/3/2024, 11:28:30 PM">23:28</time>

What is dosage data and imputed SNPs?

This is a basic approach; in reality, you may need to account for dosage data, imputed SNPs, or quality control steps.

#### ChatGPT:
<time datetime="2024-11-03T23:28:56.514Z" title="11/3/2024, 11:28:56 PM">23:28</time>

Dosage data and imputed SNPs are commonly encountered concepts in genetic studies and can impact how you calculate PRS.

### 1. **Dosage Data**

- **Definition:** Dosage data represents the probability of an individual having a specific genotype at a given SNP. Instead of directly showing a discrete genotype (like 0, 1, or 2 for the count of a risk allele), it provides a probability, reflecting uncertainty in the genotype call.
- **Use Case:** Dosage data typically appears when genotyping isn’t fully certain. For example, a SNP might have dosage values like 1.8 (meaning 80% probability of being homozygous for the risk allele) or 0.5 (50% probability of carrying one risk allele).
- **How to Use It:** In PRS calculations, dosage data is multiplied by the effect size, just like allele counts, but it provides a more nuanced score that accounts for genotype uncertainty. Here’s an example:

  ```python
  prs_data['weighted_score'] = prs_data['dosage'] * prs_data['effect_size']
  prs_score = prs_data['weighted_score'].sum()
  ```

Using dosage data can increase accuracy, especially if you have partially missing or low-confidence genotype calls.

### 2. **Imputed SNPs**

- **Definition:** Imputed SNPs are SNPs whose genotypes are inferred based on known patterns in the population, filling in gaps in genetic data. Genotyping arrays may not capture every SNP, so imputation methods predict missing SNPs based on known linkage disequilibrium (the correlation between nearby SNPs) from a reference population.
- **Why Impute:** Imputation expands the number of SNPs you can analyze, often improving the resolution of your PRS by covering more of the genome. This process is especially useful when a genotyping array doesn’t cover all SNPs related to a specific trait or disease.
- **How to Use Imputed SNPs in PRS Calculations:**
  - You would treat imputed SNPs similarly to regular SNPs but need to be cautious about their quality. Imputation usually assigns a confidence score to each imputed SNP, and researchers often filter out low-confidence SNPs.
  - Some studies exclude imputed SNPs with lower imputation quality (e.g., R² < 0.8) to ensure more reliable predictions.
  - After quality filtering, imputed SNPs can be integrated into your PRS calculation just like observed SNPs.

### Example Code for Including Dosage and Imputed SNPs in PRS

Here’s how you might adjust the PRS calculation to incorporate dosage and filter for imputed SNPs with a confidence threshold:

```python
# Load genotype data (with dosage) and effect sizes
genotype_data = pd.read_csv("genotype_data_with_dosage.csv")
effect_sizes = pd.read_csv("effect_sizes.csv")

# Merge on SNP and filter out low-confidence imputed SNPs (e.g., imputation quality < 0.8)
merged_data = pd.merge(genotype_data, effect_sizes, on="SNP")
high_confidence_data = merged_data[merged_data['imputation_quality'] >= 0.8]

# Calculate PRS using dosage
high_confidence_data['weighted_score'] = high_confidence_data['dosage'] * high_confidence_data['effect_size']
prs_score = high_confidence_data['weighted_score'].sum()
print("PRS Score with Dosage and Imputed SNP Quality Filtering:", prs_score)
```

### Quality Control Steps

For a high-quality PRS, researchers often apply quality control (QC) steps, such as:

- **SNP Filters:** Removing SNPs with low minor allele frequencies (e.g., MAF < 0.01) to avoid rare, poorly imputed SNPs.
- **Genotype Quality:** Excluding individuals or SNPs with high missingness rates or poor genotype quality.

Incorporating dosage data and imputed SNPs, while applying QC filters, generally improves the reliability of PRS, especially for larger datasets where genotype accuracy and SNP coverage can vary widely. Let me know if you’d like a specific example of QC steps or have further questions about this setup!
