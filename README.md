
# ConvLSTM Reproduction and Experimental Study

This repository contains an implementation and experimental analysis of the **Convolutional LSTM (ConvLSTM)** model proposed in:

**Shi et al., 2015 — "Convolutional LSTM Network: A Machine Learning Approach for Precipitation Nowcasting"**

The goal of this project was to reproduce the ConvLSTM architecture from scratch, perform systematic experiments, and analyze its behavior for spatiotemporal sequence prediction.

---

# Methodology

The project followed a **two-stage workflow**:

## Stage 1 — Fast Experiments

Short training runs were conducted to test multiple configurations:

- Kernel size variations
- Teacher forcing schedules
- Peephole vs no-peephole connections
- Loss weighting strategies

These experiments helped identify the best-performing configuration before long training.

---

## Stage 2 — Final Training

The optimized configuration was used to train a final ConvLSTM model.

Key model parameters:

- ConvLSTM Layers: 2  
- Kernel Size: 5×5  
- Hidden Channels: 16, 32  
- Prediction Horizon: 10 frames  
- Training Epochs: 40  

---

# Key Results

## Fast Experiment Performance

| Configuration | Val MSE | Val SSIM |
|---------------|----------|-----------|
| no_peephole | 0.042698 | 0.348966 |
| alpha_half | 0.050987 | 0.377354 |
| baseline_k3 | 0.045361 | 0.316730 |
| tf_slow_decay | 0.059350 | 0.246676 |

Best configuration:

**no_peephole**

---

## Kernel Size Comparison

| Kernel Size | Validation Loss |
|--------------|----------------|
| 1×1 | 0.2919 |
| 3×3 | 0.2301 |
| 5×5 | 0.2253 |

Observation:

Larger kernels improved prediction accuracy by increasing spatial receptive field.

---

# Observations

Key findings from experiments:

- Larger convolution kernels improve prediction accuracy
- Removing peephole connections improved training stability
- Prediction error increases gradually across time horizon
- ConvLSTM successfully captures motion dynamics

These results align with trends reported in the original ConvLSTM paper.

---

# Requirements

Typical dependencies:
Python 3.x
PyTorch
NumPy
Matplotlib
scikit-image


---

# Reference

Shi, X., Chen, Z., Wang, H., Yeung, D., Wong, W., Woo, W.  
**Convolutional LSTM Network: A Machine Learning Approach for Precipitation Nowcasting**  
NeurIPS, 2015.
