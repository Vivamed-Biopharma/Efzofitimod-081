# Data Dictionary - Patent-075

## Indisulam / CDH1-Loss ILC Drug Rescue Strategy

**Document Version:** 1.0
**Last Updated:** December 29, 2025
**Patent ID:** Patent-075

---

## 1. Neurosnap Jobs

### Completed Jobs

| Job ID | Description | Drug/Ligand | Target Protein | Status | Runtime | Credits | Date |
|--------|-------------|-------------|----------------|--------|---------|---------|------|
| `694542ee6e3da7b0c5059378` | CDH1-Entinostat-HDAC Validation | Entinostat (MS-275) | CDH1 (882 aa), HDAC7 (952 aa), HDAC9 (1011 aa) | COMPLETED | 23 min | 3.17 | 2025-12 |

### Job Details: 694542ee6e3da7b0c5059378

| Parameter | Value |
|-----------|-------|
| **Service** | Boltz-2 (AlphaFold3) |
| **MSA Mode** | mmseqs2_uniref_env |
| **Diffusion Samples** | 5 |
| **Sampling Steps** | 200 |
| **Number of Recycles** | 5 |
| **Ligand SMILES** | `Nc1ccccc1NC(=O)c1ccc(CNC(=O)OCc2cccnc2)cc1` |
| **Ligand Identity** | Entinostat (NOT Indisulam - wrong drug for patent) |
| **Local Path** | `/Users/nharris/Documents/GitHub/atlas-repos/Patent-075/neurosnap_data/694542ee6e3da7b0c5059378/` |

### Output Files (Job 694542ee6e3da7b0c5059378)

**Note:** Only metadata files were downloaded locally. Structure output files remain on Neurosnap servers.

| File | Size | Description | Status |
|------|------|-------------|--------|
| `job_record.json` | 392 bytes | Job metadata | Downloaded |
| `job_data.json` | 4.1 KB | Job configuration | Downloaded |
| `rank_1.cif` | 1.88 MB | Top-ranked structure prediction | NOT DOWNLOADED |
| `rank_2.cif` | 1.72 MB | Second-ranked structure | NOT DOWNLOADED |
| `rank_3.cif` | 1.72 MB | Third-ranked structure | NOT DOWNLOADED |
| `rank_4.cif` | 1.72 MB | Fourth-ranked structure | NOT DOWNLOADED |
| `rank_5.cif` | 1.72 MB | Fifth-ranked structure | NOT DOWNLOADED |
| `affinity.json` | 342 bytes | Binding affinity predictions | NOT DOWNLOADED |
| `scores.json` | 694.85 MB | Full confidence metrics | NOT DOWNLOADED |
| `msa_A.a3m` | 10.48 MB | Multiple sequence alignment (Chain A) | NOT DOWNLOADED |
| `msa_B.a3m` | 18.03 MB | Multiple sequence alignment (Chain B) | NOT DOWNLOADED |
| `msa_C.a3m` | 16.13 MB | Multiple sequence alignment (Chain C) | NOT DOWNLOADED |

### Recommended Jobs to Submit

| Priority | Job Name | Drug | Targets | Purpose |
|----------|----------|------|---------|---------|
| P1 | Indisulam_DCAF15_RBM39_Ternary | Indisulam | DCAF15, RBM39 | Validate molecular glue mechanism |
| P2 | Indisulam_DCAF15_Binary | Indisulam | DCAF15 | Show conformational change |
| P3 | RBM39_Apo_Structure | None | RBM39 | Baseline structure |
| P4 | Indisulam_CDH1_Negative_Control | Indisulam | CDH1 | Prove Indisulam doesn't bind CDH1 |

---

## 2. Database Tables Used

### Database: bioatlas_test (PostgreSQL)

**Connection:** localhost:5432, user: nharris

#### gtex_v10_eqtl_leads

