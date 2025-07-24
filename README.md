# Remaining Useful Life (RUL) Prediction using Transformer and BiLSTM Models

This project explores predictive maintenance by estimating the Remaining Useful Life (RUL) of aircraft engines using deep learning models. Two architectures were evaluated on the complex **NASA CMAPSS FD004** dataset: a **Transformer** and a **Bidirectional LSTM (BiLSTM)**. The Transformer model achieved the best performance.

---

## 📌 Problem Statement

* **Dataset:** NASA CMAPSS FD004
* **Engines:** 248 (train), 249 (test)
* **Fault Modes:** 2 (HPC degradation and Fan degradation)
* **Operational Conditions:** 6 unique profiles
* **Objective:** Predict Remaining Useful Life (RUL) for engines in unseen test data

---

## ⚙️ Data Preprocessing

* **Normalization:** StandardScaler applied to all 24 features
* **Features:**

  * 3 operational settings
  * 21 sensor readings
* **Windowing Strategy:**

  * Sliding window of 30 time steps (stride = 1)
  * Input shape: `(batch_size, 30, 24)`
* **RUL Label Clipping:**

  * Maximum capped at 125 cycles to avoid bias toward high RULs

---

## 🧠 Model Architectures

### 🔹 Transformer

* Input Shape: `(batch_size, 30, 24)`
* Layers:

  * 3 Transformer Encoder layers
  * 4 Attention Heads per layer
* Hyperparameters:

  * `d_model = 64`, `dim_feedforward = 128`
  * Dropout: 0.1

### 🔹 BiLSTM

* Input Shape: `(batch_size, 30, 24)`
* Layers:

  * 2 BiLSTM layers with 64 hidden units
* Dropout: 0.2

---

## 🏋️ Training Configuration

* **Train/Validation Split:** 80/20 random split on windowed data
* **Loss Function:** Mean Squared Error (MSE)
* **Optimizer:** Adam (`learning_rate = 0.001`)
* **Batch Size:** 128
* **Epochs:** 30
* **Early Stopping:** Patience of 5 epochs

---

## 📊 Evaluation Metrics (Test Set)

**Best Model: Transformer**

* ✅ **MAE:** 22.49 cycles
* ✅ **RMSE:** 29.70 cycles
* ✅ **R² Score:** 0.7032

### 📈 Plot: Predicted vs True RUL

---

## 📁 Repository Structure

```
.
├── data/                # Preprocessed or raw CMAPSS data
├── models/              # Saved Transformer/BiLSTM models
├── notebooks/           # Model training and evaluation notebooks
└── README.md            # Project overview (you are here)
```

---

## 🧠 Key Learnings & Reflections

* The **Transformer outperformed BiLSTM** on the complex FD004 dataset due to better long-range dependency modeling.
* BiLSTM suffered from **overfitting** and struggled to generalize.
* Saturation in RUL predictions above 120 cycles was observed due to **data imbalance**.
* Visuals show the model is particularly reliable in **low RUL regions**, which is critical for maintenance planning.

---

## 🔮 Future Improvements

* Add a **CNN + LSTM hybrid** model
* Explore **attention visualization** for interpretability
* Try **uncertainty estimation** (e.g., MC Dropout) for confidence bounds on RUL

---




---

## 📬 Contact

If you have any questions or feedback, feel free to reach out at \[[your.email@example.com](mailto:your.email@example.com)] or open an issue in the repo.
