# Space_To_Summer_Sea

**## Automated Destriping Pipeline

This project develops an automated image-processing pipeline for reducing striping artifacts and generating high-quality visualizations from raw imagery. The goal is to replace time-intensive manual post-processing with a reproducible, scalable workflow.

### Methodology

The pipeline combines a **hybrid Wavelet–FFT destriping method with a Residual U-Net convolutional neural network**. The Wavelet–FFT stage decomposes each image by scale and direction, identifies vertical-detail components associated with striping, and suppresses stripe-related frequencies before reconstruction.

The resulting images are then refined using a **Residual U-Net CNN**, which learns to distinguish remaining stripe artifacts from meaningful ocean and land features. The residual architecture allows the network to focus on correcting image artifacts while preserving the underlying structure of the original image.

### Key Improvements

* **Wavelet–FFT decomposition:** Separates image features by scale and direction to isolate stripe-related frequencies.
* **Residual U-Net refinement:** Uses a CNN-based residual learning approach to remove remaining artifacts while preserving important image features.
* **Rotation handling:** Improved processing of images with varying orientations.
* **Boundary handling:** Reduced reconstruction artifacts near image boundaries.
* **Missing-data handling:** Improved robustness to incomplete or masked regions.
* **Parameter optimization:** Implemented randomized parameter sampling across different wavelet types, decomposition levels, and Gaussian damping values.
* **Automated reconstruction:** Combines frequency-domain filtering and learned image refinement into a streamlined processing pipeline.

### Performance

The current pipeline achieves approximately **90% performance on our evaluation metric**, demonstrating substantial improvement in automated stripe removal while maintaining important ocean and land features.

### Current Progress

These improvements bring the project closer to a **fully automated destriping and visualization pipeline**, significantly reducing the hours of manual post-processing previously required. The combination of frequency-domain processing and deep-learning-based refinement provides a flexible framework for producing consistent and high-quality imagery at scale.

Future work will focus on further optimizing the CNN architecture, improving training data and parameter selection, and evaluating performance across a wider range of imagery and stripe patterns.



