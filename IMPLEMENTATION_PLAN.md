# RNN vs Transformer Assignment - Implementation Tracker

## Student Information
- **BITS ID**: 2025AA05686
- **Name**: PRITISH JOSHI
- **Email**: 2025aa05686@wilp.bits-pilani.ac.in
- **Date Started**: 07-02-2026

---

## Configuration Decisions

| Decision | Value | Reason |
|----------|-------|--------|
| Dataset | Apple Stock (AAPL) | Stock prices - univariate time series with >1000 samples |
| Data Source | Yahoo Finance (yfinance) | Easy access, reliable historical data |
| Framework | Keras/TensorFlow | Simpler API, has `layers.MultiHeadAttention` |
| RNN Type | GRU | Fewer parameters than LSTM, faster training |
| Sequence Length | 30 days | Standard lookback for stock prediction |
| Prediction Horizon | 1 day | Single-step ahead forecasting |
| Train/Test Split | 90/10 | Temporal split, NO shuffling |
| Primary Metric | MAE | Interpretable (dollars), less sensitive to outliers |
| Epochs | 100 | Sufficient for convergence |
| Batch Size | 32 | Standard for time series |

---

## Grading Requirements Checklist (20 marks total)

### Part 2: GRU Implementation (5 marks)
- [ ] **Architecture** (2 marks): Stacked GRU with ≥2 layers
  - Critical: Must use `layers.GRU()` with `return_sequences=True` for stacking
- [ ] **Compilation** (1 mark): `model.compile(optimizer='adam', loss='mse')`
- [ ] **Training** (1 mark): Track `initial_loss` and `final_loss`
- [ ] **Metrics** (1 mark): Calculate MAE, RMSE, MAPE, R² (all >0 and valid)

### Part 3: Transformer Implementation (5 marks)
- [ ] **Positional Encoding** (1 mark): MANDATORY - must have sin/cos formula
  - Critical: `PE(pos,2i) = sin(pos/10000^(2i/d_model))`
  - Critical: `PE(pos,2i+1) = cos(pos/10000^(2i/d_model))`
- [ ] **Multi-head Attention** (2 marks): Use `layers.MultiHeadAttention(num_heads=4)`
  - Critical: `num_heads > 1` (not single-head)
- [ ] **Training** (1 mark): Track `initial_loss` and `final_loss`
- [ ] **Metrics** (1 mark): Calculate MAE, RMSE, MAPE, R² (all >0 and valid)

### Part 3 Continued: Loss Convergence (4 marks)
- [ ] **GRU Convergence** (2 marks):
  - Full marks: loss reduction ≥50%
  - Partial: loss reduction ≥20% (1 mark)
- [ ] **Transformer Convergence** (2 marks):
  - Full marks: loss reduction ≥50%
  - Partial: loss reduction ≥20% (1 mark)

### Part 4: Metrics Validation (2 marks)
- [ ] **Both models metrics valid** (2 marks): MAE>0, RMSE>0, MAPE>0, -1≤R²≤1
- [ ] **One model metrics valid** (1 mark)

### Part 5: Analysis (2 marks)
- [ ] **8+ key topics covered** (2 marks) - need depth, not just mentions:
  1. Performance comparison (specific MAE/RMSE values)
  2. RNN/GRU architecture discussion
  3. Transformer/attention architecture
  4. Long-term dependency handling
  5. Computational cost (parameters/time)
  6. Convergence behavior (loss curves)
  7. Advantages/disadvantages comparison
  8. Insights specific to stock prediction

### Part 6: Code Structure (2 marks)
- [ ] **Model definitions** (1 mark): Both GRU and Transformer models defined
- [ ] **JSON output** (1 mark): All required fields present

---

## Phase Progress Tracker

### Phase 1: Dataset Preparation ✅ COMPLETED
**Status**: Completed (100%)
**Notebook Cells Modified**: f7883103, ijjp75gtq8o, e2b9ac13, 6ae533b6, d1ljfflwrak, 6efdacdc, ea0da181, 8dlrw5io2g7, 725e3489

**Completed**:
- ✅ Load AAPL data using yfinance (10 years: 2010-2024)
- ✅ Fill metadata: `dataset_name`, `n_samples=3773`, `sequence_length=30`, etc.
- ✅ Implement `preprocess_timeseries()` - uses MinMaxScaler
- ✅ Add time series visualization
- ✅ Data quality analysis (no missing values, no outliers)
- ✅ Implement `create_sequences()` - sliding window approach
- ✅ Apply preprocessing and create sequences
- ✅ Split 90/10 temporal (NO shuffle - preserved temporal order)
- ✅ Fill: `train_samples`, `test_samples`, `train_test_ratio="90/10"`

**Key Values Set**:
- n_samples: 3773 (✓ exceeds 1000 minimum)
- sequence_length: 30
- prediction_horizon: 1
- primary_metric: MAE

