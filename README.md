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
### Original Image
<img width="1000" height="1000" alt="300091" src="https://github.com/user-attachments/assets/57dcf180-9151-44c7-81ec-82af1729041e" />
### Case 1: σ_pixel = 10, σ_geom = 10
<img width="1000" height="1000" alt="300091-10-10" src="https://github.com/user-attachments/assets/7cc599a0-f7bf-463b-ad7b-ad7570ffb4b1" />
### Case 2: σ_pixel = 8, σ_geom = 10
<img width="1000" height="1000" alt="300091-8-10" src="https://github.com/user-attachments/assets/4fe430ff-68eb-4ad8-a963-dc2606c779b3" />

Observations

Lower $\sigma_{pixel}$ increases sensitivity to intensity differences
Boundary sharpness improves
Noise level increases in homogeneous regions

## 3.2 Comparison with K-means
<img width="1200" height="500" alt="moonexample1" src="https://github.com/user-attachments/assets/6bd2bf63-04c6-443a-ba73-c9f9a8168983" />
K-means fails to separate non-convex clusters.
Spectral clustering successfully identifies manifold structures via graph embedding.

# 4. Computational Considerations

- Eigen decomposition is computationally expensive ($O(n^3)$)
- Memory cost increases with graph size
- Sensitive to $\sigma$ selection
- Requires predefined cluster number

# 5. Future Work

- Nyström approximation for large-scale images
- Adaptive sigma estimation
- Integration with CNN feature extraction
- Application to medical image segmentation

# 6. Conclusion

Spectral clustering provides a powerful graph-based approach for image segmentation, particularly in scenarios where cluster structures are non-convex.
However, scalability and parameter sensitivity remain practical challenges.