| Column | Type | Description |
|--------|------|-------------|
| tissue | VARCHAR | GTEx tissue name |
| gene_symbol | VARCHAR | Gene symbol (e.g., CDH1, DCAF15, RBM39) |
| variant_id | VARCHAR | Variant identifier (e.g., chr16_68796608_A_T_b38) |
| slope | FLOAT | Effect size (beta coefficient) |
| pval_nominal | FLOAT | Nominal p-value |
| pval_beta | FLOAT | Beta-adjusted p-value |

**Usage:** Query tissue-specific expression regulation for CDH1, DCAF15, RBM39

#### gtex_v10_eqtl_finemap

| Column | Type | Description |
|--------|------|-------------|
| tissue | VARCHAR | GTEx tissue name |
| gene_symbol | VARCHAR | Gene symbol |
| variant_id | VARCHAR | Variant identifier |
| pip | FLOAT | Posterior inclusion probability |
| cs_id | INTEGER | Credible set identifier |

**Usage:** Fine-mapped causal eQTL variants

#### biogrid_interaction

| Column | Type | Description |
|--------|------|-------------|
| gene_a | VARCHAR | Interactor A gene symbol |
| gene_b | VARCHAR | Interactor B gene symbol |
| experimental_system | VARCHAR | Detection method (e.g., Affinity Capture-Western) |
| throughput | VARCHAR | Low Throughput or High Throughput |
| pubmed_id | VARCHAR | PubMed reference ID |

**Usage:** Validate DCAF15-RBM39 and DCAF15-DDB1 protein interactions

#### clinvar_variant_summary

| Column | Type | Description |
|--------|------|-------------|
| gene_symbol | VARCHAR | Gene symbol |
| clinical_significance | VARCHAR | Pathogenic, Likely pathogenic, Benign, etc. |
| variant_type | VARCHAR | SNV, Deletion, Duplication, Indel |
| chromosome | VARCHAR | Chromosome number |
| position_vcf | INTEGER | Genomic position (GRCh38) |
| reference_allele | VARCHAR | Reference allele |
| alternate_allele | VARCHAR | Alternate allele |

**Usage:** Identify pathogenic CDH1 variants linked to ILC

#### clinvar_gene_condition

| Column | Type | Description |
|--------|------|-------------|
| gene_id | INTEGER | NCBI Gene ID |
| disease_name | VARCHAR | Associated disease/phenotype |
| relationship_type | VARCHAR | Type of gene-disease relationship |

**Usage:** Link CDH1 variants to lobular breast cancer syndrome

#### ctrp_compound

| Column | Type | Description |
|--------|------|-------------|
| master_cpd_id | INTEGER | CTRP compound ID |
| compound_name | VARCHAR | Compound name (e.g., indisulam) |
| broad_cpd_id | VARCHAR | Broad Institute compound ID (e.g., BRD-K17610631) |
| target_or_activity | VARCHAR | Listed target (e.g., CA9) |

**Usage:** Identify indisulam in CTRP database

#### ctrp_sensitivity

| Column | Type | Description |
|--------|------|-------------|
| master_cpd_id | INTEGER | CTRP compound ID |
| master_ccl_id | INTEGER | CTRP cell line ID |
| area_under_curve | FLOAT | AUC (lower = more sensitive) |
| ec50 | FLOAT | EC50 value |

**Usage:** Query indisulam sensitivity across 741 cell lines

#### ctrp_cell_line

| Column | Type | Description |
|--------|------|-------------|
| master_ccl_id | INTEGER | CTRP cell line ID |
| cell_line_name | VARCHAR | Cell line name (e.g., MCF7, BT549) |
| lineage | VARCHAR | Tissue/cancer type lineage |

**Usage:** Identify breast cancer cell lines

#### ccle_expression

| Column | Type | Description |
|--------|------|-------------|
| cell_line_id | VARCHAR | CCLE cell line identifier |
| gene_symbol | VARCHAR | Gene symbol |
| expression_tpm | FLOAT | TPM expression value |

**Usage:** Query CDH1 expression in breast cancer cell lines

#### ccle_mutation

| Column | Type | Description |
|--------|------|-------------|
| cell_line_id | VARCHAR | CCLE cell line identifier |
| gene_symbol | VARCHAR | Gene symbol |
| variant_classification | VARCHAR | Mutation type |

