# Im3D - Single View Image to 3D Point Cloud Reconstruction 

## Introduction
This project focuses on reconstructing 3D point clouds from single-view RGB images, specifically within the chair class of the ShapeNet rendered dataset. The objective was to generate accurate 3D point clouds from 2D images using two different architectures, each with its own strengths in terms of latent space manipulation and control over the output. 
1. PCA + AutoEncoder: Used to manipulate the parameters of learned latent vector towards generating 3D point clouds, but did not allow conditoned generation.
2. Conditional Variational Auto Encoder : Used to obtain conditoned 3D point clouds by conditoning one hot encoded vector in the latent space.

## System Architecture 
In this section we will discuss about two architectures implemented for the point cloud generation.
### 1. Principal Component Analysis (PCA) + Auto-Encoder
![PCA + Auto Encoder](https://github.com/Jatinkalal/IM3D/blob/main/Images/architecture_pca.png)
This approach begins with feature extraction of 2D input image using pre-trained resnet-18 architecture, the vector obtained undergoes PCA tp reduce its dimensionality to 1x4 (as we assume there are 4 important parts in a chair), by manipualting parameters of this vector we generate the 3D point cloud, but since the vector is learned and we need to estimate parameters mapping to each part of the chair, it restricts user-controlled single attribute manipulation.

### 2. Conditional Variational Auto Encoder (C-VAE)
![C-VAE](https://github.com/Jatinkalal/IM3D/blob/main/Images/Archiecture.png)
From the previous architecture, the need for user-controlled generation led to the development of this new model. In this approach, a one-hot encoded vector is incorporated into the latent space, allowing the generation of 3D point clouds conditioned on the specific input vector. During inference, a random latent vector is sampled, and the desired output is generated by providing a user-defined condition through the conditional vector. This enables more control and flexibility in producing the desired 3D point cloud reconstructions based on user preferences.
(The one hot encoding vector is 17 dimensional vector each parameter corresponds to a specifc semantic of the chair.)

## Results from PCA + Auto Encoder (Architecture 1)
![PCA + Auto Encoder](https://github.com/Jatinkalal/IM3D/blob/main/Images/last_moment.003.png)
Results from PCA Varied, first row represents chair type1 and second row of type2, with each of 4 components individually varied.

## Results from C-VAE (Architecture 2)

| ![Swivel legs]([https://github.com/Jatinkalal/IM3D/blob/main/Images/Cantilever.gif](https://github.com/Jatinkalal/IM3D/blob/main/Images/Swivel.gif)) | ![Cantilever legs](https://github.com/Jatinkalal/IM3D/blob/main/Images/Cantilever.gif) | 
|:--------------------------:|:--------------------------:|
| Here the conditonal vector was to generate ***"Swivel legs"*** during the inference from a random noise vector          | Here the conditon was to generate ***"Cantilever legs"*** during the inference from a random noise vector.          














