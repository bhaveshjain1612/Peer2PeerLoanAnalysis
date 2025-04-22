## 1 | Project at a Glance
This capstone applies a full CRISP‑DM pipeline to LendingClub’s 2014‑15 open‑loan data, walking from raw data ingestion through exploratory analysis, ML‑driven default/return prediction, and finally portfolio optimisation. All work is contained in three Jupyter notebooks—one for each update—plus slide decks used for class presentations.

| Phase | Notebook | Slide deck | Key deliverable |
|-------|----------|-----------|-----------------|
| Update 1 | [Code](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part1_code.ipynb) | [Presentation](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part1_presentation.ipynb) | Cleaned dataset, EDA, K‑means + PCA |
| Update 2 | [Code](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part2_code.ipynb) | [Presentation](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part2_presentation.ipynb) | Classification & return‑regression models |
| Update 3 | [Code](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part3_code.ipynb) | [Presentation](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/Part3_presentation.ipynb) | Integer‑programmed optimal portfolio & sensitivity tests |

An example output—the 100‑loan, risk‑balanced portfolio—is saved as [Portfolio.csv](https://github.com/bhaveshjain1612/Peer2PeerLoanAnalysis/blob/main/optimized_loan_portfolio.csv).

---

## 2 | Key Objectives
1. **Maximise risk‑adjusted return** for retail investors using publicly available P2P‑loan data.  
2. **Compare modelling strategies** (grade‑only, ML default, ML return) versus optimised selection.  
3. **Demonstrate end‑to‑end analytics** skills: data cleaning → feature engineering → ML → operations research.

---

## 3 | Methodology Overview
### 3.1 Data & Feature Engineering  
* Download 2014‑15 LendingClub CSVs and the official data dictionary.  
* Engineer three realised‑return metrics (optimistic, pessimistic, mid‑rate) and borrower‑level credit attributes.  
* Impute / clean fields, then persist an analysis‑ready `.pkl`.

### 3.2 Exploratory Analysis  
* K‑means (auto‑k via elbow / silhouette) to approximate LendingClub grades; validated visually in the Update 1 deck.  
* PCA on numeric fields to compress variance into interpretable components.

### 3.3 Predictive Modelling  
* **Default classification:** down‑sampled logistic regression & decision tree; signal‑leakage prevention by omitting post‑issue variables.  
* **Return regression:** Lasso / Ridge and Boosting on application‑time features to predict net IRR.
* **Recovery regression:** Lasso / Ridge and Boosting on application‑time features to predict recovery in case of a default.

### 3.4 Prescriptive Optimisation  
* Assign each loan a *risk* = σ(return) of its cluster; derive *expected return* from the regression.  
* Formulate a 0‑1 integer program (multi‑knapsack / Markowitz analogue) in Gurobi to:  
  * Maximise Σ expected return  
  * Subject to budget, grade‑mix, and per‑cluster allocation caps.  
* Sensitivity tests on portfolio size and budget are illustrated in Update 3.

---

## 4 | Result
* Key impact is the creation of a user-based portfolio optimisation that takes inputs such as:
  - Budget
  - Max number of loans
  - The maximum portion of the budget that can go in a single loan
  - The maximum portion of a single loan that can be funded
* A methodology that consistently outperforms compared to random investing or investing just based on estimated returns

## 5 | Key Issues
* Data being limited to 2014-15 only for lending case limits the current deployment of a real-time solution
