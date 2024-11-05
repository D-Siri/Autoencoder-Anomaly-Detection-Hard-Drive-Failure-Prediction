# Autoencoder-based Anomaly Detection for Hard Drive Failure Prediction

This repository implements and evaluates autoencoder models for anomaly detection aimed at predicting hard drive failures using S.M.A.R.T. (Self-Monitoring, Analysis and Reporting Technology) data.

## Dataset Overview

The dataset consists of daily snapshots of operational hard drives, capturing:

- **Basic Hard Drive Information**: Date, serial number, model, and capacity.
- **S.M.A.R.T. Statistics**: 90 variables that include raw and normalized values for various S.M.A.R.T. attributes.
- **Failure Status**: A binary variable indicating whether the drive has failed (0 for OK, 1 for failure).

### Dataset Characteristics

- **Nature**: Structured data with entries representing daily snapshots.
- **Total Entries**: Each entry corresponds to one hard drive's daily data.
- **Variables Include**:
  - `date`: Date in yyyy-mm-dd format
  - `serial_number`: Manufacturer-assigned serial number
  - `model`: Manufacturer-assigned model number
  - `capacity_bytes`: Drive capacity in bytes
  - `failure`: Binary variable indicating drive failure
  - `smart_1` to `smart_90`: Various S.M.A.R.T. statistics

## Autoencoder Models

### Autoencoder 1

- **Encoder**:
  - Input Layer: Shape = input_dim
  - Dense Layers: 128 units → 64 units → 32 units (ReLU activation)
  
- **Decoder**:
  - Dense Layers: 64 units → 128 units → input_dim (ReLU activation)
  
- **Compilation**: Compiled with Adam optimizer and Mean Squared Error (MSE) loss function.

### Autoencoder 2

- **Encoder**:
  - Input Layer: Shape = input_dim
  - Dense Layers: 256 units → 128 units → 64 units (LeakyReLU with alpha=0.2)
  
- **Decoder**:
  - Dense Layers: 128 units → 256 units → input_dim (LeakyReLU with alpha=0.2)
  
- **Compilation**: Compiled with Adam optimizer and MSE loss function.

### Autoencoder 3

- **Encoder**:
  - Input Layer: Shape = input_dim
  - Dense Layers: 32 units → 16 units (ReLU activation)
  
- **Decoder**:
  - Dense Layer: input_dim (linear activation)
  
- **Compilation**: Compiled with Adam optimizer and MSE loss function.

## Results Summary

| Model          | Test Accuracy | Reconstruction Accuracy | Precision | Recall | F1 Score |
|----------------|---------------|-------------------------|-----------|--------|----------|
| Autoencoder 1 | 0.9498        | 0.999998                | 0.0010    | 0.1469 | 0.0019   |
| Autoencoder 2 | 0.9497        | 0.999999                | 0.0006    | 0.0948 | 0.0013   |
| Autoencoder 3 | 0.9498        | 0.999998                | 0.0010    | 0.1517 | 0.0020   |

## Strengths and Limitations

### Strengths
- **Unsupervised Learning**: Autoencoders can learn from unlabeled data, making them suitable for anomaly detection when labeled anomaly data is scarce.
- **Non-linearity**: They can capture complex patterns and relationships in the data.
- **Dimensionality Reduction**: Inherently reduces the dimensionality of the data.
- **Robustness to Noise**: Filters out noise during reconstruction.

### Limitations
- **Limited Interpretability**: The learned latent space may lack interpretability.
- **Threshold Setting Challenges**: Determining an appropriate threshold can be difficult.
- **Sensitivity to Normal Variability**: May struggle to differentiate anomalies from normal variations.
- **Computationally Intensive Training**: Training deep architectures can be resource-intensive.

## Usage Instructions

1. Open the Jupyter notebook.
2. Follow the instructions within the notebook to execute the code and evaluate the models.

## Requirements

Ensure you have the following libraries installed:

- Python >=3.x
- TensorFlow
- Keras
- NumPy
- Pandas
- Matplotlib
- Scikit-learn


## License
MIT License

Copyright (c) [2024] [Siri Duggineni]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
