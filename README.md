# Manifold# DA5401 A5 — Visualizing Data Veracity Challenges in Multi-Label Classification

### 📘 Course: Data Analytics (DA5401)
### 🧑‍💻 Student: Robin
### 🗓️ Assignment: A5 — Manifold Visualization

---

## 🧭 Objective
This assignment explores **data veracity issues** in real-world machine learning, focusing on **multi-label classification** using the **Yeast dataset**.  
By applying **t-SNE** and **Isomap**, we visualize how noisy labels, outliers, and ambiguous samples appear in high-dimensional gene expression data.  
The goal is to understand how data structure and manifold complexity affect model performance.

---

## 🧪 Dataset
**Dataset:** Yeast Dataset (from MULAN Repository)  
- **Features (X):** 103 gene expression attributes  
- **Labels (Y):** 14 functional categories (multi-label targets)  
- Each instance represents a biological experiment or gene product.

**Source:**  
[MULAN Repository – Yeast Dataset](http://mulan.sourceforge.net/datasets-mlc.html)

---

## 🧩 Assignment Breakdown

### **Part A — Preprocessing and Initial Setup (10 pts)**
1. **Data Loading:** Loaded Yeast dataset (`yeast.arff`) using `scipy.io.arff`.  
2. **Dimensionality Check:** Verified shape → 86 features × *n* samples.  
3. **Label Simplification:** Created a simplified target for visualization:
   - Two most frequent single-label classes  
   - The most common multi-label combination  
   - All other samples labeled as “Other”  
4. **Scaling:** Applied `StandardScaler` to standardize features before applying distance-based algorithms.  
   - *Rationale:* t-SNE and Isomap rely on Euclidean/geodesic distances, so unscaled features distort results.

---

### **Part B — t-SNE and Veracity Inspection (20 pts)**
1. **Implementation:** Applied t-SNE on `X_scaled` with different perplexities (5, 30, 50, 100).  
2. **Visualization:** Colored points by the simplified `Viz_Label` variable.  
3. **Veracity Analysis:**  
   - **Inconsistent / noisy samples:** 249 (black `x`)  
   - **Outliers:** 25 (red `*`)  
   - **Ambiguous samples:** 209 (yellow hollow circles)  

   Each was interpreted through neighborhood-purity, label entropy, and distance heuristics.

---

### **Part C — Isomap and Manifold Learning (20 pts)**
1. **Implementation:** Applied Isomap (2D, n_neighbors=10) to preserve global manifold geometry.  
2. **Comparison with t-SNE:**  
   - **t-SNE** preserves *local* structure (tight, well-separated clusters).  
   - **Isomap** preserves *global* relationships (cluster positioning reflects global distances).  
3. **Manifold Curvature Discussion:**  
   - The Isomap plot suggests a **curved, complex manifold**.  
   - Such complexity indicates non-linear class boundaries → higher classification difficulty.  
   - Models must capture non-linear interactions to achieve high accuracy.

---

## 🧠 Key Insights
- High-dimensional biological data often lies on a **non-linear manifold** with overlapping categories.  
- **Noisy or ambiguous labels** can arise from biological continua or annotation errors.  
- **t-SNE** highlights local structure and potential mislabels.  
- **Isomap** reveals global relationships and overall manifold curvature.  
- Understanding these structures is essential for designing robust, uncertainty-aware classifiers.

---

## ⚙️ Requirements
**Python Libraries**
```bash
pip install numpy pandas scipy scikit-learn matplotlib seaborn
