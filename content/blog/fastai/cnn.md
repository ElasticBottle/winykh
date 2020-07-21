---
title: "Understanding Convolution Neural networks"
date: 2020-07-10T11:22:39+08:00
slug: "understanding-cnn"
description: "Everything about convolution neural networks"
keywords: ["Convolution neural network", "cnn", "deep learning", "ML", "ai"]
draft: true
tags: ["FastAI", "AI"]
math: false
toc: false
---

## Neural Networks

## Convolution Neural networks

A Convolution refers to the processing of an input with a kernel.

The kernel acts as a sliding window, performing element wise multiplication with each element before summing everything up to obtain a single value in our output.

![Image of kernel multiplication with input image](/static/images/fastai/cnn.png "Image of kernel multiplication with input image")

Instead of sliding window, convolution can also be done by expanding the kernel as a circulant matrix and performing matrix multiplication with the input.

### Kernels

Kernels comes in all shape and sizes, The most common size is a $3 \times 3 \times \text{number of image channel.}$

The resulting output then would be a single channel image, with a one pixel border.

To fix that, padding is often added following the formula:

$$\text{padding } = \lfloor\frac{\text{kernel size}}{2}\rfloor$$

The first input to the convolution neural net is often the number of channels in the image.

The number of output following the input can often be thought of as maximally being as large as the total elements in the kernel.

Why?

The intuition is that each output represents a feature and if each value in the kernel represented a feature, you would be able to extract at most $\text{kernel size}$ number of features.

#### Types of Kernels

- Identity
- blur
  - Mean
  - Gaussian
- Sobel top/bottom/left/right
- Emboss

##### Identity Kernel

Everything is 0 except for a single 1 in the matrix.

The result is the exact same image copied over with a one pixel border all around. (solved by adding padding)

$$\begin{bmatrix}
    0 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 0 \\
\end{bmatrix}$$

##### Blur Kernels

Both mean and gaussian matrices results in a blurred image.

The mean matrix involving having a 1 by matrix divided by the number of elements in the kernel:

$$
\frac{1}{9}
\begin{bmatrix}
    1 & 1 & 1 \\
    1 & 1 & 1 \\
    1 & 1 & 1 \\
\end{bmatrix}
$$

The gaussian matrix involves having the values spread out like in a 2d gaussian curve (for a 2d kernel):

$$
\frac{1}{16}
\begin{bmatrix}
    1 & 2 & 1 \\
    2 & 4 & 2 \\
    1 & 2 & 1 \\
\end{bmatrix}
$$

##### Sobel kernel

The Sobel kernel is useful in detecting edges in an image:

$$\begin{bmatrix}
    1 & 0 & -1 \\
    2 & 0 & -2 \\
    1 & 0 & -1 \\
\end{bmatrix}$$

Above is a left Sobel kernel.

##### Emboss Kernel

The emboss kernel is similar to the sobel kernel in that it helps detect edges. This time, in the diagonal directions.

$$\begin{bmatrix}
    -2 & -1 & 0 \\
    -1 & 1 & 1 \\
    0 & 1 & 2 \\
\end{bmatrix}$$

The above is an emboss kernel detecting changes from the top left to bottom right.

## Regularization

Regularization is a means of allowing our model to have the required expressivity while preventing it from over-fitting our model.

It works by preventing the coefficients from getting too large since a model left unchecked will result in the weights growing larger overtime (really?)

### Drop Out

For dropout, we throw away at random, some percentage $p$ of the activations. A common value for $p$ is 0.5.

The activation that is being thrown away varies from batch to batch.

This prevents any one activation from remembering part of the input, thereby preventing over-fitting.

During actual evaluation, the activations are multiplied by $p$. This is to compensate the activations being louder since there were less of it during training time.

```python
noise.bernoulli_(1 - p)
noise.div_(1-p)
return multiply<inplace>(input, noise)
```

The above is a rough implementation of drop out.

- `noise` is the drop out mask and basically represents whether or not to keep the `input` (activation) or not.
- We use `1 -p` because that's the probability we keep the inputs
- we divide `noise` by `1-p` so as to amplify the activation to compensate for the loss of activations.

### Weight Decay

Add a penalty for having the magnitude of the weights become too large.

## Normalization

Normalization is the process of standardizing the values that flows through the neural network.

Often, we standardized during input to make sure that incoming values have a mean of 0 and variance of 1.

The reason?

So that larger value inputs does not unfairly influence activations.

### Input Normalization

Input Normalization refers to normalizing our data before training begins.

This can be done in one of two main ways:

- Subtracting the mean value from each individual value and dividing it by the difference between min and max values
- Subtracting the value of the mean and dividing by the standard deviation of the batch (this is more accurately known as standardizing)

### Batch Normalization

Refers to re-normalizing outputs of the activations a layer in the neural network.

$$
var(batch) \\

\bar{batch} = \\

normalized = \frac{input - \bar{batch}}{var(batch)} \\
output = \gamma normalized + \beta
$$

Does not work with small batch sizes due to high variance and fluctuation in batch mean and variance.

It negates the effect of weight decay(?)

## Training Optimization

### Momentum

Have the update be based on current gradient and previous gradient.

### RMS Prop

### Adam

## Evaluating performance - Loss functions
