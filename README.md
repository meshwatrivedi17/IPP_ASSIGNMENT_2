[README_Practical-2.md](https://github.com/user-attachments/files/34223555/README_Practical-2.md)
# Image Processing & Pattern Recognition – Practical 2

**Topic:** Edge detection, noise analysis, compression and segmentation
**Notebook:** `IPP_Practical-2.ipynb`
**Course:** PGDM in Big Data Analytics , AIDTM (Batch 2025–27)

---

## Overview

This practical works through six problems that go beyond the basics: comparing edge detectors, testing noise sensitivity, comparing lossless compression methods, analysing JPEG-style compression, and segmenting images using texture and multi-feature clustering.

---

##  Tech Stack

| Library | Purpose |
|---|---|
| OpenCV (`cv2`) | Edge detection, filtering, DCT / inverse DCT |
| NumPy | Pixel and matrix operations |
| Matplotlib | Visualisation |
| scikit-image | GLCM texture features, SSIM |
| scikit-learn | K-Means clustering |
| heapq, collections | Huffman coding and frequency counting |

---

##  Problems

### Problem 1 – Comparative Edge Detection on Natural Images
Applied **Sobel**, **Laplacian** and **Canny** to an outdoor image.

**Finding:** Canny captured the most meaningful edges, with thin and well-defined boundaries. Sobel highlights gradient direction, while Laplacian picks up fine detail but is noisier.

---

### Problem 2 – Noise Sensitivity Experiment
Added **Gaussian noise** and **salt-and-pepper noise** to a grayscale image, then applied Sobel and Laplacian.

**Findings:**
- Laplacian is more affected by noise because it uses second-order derivatives.
- Noise creates false edges and reduces edge clarity.
- **Gaussian blur** before edge detection improves the results.

---

### Problem 3 – Compression Ratio Comparison (RLE vs Huffman)
Compressed a grayscale image with **Run-Length Encoding** and **Huffman Coding**.

| Method | Size (bits) | Reduction |
|---|---|---|
| Original | 13,107,200 | – |
| RLE (estimated) | 51,464,800 | −292.65% (size increased) |
| Huffman | 12,235,786 | 6.65% |

**Finding:** RLE only helps when there are long runs of identical pixels. This image had too few, so the output grew. Huffman gave a modest gain by exploiting uneven pixel frequencies.

---

### Problem 4 – JPEG Block Artifact Analysis
Implemented 8×8 block **DCT + quantisation** on the luminance channel at three quantisation levels.

| Level | MSE | PSNR (dB) | SSIM |
|---|---|---|---|
| Low | 25.8 | 34.02 | 0.9031 |
| Medium | 37.1 | 32.44 | 0.8832 |
| High | 55.92 | 30.65 | 0.8580 |

**Finding:** Stronger quantisation discards more high-frequency information, so PSNR and SSIM drop and block artifacts become more visible around edges and fine textures.

---

### Problem 5 – Texture-Based Segmentation using GLCM
Extracted **contrast, energy and homogeneity** from 5×5 neighbourhoods and segmented the image into **k = 3** clusters with K-Means.

**Finding:** Contrast highlights texture variation, while energy and homogeneity identify uniform regions. Combining them works better than any single feature, though similar textures can still be grouped together.

---

### Problem 6 – Multi-Feature Segmentation for Disease Detection
Built a feature vector from **intensity**, **Sobel gradient magnitude** and **local 3×3 variance**, then segmented a leaf image with K-Means (k = 3).

**Findings:**
- Intensity was the most useful for separating dark diseased spots from healthy areas.
- Sobel gradient highlights leaf and spot boundaries.
- Misclassifications occur where diseased and healthy regions have similar intensity or texture, and background pixels can form their own cluster.

---

##  Input Images Required

Place these files in the same folder as the notebook:

`outdoor.jpg`, `smooth_image.jpg`, `city.jpg`, `texture.jpg`, `leaf_disease.jpg`

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. Install dependencies
pip install opencv-python numpy matplotlib scikit-image scikit-learn jupyter

# 3. Launch Jupyter and open the notebook
jupyter notebook IPP_Practical-2.ipynb
```

> **Note:** Problem 5 computes GLCM features pixel by pixel, so it can take a little while to run.

---

## Key Learnings

- Canny gives cleaner edges than Sobel or Laplacian, but all three are sensitive to noise without smoothing.
- Lossless methods like RLE and Huffman depend heavily on the image's pixel distribution.
- Quantisation in JPEG trades image quality (PSNR / SSIM) for compression.
- Choice of features strongly affects segmentation quality in K-Means.

---

## Author

**Meshwa**
PGDM – Big Data Analytics, AIDTM
