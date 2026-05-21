# 🧬 Deciphering the LIN28A-mediated Immune Evasion Code via Machine Learning

## 📌 Project Overview & Hypothesis
본 프로젝트는 논문 [**"LIN28A Is a Suppressor of ER-Associated Translation in Embryonic Stem Cells" (GSE37114)**]의 전사체 및 번역체 빅데이터를 기반으로 진행하는 **나만의 분석(Your Own Analysis)** 프로젝트입니다. 

### 💡 Core Hypothesis
> **"줄기세포 및 암세포는 LIN28A 단백질을 이용해 세포막 면역 단백질(MHC class I 등) 및 분비 단백질의 번역을 선택적으로 억제함으로써 몸의 면역계로부터 자신을 숨긴다(Immune Evasion/스텔스 기능). 이때 LIN28A는 mRNA 서열 전반에 흐르는 '코돈 편향성(Codon Bias)'과 국소적인 '결합 모티프(Motif)'라는 서열 암호를 조합하여 타겟 유전자를 식별할 것이다."**

---

## 🎯 Project Goals
1. **생물학적 현상 규명 (Biological Validation):** `Lin28a`를 제거(Knockdown)했을 때, 일반 유전자군에 비해 **면역 관련 및 세포막/분비 단백질 유전자군의 번역 효율(Translation Efficiency, TE)**이 통계적으로 유의미하게 폭발적으로 증가하는지 데이터로 증명합니다.
2. **서열 특징 분석 (Feature Analysis):** LIN28A 타겟 유전자들이 가지는 독특한 서열 패턴(**코돈 사용 빈도, GC 비율, 결합 모티프 개수**)을 추출하고 상관관계를 규명합니다.
3. **머신러닝 분류 모델 구축 (Predictive Modeling):** 오직 유전자의 mRNA 서열 정보(X)만 입력하면, 해당 유전자가 LIN28A에 의해 번역이 통제되는 타겟(Y)인지 아닌지를 80% 이상의 정확도로 맞추는 **인공지능 타겟 예측기(Target Predictor)**를 개발합니다.

---

## 📅 3-Week Project Timeline & Deliverables

### 🛠️ Week 1: Data Alignment & Master Feature Table Construction
* **목표:** 기존 실습 환경에 준비된 전처리 데이터(`read-count.txt` 및 CLIP-seq 파일)를 로드하고, 이를 유전자 서열 데이터와 결합하여 머신러닝 학습을 위한 통합 마스터 테이블(Master Dataframe)을 구축합니다.
* **주요 세부 과제:**
  1. **로컬 데이터 로드:** `read-count.txt` 파일을 Pandas로 읽어 들여 유전자별 RNA-seq 및 Ribo-seq 카운트 데이터 구조 파악
  2. **번역 효율(TE) 산출:** 전사량(RNA) 대비 실제 번역량(Ribo)의 비율을 계산하여 LIN28A Knockdown 시 번역 변화량($\Delta$TE) 도출
  3. **면역/세포막 타겟 라벨링:** 유전자 이름(Gene Symbol) 매칭 혹은 키워드 필터링을 통해 면역(Immune) 및 세포막(Membrane) 유전자군을 분류하고 목적 변수(`is_immune`, `is_target`) 생성
  4. **서열 기반 피처 엔지니어링:** `lin28a-clip-seq.pileup` 데이터와 유전자 서열을 연동하여, 유전자별 기초 서열 특성(GC 비율, `GGAG` 결합 모티프 개수)을 계산하고 표에 결합
* **Commit Artifacts:** `data_preprocessing.ipynb`, `processed_master_table.csv`

### 📊 Week 2: Exploratory Data Analysis & Multidimensional Visualization
* **목표:** 가설을 다각도로 시각화하여 생물학적으로 증명하고, 머신러닝에 사용할 핵심 특징(Feature)을 정제합니다.
* **주요 세부 과제 (Outputs):**
  * **Figure 1 (Box/Violin Plot):** 대조군(WT) 대비 `Lin28a` Knockdown 시 일반 유전자 vs 면역/세포막 유전자의 번역 효율 변화량($\Delta$TE) 분포 시각화
  * **Figure 2 (Heatmap / PCA Plot):** LIN28A에 의해 조절되는 유전자군과 일반 유전자군 간의 **64개 코돈 편향성(Codon signature)** 패턴 차이 분석
  * **Figure 3 (Scatter Plot):** LIN28A 결합 세기(CLIP Peak)와 mRNA 서열의 특성(GC content, 모티프 밀도) 간의 상관관계 도출
* **Commit Artifacts:** `exploratory_data_analysis.ipynb`, `figures/` (PNG 파일들)

### 🤖 Week 3: Machine Learning Modeling & Model Interpretation
* **목표:** 머신러닝 분류 알고리즘을 학습시키고, 모델이 해독한 LIN28A의 번역 조절 암호를 분석합니다.
* **주요 세부 과제 (Outputs):**
  1. `scikit-learn` 기반의 분류 모델(Random Forest, XGBoost 등) 구축
  2. **X(Input):** 코돈 빈도(64개) + GC 비율 + 모티프 개수 / **Y(Target):** LIN28A 번역 억제 유전자 여부(Binary Classification)
  * **Figure 4 (ROC-AUC Curve):** 테스트 데이터를 활용한 모델의 최종 예측 정확도 평가 및 시각화
  * **Figure 5 (Feature Importance Bar Plot):** 모델이 예측할 때 가장 크게 기여한 서열 특징 순위 도출 (LIN28A가 어떤 코돈이나 모티프를 가장 선호했는지 해독)
3. 프로젝트 최종 레포트 작성 및 코드 정리
* **Commit Artifacts:** `machine_learning_model.ipynb`, `final_report.md`

---

## 🛠️ Tech Stack & Libraries
* **Language:** Python 3.x
* **Data Science:** Pandas, NumPy, Scikit-learn
* **Bioinformatics:** Biopython (Sequence retrieval)
* **Visualization:** Matplotlib, Seaborn
* **Version Control:** Git / GitHub