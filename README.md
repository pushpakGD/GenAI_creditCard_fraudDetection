# Data Balancing with GenAI - Credit Card Fraud Detection

## Summary: 
- This project focuses on addressing data imbalance in the context of credit card fraud detection using Generative Adversarial Networks (GANs). Imbalanced datasets, such as those encountered in fraud detection, often lead to biased model performance.
- To overcome this challenge, this project uses GAN to generate synthetic data, thereby balancing the dataset. GANs create artificial samples that resemble the minority class, improving the model's ability to recognize and classify fraud instances accurately.

## Background:
This dataset is provided by Secure Trust Financial Services. And the model is a binary classifier but it is not working well because the data is imbalanced. To solve this problem, General Adversial Networks (GANs), a type of generative AI is used, to generate synthetic fraudulent transactions that are indistinguishable from real transactions. This method will help to improve the accuracy of the fraud detection model.

## Process:

To see the running GAN model, please refer the notebook file included in this repository.

### 1. EDA

This step included data exploration and dimensionality reduction.
- PCA to reduce dimensionality of features X into two dimensions
- Scatter plot to visualize data

A block diagram for undesrtanding the process

A Generator-Discriminator model, commonly referred to as a GAN (Generative Adversarial Network), is a framework in machine learning where two neural networks, the generator and the discriminator, are trained simultaneously through adversarial training. The basic idea is to have the generator create data instances, and the discriminator evaluate them. This process continues iteratively, with both networks improving over time (based on number of epochs and batch_size you describe).

![GANss1](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss1.png)

- 1. Generator:
The generator takes random noise as input and produces synthetic data.
The objective of the generator is to create data that is indistinguishable from real data.
Initially, the generator produces data that may not resemble the real data.

- 2. Discriminator:
The discriminator takes both real and synthetic data as input and classifies them as either real or fake.
The discriminator is trained to correctly classify real data as real and synthetic data as fake.
Initially, the discriminator's performance might be random.

- 3. Training Process:
During training, the generator and discriminator are combined and are always in a constant feedback loop.
The generator tries to improve its ability to generate realistic data by fooling the discriminator.
The discriminator aims to become better at distinguishing real from synthetic data.

- 4. Adversarial Nature:
The generator and discriminator are adversaries in the sense that one is trying to outperform the other.
The competition between them results in the generator producing increasingly realistic data, and the discriminator becoming more skilled at telling real from fake.

total 29 features and one class column

![GANss2](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss2.png)

![GANss3](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss3.png)

### 2. Building generator and discriminator models

###### Generator: 
- generating more fradulent data to balance the dataset
- defined a function to create a generator model.

This function, build_generator(), constructs a generator model for a Generative Adversarial Network (GAN). The generator is designed using a sequential architecture in Keras. It comprises several fully connected layers with rectified linear unit (ReLU) activations and batch normalization to enhance training stability. The generator takes an input of dimension 29 and produces an output of the same dimension with a linear activation function. This function is a key component in GANs, responsible for generating synthetic data.

###### Discriminator:
- function to build a discriminator model

The discriminator is designed as a sequential neural network using Keras. It consists of several fully connected layers with rectified linear unit (ReLU) activations. The input dimension is set to 29, matching the expected input dimension of the data. The output layer uses a sigmoid activation function to produce binary classification results (real or fake). The model is compiled using the Adam optimizer and binary crossentropy loss. This discriminator is a crucial part of the GAN, as it aims to distinguish between genuine and generated data.

### 3. Combining generator and discriminator

This task includes
- combining both generator and discriminator models to create GAN
- a function to generate synthetic data

This GAN model, when trained, allows the generator to learn to produce data that is indistinguishable from real data by fooling the discriminator. The overall goal is to achieve a generator that generates realistic data.

In the scatter plots below, it can be seen how the combined generator and discriminator model generates synthetic data points to resemble the real data points.

![GANss4](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss4.png)

![GANss5](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss5.png)

![GANss6](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss6.png)

![GANss7](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss7.png)

### 4. Model evaluation

This task includes training and evaluating GAN by creating a function to monitor generator for defined number of epochs and batch size.
Finally generating synthetic data using trained generator.

Input Parameter: generator, The generator model.
###### Functionality:
The function uses Principal Component Analysis (PCA) to reduce the dimensionality of the real fraud data (excluding the 'Class' column).
The real fraud data is transformed using PCA, and a DataFrame (df_real) is created with the transformed data and an additional 'label' column set to 'real'.
Synthetic fraud data is generated using the provided generator, and PCA is applied to transform it.
Another DataFrame (df_fake) is created for the transformed synthetic data with an additional 'label' column set to 'fake'.
The real and fake data DataFrames (df_real and df_fake) are concatenated into a single DataFrame (df_combined).
A scatter plot is created using Seaborn (sns.scatterplot), where the first and second PCA components are used as the x and y axes, respectively. Points are colored based on the 'label' column, with a size of 10.

- histograms to check the individual distribution of syntehtic and real fraud data.

Histograms to visualize the distribution of each feature while differentiating between real and fake data points.
- for all 29 features

![GANss8](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss8.png)

![GANss9](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss9.png)

![GANss10](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss10.png)

![GANss11](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss11.png)

![GANss12](https://github.com/pushpakGD/GenAI_creditCard_fraudDetection/blob/main/images/GANss12.png)
