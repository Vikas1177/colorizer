# IMAGE COLORIZER
## Overview
The goal is to generate color images from black and white images, leveraging the power of GANs. The model is trained on the Image Colorization dataset from Kaggle.

## Background
Generative Adversarial Network (GAN)
- A GAN consists of two networks: Generator and Discriminator.
- The Generator creates images trying to fool the Discriminator.
- The Discriminator learns to distinguish between real and generated images.
- DCGAN uses convolutional layers to enhance the image generation quality.

## Color Space
We use LAB color space where:
- L channel represents luminance (grayscale image input).
- A and B channels represent color.
The generator takes the L channel as input and generates the A and B channels.
Includes sample results showcasing the model's performance

## Model Architecture
- Based on U-Net architecture with skip connections between downsampling and upsampling layers.
- Generator uses Conv2d, BatchNorm2d, LeakyReLU for downsampling, and ConvTranspose2d, BatchNorm2d, LeakyReLU for upsampling.
- Final activation is a Tanh function to output color values normalized in [-1, 1].
- Discriminator uses downsampling layers with MaxPool2D, Flatten, Linear layers, and Sigmoid activation for binary classification (real or fake).

## Loss Functions
- Discriminator maximizes the probability of correctly identifying real vs generated images, with label smoothing (0.1) to prevent overconfidence.
- Generator tries to fool the discriminator and minimize L1 loss between generated and real images weighted by λ=100 for color similarity.

## Training Challenges and Solutions
- Learning rate tuning with ReduceLROnPlateau scheduler to avoid divergence.
- Managing discriminator dominance by adjusting learning rates and training frequency.
- Overfitting handled via batch normalization and regularization.
- Large dataset (25,000 images) split into smaller parts due to GPU constraints.
- Persistent noise in generated images attributed to local minima in generator training.

## Results
- Good colorization on some images like sky and simple backgrounds.
- Challenges remain in colorizing complex objects and avoiding noise.
- Further improvements may be possible with architectural tweaks like InstanceNorm2d and dropout.

## To know more read this
[ppt](ppt.pptx)
## Results from my colorizer
![result-1](results/Screenshot_2024-09-30_204922.png)
![result-2](results/Screenshot_2024-09-30_160857.png)
![result-3](results/Screenshot_2024-09-30_162158.png)
![result-4](results/Screenshot_2024-09-30_205919.png)
