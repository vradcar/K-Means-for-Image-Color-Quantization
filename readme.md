### **1. K-Means Algorithm (`kmeans(image, k, max_iters=100)`)**

This function implements the K-Means clustering algorithm manually. It’s designed to find `k` representative colors (centroids) for the image.

- **Step 1: Initialize Centroids**
  - At the start, `k` random pixels from the image are selected as initial centroids. These represent the first guesses for the cluster centers (colors).
  
- **Step 2: Assign Pixels to the Nearest Centroid**
  - For each pixel in the image, calculate its distance from all the centroids using the Euclidean distance formula.
  - Assign each pixel to the nearest centroid based on its RGB value.
  
- **Step 3: Update Centroids**
  - Once every pixel is assigned to a cluster (centroid), recompute the centroids as the average color of all pixels assigned to them.
  
- **Step 4: Repeat Until Convergence**
  - Repeat Steps 2 and 3 until the centroids no longer change (or change very little), or the number of iterations exceeds `max_iters`.

- **Handle Empty Clusters:**
  - If a centroid ends up with no pixels assigned to it (an empty cluster), reinitialize that centroid randomly from the dataset.

---

### **2. Quantizing the Image (`quantize_image(image, centroids, labels)`)**

This function takes the centroids calculated by the K-Means algorithm and uses them to reduce the number of colors in the image.

- **Input:**
  - `image`: The original image matrix (RGB values).
  - `centroids`: The colors (centroids) calculated by K-Means.
  - `labels`: The cluster assignments for each pixel (which centroid each pixel belongs to).

- **Process:**
  - For each pixel, find its corresponding cluster assignment in `labels` and replace its color with the centroid (the representative color for that cluster).
  - The result is an image where each pixel’s RGB value is one of the `k` centroid values, reducing the color complexity.

---

### **3. Applying K-Means to an Image (`apply_kmeans(image_path, k_values)`)**

This function applies the K-Means algorithm to an image for different values of `k` (the number of clusters).

- **Steps:**
  1. Load the image using `plt.imread()`.
  2. For each `k` in `k_values` (e.g., `k = 2, 8, 16, 32`):
     - Run the K-Means algorithm to compute `k` centroids.
     - Use the `quantize_image` function to apply the centroids and labels to the image.
     - Display the quantized image using `plt.imshow()`.

---

### **4. Random Centroids Quantization (`random_centroids_quantization(image_path, k_values)`)**

This function does color quantization using randomly selected pixel values as centroids, instead of running K-Means.

- **Process:**
  - Load the image as before.
  - For each `k` in `k_values`:
    - Randomly select `k` pixels from the image to use as centroids.
    - Assign each pixel to the nearest centroid (randomly selected).
    - Apply the `quantize_image` function to generate the quantized image.
    - Display the quantized image.

This is used for comparison with the result of using K-Means.

---

### **5. Apply to a Custom Image (`quantize_custom_image(image_path, k)`)**

This function applies the K-Means color quantization on a custom image you select, using any value of `k`.

- **Process:**
  - Load the custom image.
  - Apply the K-Means algorithm with a chosen `k`.
  - Quantize the image and display it.

This part of the assignment allows you to experiment with your chosen image and see the effects of K-Means quantization with different numbers of clusters.

---

### **Additional Concepts:**

- **`max_iters`**: Limits the number of iterations the K-Means algorithm runs. It prevents the algorithm from running indefinitely if it doesn’t converge quickly.
  
- **`plt.imshow()`**: Part of the `matplotlib` library, used for displaying images.
  
- **Centroids**: These are the representative colors in the final image. After K-Means converges, the centroids represent the average colors of the clusters in the image.

---

### **Key Takeaways:**
- **Manual K-Means Implementation**: You will manually implement K-Means without relying on machine learning libraries like `scikit-learn`. You’re allowed to use `numpy` for matrix operations.
  
- **Color Quantization**: K-Means is applied to reduce the number of colors in an image, making it suitable for display devices with limited color capabilities.
  
- **Random Centroid Initialization**: Comparing results using calculated centroids versus randomly chosen centroids helps you understand how well K-Means clusters data in terms of color representation.