**Critical Reminders**:
- ✅ Verified n_samples = 3773 ≥ 1000
- ⚠️ Must use temporal split only (no shuffling)

---

### Phase 2: GRU Implementation ✅ COMPLETED
**Status**: Completed (100%)
**Notebook Cells Modified**: 87daaa54, dk61253vqz, vgmpmjfvr4, 02ade3a8, 1678f898, fp0bjrcum3, 43dcb302, dg2vqgloo7t

**Completed**:
- ✅ Implement `build_rnn_model()` - 2 stacked GRU layers with dropout
- ✅ Create GRU model instance (64 units → 32 units → Dense output)
- ✅ Compile with Adam optimizer, MSE loss, MAE metric
- ✅ Train model (100 epochs, batch_size=32, 10% validation split)
- ✅ Track `rnn_initial_loss` and `rnn_final_loss` from history
- ✅ Implement `calculate_mape()` function
- ✅ Make predictions on test set and inverse transform to actual prices
- ✅ Calculate all 4 metrics: `rnn_mae`, `rnn_rmse`, `rnn_mape`, `rnn_r2`
- ✅ Create visualizations (loss curve, predictions vs actual, residuals)

**Architecture Decisions**:
- Layer 1: 64 units, return_sequences=True, dropout=0.2
- Layer 2: 32 units, return_sequences=False, dropout=0.2
- Output: Dense(1)
- Total layers: 2 GRU + dropouts + Dense output

**Training Configuration Rationale**:
- epochs=100: Sufficient for convergence (50-100 typical for stock data), ensures ≥50% loss reduction for full marks
- batch_size=32: Standard for ~3K samples; balances training speed vs gradient stability (16=too slow, 64=less stable)
- validation_split=0.1: Monitors overfitting without touching test set; 10% of training data = ~337 validation samples
- verbose=1: Shows progress bar per epoch for debugging and assignment output visibility

**Critical Reminders**:
- ⚠️ Track initial_loss from history.history['loss'][0]
- ⚠️ Track final_loss from history.history['loss'][-1]
- ⚠️ Use scaler.inverse_transform() before calculating metrics

---

### Phase 3: Transformer Implementation ⬜ NOT STARTED
**Status**: Not started
**Notebook Cells Modified**: None yet

**What needs to be done**:
- Implement `positional_encoding()` function with sin/cos
- Implement `build_transformer_model()` with MultiHeadAttention
- Add positional encoding to input embeddings
- Compile with Adam, MSE loss, MAE metric
- Train and track: `transformer_initial_loss`, `transformer_final_loss`, `transformer_training_time`
- Predict and inverse transform
- Calculate: `transformer_mae`, `transformer_rmse`, `transformer_mape`, `transformer_r2`
- Create visualizations

**Architecture Decisions**:
- d_model: 64
- n_heads: 4
- n_layers: 2
- d_ff: 256
- Global average pooling before output

**Critical Reminders**:
- ⚠️ MANDATORY: Must implement sin/cos positional encoding
- ⚠️ Must use MultiHeadAttention with num_heads=4 (>1)
- ⚠️ Must add positional encoding: `x = x + pos_enc`

---

### Phase 4: Model Comparison ⬜ NOT STARTED
**Status**: Not started
**Notebook Cells Modified**: None yet

**What needs to be done**:
- Create comparison DataFrame with all metrics
- Get model parameters: `model.count_params()`
- Create visualizations (side-by-side predictions, metric bars)
- Calculate loss reduction percentages

**Values to Track**:
- rnn_params vs transformer_params
- Better performing model and by how much
- Training time comparison

---

### Phase 5: Analysis Writing ⬜ NOT STARTED
**Status**: Not started
**Notebook Cells Modified**: None yet

**What needs to be done**:
- Write analysis covering 8+ key topics
- Focus on depth, not just word count
- Use specific numbers from results

**Required Topics** (need 8+):
1. Performance metrics comparison (MAE, RMSE specific values)
2. GRU architecture explanation (gates, sequential)
3. Transformer architecture (attention, parallel)
4. Long-term dependencies (attention vs gates)
5. Computational cost (parameters, time)
6. Convergence behavior (loss reduction %)
7. Advantages/disadvantages
8. Stock prediction insights

**Critical Reminders**:
- ⚠️ Guideline: 200 words (no marks deduction if exceeded)
- ⚠️ Quality matters: depth > length

---

### Phase 6: JSON Output ⬜ NOT STARTED
**Status**: Not started
**Notebook Cells Modified**: None yet

**What needs to be done**:
- Fill all architecture parameters in `get_assignment_results()`
- Set framework: "keras"
- Set model_type: "GRU"
- Set all training_config values
- Verify boolean flags: `has_positional_encoding=True`, `has_attention=True`
- Print JSON and verify structure

