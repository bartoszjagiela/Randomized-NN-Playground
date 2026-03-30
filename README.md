# Randomized Neural Network Playground

An interactive browser-based visualization tool for exploring randomized learning methods for feedforward neural networks, inspired by [TensorFlow Playground](https://playground.tensorflow.org/).

![Screenshot](https://img.shields.io/badge/status-live-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue)

## Live Demo

**[Launch Playground](https://bartoszjagiela.github.io/Randomized-NN-Playground/)**

## Overview

This tool implements and visualizes four randomized neural network training methods, allowing users to compare their behavior in real-time on various datasets. It is based on the research paper:

> G. Dudek, *"A constructive approach to data-driven randomized learning for feedforward neural networks"*, Applied Soft Computing, vol. 112, 2021.

## Methods

| Method | Description |
|--------|-------------|
| **RVFL** | Random Vector Functional Link — random weights from [-1,1], with direct input-output links |
| **ELM** | Extreme Learning Machine — random weights, no direct links or output bias |
| **D-DM** | Data-Driven Method — places sigmoids in randomly selected input regions, adjusts slopes to local target function complexity |
| **CD-DM** | Constructive D-DM — iteratively builds the network, accepting nodes only when error reduction exceeds an adaptive threshold &theta; |

### Key Insight: CD-DM vs D-DM

While D-DM generates all nodes at once (many of which are flat/redundant), **CD-DM selectively constructs the network** by:
- Accepting only nodes that significantly reduce the error
- Starting with a strict threshold (modeling rough shape)
- Gradually relaxing the threshold (capturing finer details)

This results in **2-5x fewer nodes** for the same accuracy level.

## Datasets

### Classification (2D)
- **Circle** — points inside vs outside a radius
- **XOR** — classic nonlinear separation problem
- **Spiral** — two interleaved spirals
- **Clusters** — two Gaussian blobs

### Regression (1D)
- **Function (6)** from the paper: `g(x) = 0.2·exp(-(10x-4)²) + 0.5·exp(-(80x-40)²) + 0.3·exp(-(80x-20)²)`

### Regression (2D)
- **Function (7)** from the paper: `g(x) = sin(20·exp(x₁))·x₁² + sin(20·exp(x₂))·x₂²`

## Features

- **Step-by-step animation** of the network construction process
- **Real-time visualizations**: network architecture, decision boundary / fitted curve, sigmoid distributions, RMSE convergence
- **CD-DM process view**: accepted (green) vs rejected (red) candidate nodes
- **Adjustable parameters**: number of nodes (m), neighborhood size (k'), threshold (θ), patience (Q), and more
- **Interactive controls**: play/pause, step, speed slider, dataset noise and size
- **Dark theme UI** inspired by TensorFlow Playground

## Usage

Simply open `index.html` in any modern browser. No dependencies, no build tools, no server required.

1. Select a **method** (RVFL, ELM, D-DM, or CD-DM)
2. Choose a **dataset** (classification or regression)
3. Adjust **parameters** (nodes, neighborhood size, noise)
4. Click **Play** ▶ and watch the network learn

## Technical Details

- Pure **HTML/CSS/JavaScript** — single file, zero dependencies
- **Canvas-based** rendering for smooth visualizations
- Linear algebra implemented from scratch (Cholesky decomposition, pseudoinverse via regularized normal equations)
- Algorithms faithfully implement the methods described in the paper, including the full CD-DM construction process with adaptive threshold

## References

- Dudek, G. (2021). *A constructive approach to data-driven randomized learning for feedforward neural networks*. Applied Soft Computing, 112, 107797. [DOI](https://doi.org/10.1016/j.asoc.2021.107797)
- Dudek, G. (2020). *Data-driven randomized learning of feedforward neural networks*. IJCNN 2020.
- Dudek, G. (2019). *Generating random weights and biases in feedforward neural networks with random hidden nodes*. Information Sciences, 481, 33-56.

## License

MIT License
