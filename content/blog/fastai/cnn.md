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

A neural network is nothing more than a combination of weights (sometimes called parameters) and activations.

### Parameters

These are the weights associated with each layer. They are also the ones that get updated.

### Activations

These are the non-linearity that is present within the neural network. Non-linearity is important because it allows us to approximate infinitely complex functions by layering these non-linearity.

There are many types of activation. Here are some common ones:

- Sigmoid
  - Squishes an input between the range of $]0, 1[$
  - Also known as the logistic function, $f(x) = \frac{1}{1 + e^{-x}}$
  - Often applied in the last layer of a binary classification network.
  - Experience a vanishing gradient as score is very positive or negative.
- Softmax
  - Applies to a layer of outputs and squishes such that the $\sum_{output} = 1$
  - $f(x) = \frac{e^{x}}{\sum_{i = 1}^{C}e^{x_i}}$
  - Often applied in the last layer of the a multi-class classification neural network.
- ReLu (Rectified Linear Unit)
  - Is often used in place of the sigmoid these days to fix vanishing gradient problem
  - $ReLu(x) = \max(x, 0)$
  - Has other variants where the gradient for $x \lt 0$ is non zero. Otherwise known as *Leaky ReLu*

## Convolution Neural networks

A Convolution refers to the processing of an input with a kernel.

The kernel acts as a sliding window, performing element wise multiplication with each element before summing everything up to obtain a single value in our output.

![Image of kernel multiplication with input image](/images/fastai/cnn.png "Image of kernel multiplication with input image")

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

### Classification - Cross Entropy Loss

Before we dive into the loss function for evaluating image classification problem, we need to evaluate the type of image classification.

In particular, we have:

- Multi-class classification
  - Each image belong to 1 of $C$ classes.
  - Number of output correspond to $C$ and the max score of the outputs is taken as the class for that image.
- Multi-label classification
  - Each image belong to some number of $C$ classes.
  - Number of output correspond to $C$.
  - Each output attempts a binary task of deciding if that image belongs to that label or not. An image is said to be in that class if it passes some threshold for that class.

Cross Entropy is then defined as:

$$Loss(x) = - \sum_{i = 0}^{n}t_i\log(s_i) \text{ , where }\\
n\text{ is the number of classes, }\\
t\text{ is the ground truth}\\
s \text{ is the score for that class, derived from }x$$

Variants of cross entropy loss are then used for the two different kind of classification problem.

#### Categorical Cross Entropy Loss

This variant of Cross Entropy Loss is often used for Multi-class classification. It is also sometimes called the softmax loss.

$s$ is a $Softmax(x)$ activation function.

$t_i$ is the One-hot encoded matrix for ground truth of the image class.

Resulting equation is:

$$Loss(x) = - \log(\frac{e^{s_{pred}}}{\sum_{i = 0}^{n} e^{s_I}}), s = neuralNetwork(x)$$

$$\nabla_{s_{pred}}Loss(x) = \underbrace{\frac{e^{s_{pred}}}{\sum_{i = 0}^{n} e^{s_i}}}_{softmax} - 1$$

$$\nabla_{s_{other}} Loss(x) = \frac{e^{s_{other}}}{\sum_{i = 0}^{n}e^{s_i}}$$

Cross Entropy can also be extended to multi-label classification.

Although not originally intended for it, it has been shown by [this paper](https://research.fb.com/publications/exploring-the-limits-of-weakly-supervised-pretraining/) that it works better than the normally used binary cross entropy loss.

The modified categorical cross entropy loss is simply the log sum of the predicted class divided by the number of classes $M$ predicted.

$$ Loss(x) = \frac{1}{M}\sum_{p}^{M}-\log{\frac{e^{s_p}}{\sum_{i = 0}^{n}e^{s_i}}}$$
$$\nabla_{s_{other}} Loss(x) = \frac{e^{s_{other}}}{\sum_{i = 0}^{n}e^{s_i}}$$
$$\nabla_{s_{p^i}} Loss(x) = \frac{1}{M}\left(\frac{e^{s_{p^i}}}{\sum_{i = 0}^{n}e^{s_i}} - 1 + (M - 1)\frac{e^{s_{p^i}}}{\sum_{i = 0}^{n}e^{s_i}}\right)$$

Where $s_{p^i}$ is the score of any positive class.

#### Binary Cross Entropy Loss

Binary Cross Entropy loss is also sometimes called the sigmoid cross entropy loss.

Due to the use of sigmoid as an activation function instead of softmax, it is often used for multi-label classification.

Why?

Because the insight of an input belonging to a certain class does not affect the chance of the input belonging to another class.

The way this is done is by having binary Cross entropy loss set-up a $C = 2$ classification problem for each class, $c$, in $C$.

$$\begin{aligned}Loss(x) &= - \sum_{i = 0}^{1} t_i\log{\sigma(s_i)} \\ &= - [t_0\log{\sigma(s_0)} + (1 - t_0)\log{\sigma(1 - s_0)}\end{aligned}$$

where $\sigma$ is the sigmoid function.

$$\nabla_{s_i} Loss(x) = t_0(\sigma(s_i) + 1) + (1 - t_0)(\sigma(s_i)$$

#### Focal Loss

Focal Loss uses sigmoid activation and is a variant of Binary Cross Entropy Loss.

Focal Loss supposedly reduces the problem of class imbalance by making the loss implicitly focus in those problematic classes.

$$\begin{aligned}Loss(x) &= -\sum_{i = 0}^{1}(1 - \sigma(s_i))^{\gamma} t_i\log{\sigma(s_i)} \\ &= -[t_0(1 - \sigma(s_i))^{\gamma}\log{\sigma(s_i)} + (1 - t_0)(1 - \sigma(1 - s_0))^{\gamma}\log{\sigma(1 - s_0)}\end{aligned}$$

The equation above reduces to Binary Cross Entropy when $\gamma = 0$.

$$\nabla_{s_0} Loss(x) = (1 - \sigma(s_i))^{\gamma}(-\gamma \sigma(s_i) \log{\sigma(s_i)} + \sigma(x) - 1)$$

To get the differential with respect to $s_1$, simply replace $s_0$ with $1-s_0$
