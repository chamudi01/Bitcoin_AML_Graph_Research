# 🔗 Graph-Theoretical Feature Analysis for Illicit Transaction Detection in Bitcoin Networks

### Graph Theory | Bitcoin Transaction Networks | Machine Learning | Financial Crime Detection

A research-based project investigating whether **graph-theoretical features improve illicit Bitcoin transaction detection** when combined with existing transaction features.

Using the real-world **Elliptic Bitcoin Transaction Dataset**, this project analyzes Bitcoin transaction networks, extracts structural graph features, and evaluates three Random Forest classifiers using a chronological train-validation-test split.

The research also investigates **temporal performance changes**, feature redundancy, and the limitations of graph-based transaction classification.

---

## 🎯 Research Objective

**Research Question:**

> Can explicitly engineered graph-theoretical features improve illicit Bitcoin transaction detection beyond the original transaction features under chronological evaluation?

The project focuses on:

- Constructing and analyzing a directed Bitcoin transaction network.
- Extracting graph-theoretical features to describe transaction relationships.
- Comparing original, graph-only, and combined feature sets.
- Evaluating classification performance on future time periods.
- Investigating temporal instability and graph feature importance.

## 📊 Dataset

**Dataset:** [Elliptic Bitcoin Transaction Dataset](https://www.kaggle.com/datasets/ellipticco/elliptic-data-set)

| Dataset Property | Value |
|---|---:|
| Total Transactions | 203,769 |
| Directed Edges | 234,355 |
| Time Steps | 49 |
| Original Features | 165 |
| Illicit Transactions | 4,545 |
| Licit Transactions | 42,019 |
| Unknown Transactions | 157,205 |

Only labeled transactions were used for supervised learning. All transactions were retained during graph construction to preserve the network structure.

## 🧠 Methodology

The project follows six main stages:

**1. Data Understanding and Preprocessing**

- Loaded and validated transaction features, class labels, and directed edges.
- Analyzed class imbalance and temporal distributions.
- Checked data integrity, missing values, and transaction identifiers.

**2. Graph Construction and Analysis**

Constructed a directed graph using NetworkX:

- **Nodes:** Bitcoin transactions
- **Edges:** Directed transaction relationships

Analyzed node degrees, connected components, PageRank, and network connectivity.

**3. Graph Feature Engineering**

Extracted seven graph-theoretical features:

| Feature | Purpose |
|---|---|
| In-Degree | Measures incoming connections |
| Out-Degree | Measures outgoing connections |
| Total Degree | Measures overall connectivity |
| Degree Difference | Captures directional connectivity differences |
| Degree Ratio | Describes the balance of incoming and outgoing connections |
| Component Size | Measures weakly connected component size |
| Scaled PageRank | Measures relative structural importance |

**4. Chronological Data Splitting**

To evaluate performance on future time periods:

| Dataset | Time Steps | Samples |
|---|---|---:|
| Training | 1–34 | 29,894 |
| Validation | 35–41 | 7,829 |
| Testing | 42–49 | 8,841 |

**5. Machine Learning Experiments**

Trained three Random Forest models:

- **Baseline:** 165 original dataset features
- **Graph-only:** 7 engineered graph features
- **Combined:** 172 original and graph features

All models used consistent hyperparameters, class-weight balancing, and validation-based threshold selection.

**6. Temporal Robustness and Ablation Analysis**

- Analyzed performance across individual time steps.
- Investigated graph feature redundancy.
- Compared different graph feature combinations.
- Examined the influence of component size and temporal variation.

## 📈 Experimental Results

### Test Set Performance

| Metric | Baseline | Graph-only | Combined |
|---|---:|---:|---:|
| Precision | **0.9272** | 0.0342 | **0.9272** |
| Recall | **0.4681** | 0.3284 | **0.4681** |
| F1-Score | **0.6221** | 0.0619 | **0.6221** |
| Average Precision (AP) | **0.5479** | 0.0369 | 0.5470 |
| ROC-AUC | **0.8569** | 0.3676 | 0.8522 |

### Key Research Findings

**1. Original Features Outperformed Graph-Only Features**

The Baseline achieved an Average Precision of **0.5479**, while the Graph-only model achieved **0.0369**.

**2. Adding Graph Features Did Not Improve Test Performance**

The Combined model achieved the same precision, recall, and F1-score as the Baseline, with slightly lower AP and ROC-AUC.

**3. Significant Temporal Performance Variation**

Baseline Average Precision decreased from **0.9304 on validation** to **0.5479 on testing**.

**4. Detection Performance Was Concentrated in One Time Period**

Of the 191 illicit transactions correctly detected by the Baseline model, **188 were detected at time step 42**.

**5. Structural Differences Did Not Guarantee Predictive Improvement**

Although several graph features showed statistically significant differences between licit and illicit transactions, they did not provide additional predictive value in the Combined model.

### Research Conclusion

> The experiments demonstrate that the seven selected graph-theoretical features did not improve illicit Bitcoin transaction detection beyond the original Elliptic features under chronological evaluation. The findings also highlight substantial temporal instability, emphasizing the importance of evaluating financial crime detection models across different time periods.

## 🛠️ Technologies Used

| Category | Technologies |
|---|---|
| Programming | Python |
| Data Processing | Pandas, NumPy |
| Graph Analysis | NetworkX |
| Machine Learning | Scikit-learn, Random Forest |
| Visualization | Matplotlib, Seaborn |
| Statistical Analysis | SciPy |
| Development | Jupyter Notebook, VS Code |
| Model Storage | Joblib |

## 📁 Project Structure

```text
Graph-Theoretical-Bitcoin-Detection/
│
├── data/
│   ├── raw/                      # Original Elliptic dataset
│   └── processed/                # Prepared datasets
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_graph_analysis.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_model_experiments.ipynb
│   ├── 05_results_visualization.ipynb
│   └── 06_final_research_findings.ipynb
│
├── outputs/
│   ├── figures/                  # Research visualizations
│   ├── tables/                   # Experimental results
│   └── models/                   # Trained classifiers
│
├── README.md
└── .gitignore
```

## ⚠️ Research Limitations

- Experiments were conducted using one dataset and Random Forest classifiers.
- The original Elliptic features already contain neighborhood-aggregated information.
- The engineered graph features were calculated from completed time-step networks, making the analysis retrospective rather than real-time.
- Model performance varied substantially across time periods.
- The findings apply to the evaluated feature sets and experimental configuration, rather than all graph-based detection approaches.

## 🔮 Future Improvements

- Explore advanced graph features and multi-hop neighborhood relationships.
- Investigate Graph Neural Networks and graph embeddings.
- Develop time-aware graph learning approaches.
- Improve robustness under changing transaction distributions.
- Evaluate alternative models and imbalance-handling strategies.

## 📚 References

1. M. Weber *et al.*, "Anti-Money Laundering in Bitcoin: Experimenting with Graph Convolutional Networks for Financial Forensics," 2019. [Paper](https://arxiv.org/abs/1908.02591).
2. L. Akoglu, H. Tong, and D. Koutra, "Graph-Based Anomaly Detection and Description: A Survey," *Data Mining and Knowledge Discovery*, vol. 29, pp. 626–688, 2015.
3. Elliptic, [Elliptic Bitcoin Transaction Dataset](https://www.kaggle.com/datasets/ellipticco/elliptic-data-set).

---

### ⭐ Project Highlight

This research emphasizes an important lesson in graph-based machine learning:

**More features do not always lead to better predictions. Understanding network structure, measuring actual predictive value, and testing temporal robustness are equally important.**

*Developed as an academic Graph Theory research project using real-world Bitcoin transaction network data.*