**Usage:** Identify CDH1 mutations in cell lines

#### ccle_cnv

| Column | Type | Description |
|--------|------|-------------|
| cell_line_id | VARCHAR | CCLE cell line identifier |
| gene_symbol | VARCHAR | Gene symbol |
| copy_number | FLOAT | Copy number value |

**Usage:** Identify CDH1 deletions in cell lines

### Database: bio_kg_full (PostgreSQL)

**Connection:** localhost:5432, user: nharris

#### l1000_compound_info

| Column | Type | Description |
|--------|------|-------------|
| pert_id | VARCHAR | Perturbation ID (e.g., BRD-K17610631) |
| pert_iname | VARCHAR | Compound name |
| smiles | VARCHAR | SMILES structure |

**Usage:** Identify indisulam in L1000 database

#### l1000_activity

| Column | Type | Description |
|--------|------|-------------|
| pert_id | VARCHAR | Perturbation ID |
| sig_id | VARCHAR | Signature ID |
| cell_id | VARCHAR | Cell line ID |
| pert_dose | FLOAT | Perturbation dose |
| zscore | FLOAT | Activity z-score |

**Usage:** Query transcriptional signatures of indisulam

#### l1000_cell_info

| Column | Type | Description |
|--------|------|-------------|
| cell_id | VARCHAR | Cell line ID |
| cell_type | VARCHAR | Cell type |
| tissue | VARCHAR | Tissue of origin |
| disease | VARCHAR | Associated disease |

**Usage:** Filter for breast cancer cell lines

#### l1000_signature

| Column | Type | Description |
|--------|------|-------------|
| sig_id | VARCHAR | Signature ID |
| cell_id | VARCHAR | Cell line ID |
| pert_type | VARCHAR | Perturbation type |

**Usage:** Link signatures to cell lines

#### drug

| Column | Type | Description |
|--------|------|-------------|
| drug_id | VARCHAR | Drug identifier |
| drug_name | VARCHAR | Drug name |
| max_phase | INTEGER | Maximum clinical phase |

**Usage:** Query drug clinical development status

#### drug_disease

| Column | Type | Description |
|--------|------|-------------|
| drug_id | VARCHAR | Drug identifier |
| disease_id | VARCHAR | Disease identifier |
| relation_type | VARCHAR | Indication type |
| max_phase | INTEGER | Clinical phase for indication |

**Usage:** Query indisulam clinical indications (breast neoplasm = Phase 2)

#### disease

| Column | Type | Description |
|--------|------|-------------|
| disease_id | VARCHAR | Disease identifier |
| disease_name | VARCHAR | Disease name |

**Usage:** Link to lobular breast carcinoma entities

---

## 3. API Endpoints

### Snaptron (GTEx v2)

| Parameter | Value |
|-----------|-------|
| **Base URL** | `http://snaptron.cs.jhu.edu/gtexv2/snaptron` |
| **Dataset** | GTEx v2 |
| **Query Format** | `?regions=chr:start-end&rfilter=...&sfilter=...` |

**Example Query (RBM39 region):**
```
http://snaptron.cs.jhu.edu/gtexv2/snaptron?regions=chr20:35620000-35680000
```

**Response Fields:**
| Field | Description |
|-------|-------------|
| snaptron_id | Junction identifier |
| chromosome | Chromosome |
| start | Junction start position |
| end | Junction end position |
| strand | + or - |
| annotated | Yes/No |
| samples_count | Number of samples with junction |
| coverage_sum | Total read coverage |

### Recount3

| Parameter | Value |
|-----------|-------|
| **Base URL** | `http://duffel.rail.bio/recount3/` |
| **Purpose** | Uniform RNA-seq quantifications |
| **Data Types** | Gene expression, exon usage, junction counts |

### DepMap Portal

| Parameter | Value |
|-----------|-------|
| **URL** | `https://depmap.org/portal/` |
| **Datasets** | PRISM, Achilles CRISPR, Cell Line Metadata |
| **Key Data** | Indisulam sensitivity (PRISM), RBM39 dependency (Achilles) |