**Critical Fields**:
- rnn_model.architecture.n_layers = 2
- rnn_model.architecture.total_parameters = (use model.count_params())
- transformer_model.architecture.n_heads = 4
- transformer_model.architecture.has_positional_encoding = True
- transformer_model.architecture.has_attention = True

---

## Change Log

### Session 1 (2026-02-06)
**Date**: 2026-02-06
**Changes**: Planning and setup
**Files Created**:
- IMPLEMENTATION_PLAN.md (this file)
- CLAUDE.md (context loader)

**Decisions Made**:
- Dataset: Apple Stock (AAPL)
- Framework: Keras/TensorFlow
- RNN Type: GRU
- Configuration: 30-day lookback, 1-day prediction

**Template Modifications**: None yet

### Session 2 (2026-02-06) - Phase 1 Implementation
**Date**: 2026-02-06
**Changes**: Started Phase 1 - Dataset Preparation

**Cells Modified**:
1. **f7883103** (Imports): Added TensorFlow/Keras imports and yfinance
2. **ijjp75gtq8o** (NEW): Added data loading cell for AAPL stock data
3. **e2b9ac13** (Metadata): Filled dataset metadata dynamically from data
4. **6ae533b6** (Primary Metric): Set primary_metric="MAE" with justification
5. **d1ljfflwrak** (NEW): Added time series visualization plot
6. **6efdacdc** (Preprocess Function): Implemented MinMaxScaler normalization
7. **ea0da181** (Create Sequences Function): Implemented sliding window approach
8. **8dlrw5io2g7** (NEW): Applied preprocessing, created sequences, performed 90/10 temporal split
9. **725e3489** (Train/Test Info): Filled train_test_ratio, train_samples, test_samples dynamically
10. **87daaa54** (Build RNN Function): Implemented build_rnn_model() - GRU only (removed LSTM)
11. **c800bf2e** (JSON Function): Fixed rnn_model_type from "LSTM" to "GRU"
12. **dk61253vqz** (NEW): Created and compiled GRU model instance
13. **vgmpmjfvr4** (NEW): Trained GRU model (100 epochs, batch_size=32, 10% validation)
14. **02ade3a8**: Tracked initial_loss and final_loss from training history
15. **1678f898**: Implemented calculate_mape() function
16. **fp0bjrcum3** (NEW): Made predictions on test set and inverse transformed to actual prices
17. **43dcb302**: Calculated all 4 metrics (MAE, RMSE, MAPE, R²)
18. **dg2vqgloo7t** (NEW): Created 3 visualizations (loss curve, predictions vs actual, residuals)

**Values Set**:
- dataset_name: "Apple Inc. (AAPL) Stock Prices"
- dataset_source: "Yahoo Finance (yfinance API)"
- n_samples: 3773 (from len(data))
- sequence_length: 30
- prediction_horizon: 1
- primary_metric: "MAE"

**Decisions Made**:
- Data range: 2010-2024 (10 years) instead of 5 years → 3773 samples (better model training)
- Data quality verified: No missing values, no outliers, clean data
- Normalization: MinMaxScaler with range [0,1] chosen because:
  * Standard choice for time series + neural networks
  * No outliers in data (verified via IQR analysis)
  * Stock prices are positive (bounded data)
  * [0,1] range optimal for neural network activation functions
  * Easier inverse transform for predictions back to dollar values
  * Alternative considered: StandardScaler (would work but produces unbounded negative values)
- RNN Model: GRU chosen over LSTM because:
  * Stock data has short-term dependencies (30-day lookback, 1-day prediction)
  * Fewer parameters → less overfitting on noisy stock data
  * Faster training → better convergence for our use case
  * Research shows GRU performs as well or better than LSTM on financial time series
  * Simpler gating mechanism is more robust for noisy data

**Status**: Phase 1 is 60% complete. Next: implement create_sequences() and train/test split

---

## Auto-Fail Conditions (VERIFY BEFORE SUBMISSION)

- [ ] Filename is `2025AA05686_rnn_assignment.ipynb`
- [ ] BITS ID in filename matches BITS ID in notebook (2025AA05686)
- [ ] Student name matches folder name
- [ ] All cells executed (Kernel → Restart & Run All)
- [ ] No execution errors in any cell
- [ ] All outputs visible (not cleared)
- [ ] File opens without corruption
- [ ] Positional encoding present in Transformer
- [ ] NO shuffle=True anywhere in code
- [ ] Screenshot of Colab environment included

---

## Expected Final Results

| Metric | Target |
|--------|--------|
| **Total Marks** | 18-20 / 20 |
| GRU Convergence | ≥50% loss reduction |
| Transformer Convergence | ≥50% loss reduction |
| All Metrics Valid | MAE, RMSE, MAPE, R² calculated |
| Analysis Quality | 8+ topics covered with depth |
| JSON Complete | All fields filled correctly |

---

## Notes & Observations

(Add notes here as you work through the assignment)

-
-
