# Graph-Based Image Segmentation via Spectral Clustering

# 1. Introduction

Traditional clustering algorithms such as K-means fail to separate non-convex cluster structures.  
Spectral clustering leverages the eigenstructure of the graph Laplacian to embed data into a space where clusters become linearly separable.

This project explores graph-based image segmentation using:

- Pixel intensity
- Spatial coordinates
- k-nearest neighbour graph construction
- Random-walk normalized Laplacian

---

# 2. Methodology

## 2.1 Feature Representation

Each pixel is represented as:

$$
x_i = [I_i, x_i, y_i]
$$

where:

- $I_i$ is pixel intensity
- $(x_i, y_i)$ are spatial coordinates

---

## 2.2 Similarity Graph Construction

A Gaussian similarity function is used:

$$
w_{ij} =
\exp\left(
-\frac{(I_i - I_j)^2}{2\sigma_{pixel}^2}
-\frac{\|p_i - p_j\|^2}{2\sigma_{geom}^2}
\right)
$$

The similarity graph is constructed using k-nearest neighbours.

---

## 2.3 Random Walk Laplacian

The random-walk normalized Laplacian is defined as:

$$
L_{rw} = I - D^{-1}W
$$

Eigenvectors corresponding to the smallest eigenvalues are used as spectral embeddings.  
Clustering is then performed using K-means in the embedded space.

---

# 3. Experimental Results

## 3.1 Parameter Sensitivity

### Case 1: σ_pixel = 10, σ_geom = 10