---

## 4. Key Chemical Identifiers

### Indisulam (E7070)

| Identifier Type | Value |
|-----------------|-------|
| **SMILES (Canonical)** | `NS(=O)(=O)c1ccc(cc1)S(=O)(=O)Nc1cccc2c(Cl)c[nH]c12` |
| **InChI Key** | `CTLOSZHDGXBSIG-UHFFFAOYSA-N` |
| **CAS Number** | 165668-41-7 |
| **PubChem CID** | 216468 |
| **ChEMBL ID** | CHEMBL77517 |
| **CTRP ID** | BRD-K17610631 |
| **Molecular Formula** | C14H12ClN3O4S2 |
| **Molecular Weight** | 385.85 g/mol |

### Entinostat (MS-275) - Modeled in Neurosnap Job

| Identifier Type | Value |
|-----------------|-------|
| **SMILES** | `Nc1ccccc1NC(=O)c1ccc(CNC(=O)OCc2cccnc2)cc1` |
| **PubChem CID** | 4261 |
| **Mechanism** | HDAC inhibitor |
| **Note** | NOT relevant to patent - wrong drug modeled |

---

## 5. Key Protein Identifiers

### CDH1 (E-cadherin)

| Identifier Type | Value |
|-----------------|-------|
| **UniProt ID** | P12830 |
| **NCBI Gene ID** | 999 |
| **Ensembl Gene** | ENSG00000039068 |
| **Chromosome** | 16q22.1 |
| **Length** | 882 amino acids |
| **Function** | Calcium-dependent cell adhesion |

### DCAF15

| Identifier Type | Value |
|-----------------|-------|
| **UniProt ID** | Q66K64 |
| **NCBI Gene ID** | 90379 |
| **Ensembl Gene** | ENSG00000132017 |
| **Chromosome** | 19p13.2 |
| **Length** | 1454 amino acids |
| **Function** | E3 ligase substrate receptor |

### RBM39

| Identifier Type | Value |
|-----------------|-------|
| **UniProt ID** | Q14498 |
| **NCBI Gene ID** | 9584 |
| **Ensembl Gene** | ENSG00000131051 |
| **Chromosome** | 20q11.22 |
| **Length** | 530 amino acids |
| **Function** | Pre-mRNA splicing factor |
| **Alternative Names** | CAPERalpha, HCC1, RNPC2 |

### DDB1

| Identifier Type | Value |
|-----------------|-------|
| **UniProt ID** | Q16531 |
| **NCBI Gene ID** | 1642 |
| **Length** | 1140 amino acids |
| **Function** | CRL4 E3 ligase scaffold |

---

## 6. Clinical Trial Identifiers

### Key Trials

| NCT ID | Title | Phase | Status | Enrollment |
|--------|-------|-------|--------|------------|
| **NCT00080197** | E7070 in Metastatic Breast Cancer | Phase 2 | COMPLETED | 250 |
| NCT00014625 | E7070 in Melanoma | Phase 2 | COMPLETED | 28 |
| NCT00003976 | E7070 in Solid Tumors | Phase 1 | COMPLETED | 30 |
| NCT00060567 | E7070 + Irinotecan | Phase 1 | COMPLETED | 88 |
| NCT00059735 | E7070 in Renal Cell Carcinoma | Phase 2 | COMPLETED | 30 |
| NCT01692197 | E7070 in AML/MDS | Phase 2 | COMPLETED | 43 |

---

## 7. File Manifest

### Repository Files

| Path | Description | Size | Created |
|------|-------------|------|---------|
| `/README.md` | Repository overview | ~6 KB | 2025-12-29 |
| `/PROVISIONAL_PATENT.md` | Filing-ready patent application | ~58 KB | 2025-12-29 |
| `/DATA_DICTIONARY.md` | This file | ~12 KB | 2025-12-29 |
| `/discovery/00_DATA_DISCOVERY.md` | Initial data discovery report | ~55 KB | 2025-12-28 |
| `/discovery/01_VALIDATION.md` | Enabling data validation | ~12 KB | 2025-12-29 |
| `/neurosnap_data/694542ee6e3da7b0c5059378/` | Structural biology job metadata (output files not downloaded) | ~4.5 KB | 2025-12 |

### External Data Files Referenced

| Path | Description | Database |
|------|-------------|----------|
| `/Users/nharris/Desktop/untitled folder 4/NEUROSNAP_FINAL_MASTER_20251227_064517.csv` | Neurosnap job master list | Local |
| `/Users/nharris/Documents/GitHub/atlas-3.0/MASTER_DRUG_RANKINGS_ALL_DISEASES.csv` | Drug repurposing rankings | Local |

---

## 8. Query Examples

### GTEx CDH1 eQTLs
```sql
SELECT tissue, gene_symbol, variant_id, slope, pval_nominal
FROM gtex_v10_eqtl_leads
WHERE gene_symbol = 'CDH1'
ORDER BY pval_nominal ASC
LIMIT 20;
```

### BioGRID DCAF15-RBM39 Interaction
```sql
SELECT gene_a, gene_b, experimental_system, throughput, pubmed_id
FROM biogrid_interaction
WHERE (gene_a = 'DCAF15' AND gene_b = 'RBM39')
   OR (gene_a = 'RBM39' AND gene_b = 'DCAF15');
```

### CTRP Indisulam Sensitivity
```sql
SELECT cc.compound_name, cl.cell_line_name, cl.lineage,
       cs.area_under_curve, cs.ec50
FROM ctrp_compound cc
JOIN ctrp_sensitivity cs ON cc.master_cpd_id = cs.master_cpd_id
JOIN ctrp_cell_line cl ON cs.master_ccl_id = cl.master_ccl_id
WHERE LOWER(cc.compound_name) LIKE '%indisulam%'
ORDER BY cs.area_under_curve ASC
LIMIT 20;
```

### ClinVar CDH1 Pathogenic Variants
```sql
SELECT cvs.gene_symbol, cvs.clinical_significance,
       cvs.variant_type, cgc.disease_name
FROM clinvar_variant_summary cvs
JOIN clinvar_gene_condition cgc ON cvs.gene_id = cgc.gene_id
WHERE cvs.gene_symbol = 'CDH1'
  AND cvs.clinical_significance LIKE '%Pathogenic%'
  AND cgc.disease_name LIKE '%breast%';
```

### L1000 Indisulam Signatures
```sql
SELECT lci.cell_id, lci.tissue, la.pert_iname, la.zscore
FROM l1000_activity la
JOIN l1000_cell_info lci ON la.cell_id = lci.cell_id
JOIN l1000_compound_info lco ON la.pert_id = lco.pert_id
WHERE LOWER(lco.pert_iname) LIKE '%indisulam%'
ORDER BY ABS(la.zscore) DESC
LIMIT 50;
```

---

## 9. Key Metrics Summary

| Metric | Value | Source |
|--------|-------|--------|
| Cell lines with indisulam data | 741 | CTRP |
| Breast cancer cell lines | 11 | CTRP |
| DCAF15-RBM39 PPI validations | 2 | BioGRID |
| DCAF15-DDB1 PPI validations | 8 | BioGRID |
| CDH1 pathogenic variants | 11 | ClinVar |
| CDH1 eQTL tissues | 14 | GTEx v10 |
| DCAF15 eQTL tissues | 12 | GTEx v10 |
| RBM39 eQTL tissues | 7 | GTEx v10 |
| RBM39 splice junction samples | 716 | Snaptron |
| Completed indisulam trials | 10 | AACT |
| Breast cancer trial enrollment | 250 | NCT00080197 |
| Total Neurosnap jobs searched | 7,576 | Local CSV |

---

**CONFIDENTIAL - PATENT PENDING - DO NOT DISTRIBUTE**

*All data validated from local PostgreSQL databases (bioatlas_test, bio_kg_full), Snaptron API, and local Neurosnap job archives. Last query date: December 29, 2025.*
