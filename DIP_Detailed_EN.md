# COMPREHENSIVE STUDY GUIDE: DIGITAL IMAGE PROCESSING (DIP)
*Author: Professor of Computer Science & Digital Image Processing*

Welcome to this comprehensive study guide for the **Digital Image Processing (DIP)** course. This document is a deeply analytical guide based strictly on the course lecture slides (Chapters 1 to 10) and practical labworks (Labwork 1 to 3). 

This guide uses clear, intuitive explanations, standard mathematical formulas in $\text{\LaTeX}$ notation, and concrete step-by-step practice questions with detailed solutions.

---

## TABLE OF CONTENTS

1. [Chapter 1: Introduction to Digital Image Processing](#1-chapter-1-introduction-to-digital-image-processing)
2. [Chapter 2: Digital Image Fundamentals](#2-chapter-2-digital-image-fundamentals)
3. [Chapter 3: Intensity Transformations and Histogram Processing](#3-chapter-3-intensity-transformations-and-histogram-processing)
4. [Chapter 4: Point Processing in the Spatial Domain](#4-chapter-4-point-processing-in-the-spatial-domain)
5. [Chapter 5: Spatial Filtering 1 - Image Smoothing](#5-chapter-5-spatial-filtering-1---image-smoothing)
6. [Chapter 6: Spatial Filtering 2 - Image Sharpening](#6-chapter-6-spatial-filtering-2---image-sharpening)
7. [Chapter 7: Filtering in the Frequency Domain](#7-chapter-7-filtering-in-the-frequency-domain)
8. [Chapter 8: Image Segmentation 1 - Point, Line, and Edge Detection](#8-chapter-8-image-segmentation-1---point-line-and-edge-detection)
9. [Chapter 9: Image Segmentation 2 - Thresholding](#9-chapter-9-image-segmentation-2---thresholding)
10. [Chapter 10: Morphological Image Processing](#10-chapter-10-morphological-image-processing)
11. [Detailed Solution to Labwork 1 Pen and Paper Exercises](#11-detailed-solution-to-labwork-1-pen-and-paper-exercises)
12. [Detailed Solution to Labwork 2 Pen and Paper Exercises](#12-detailed-solution-to-labwork-2-pen-and-paper-exercises)
13. [Detailed Solution to Labwork 3 Pen and Paper Exercises](#13-detailed-solution-to-labwork-3-pen-and-paper-exercises)

---

## 1. Chapter 1: Introduction to Digital Image Processing

### a. Core Concepts & Definitions
*   **Digital Image**: A representation of a two-dimensional image as a finite set of digital values, called picture elements or **pixels**.
*   **Pixel Value**: Typically represents gray levels, colors, heights, opacities, etc. For most of this course, we focus on grayscale images (1 sample per point).
*   **Digitization**: The process of converting a continuous real-world scene into a discrete digital image. This implies that a digital image is always an approximation of a real scene.
*   **Digital Image Processing (DIP)** focuses on two major tasks:
    1.  Improvement of pictorial information for human interpretation.
    2.  Processing of image data for storage, transmission, and representation for autonomous machine perception (computer vision).

### b. Hierarchy of Processes
The continuum from image processing to computer vision can be categorized into three levels:
1.  **Low-level Process**: Input is an image, output is an image. Examples: noise removal, image sharpening.
2.  **Mid-level Process**: Input is an image, output is attributes extracted from the image. Examples: segmentation, object recognition.
3.  **High-level Process**: Input is attributes, output is understanding (scene understanding, autonomous navigation).

### c. History and Practical Applications
*   **History**: Early applications include thenewspaper industry in the 1920s (Bartlane cable picture transmission service). In the 1960s, space missions like Ranger 7 used computers to improve the quality of images of the moon. In the 1970s, Computerised Axial Tomography (CAT) scan technology emerged, winning the Nobel prize in Medicine in 1979.
*   **Applications**: Medical visualization (MRI, CT scans), Geographic Information Systems (GIS - satellite imagery manipulation), Industrial Inspection (PCB inspection), Law Enforcement (number plate and fingerprint recognition), and Human-Computer Interfaces (HCI).

---

### d. Practice Questions & Solutions
**Question 1**: Describe the input-output characteristics of low-, mid-, and high-level image processes. Give a real-world example of each.
*   **Solution**:
    *   *Low-level process*: Input: Image $\rightarrow$ Output: Image. Example: Adjusting the brightness of a photo on your smartphone.
    *   *Mid-level process*: Input: Image $\rightarrow$ Output: Attributes. Example: A barcode scanner reading a barcode on a parcel to get the numerical ID.
    *   *High-level process*: Input: Attributes $\rightarrow$ Output: Cognitive Understanding. Example: An autonomous vehicle detecting a pedestrian and making the decision to brake.

**Question 2**: If a grayscale digital image has a size of $512 \times 512$ pixels, and each pixel can represent 256 gray levels, how many bits are required to store the image?
*   **Solution**:
    *   Since the number of gray levels is $L = 256$, and $L = 2^k$, we have $k = \log_2(256) = 8$ bits per pixel.
    *   Total number of pixels: $512 \times 512 = 262,144$ pixels.
    *   Total storage required: $262,144 \text{ pixels} \times 8 \text{ bits/pixel} = 2,097,152 \text{ bits} = 262,144 \text{ bytes} = 256 \text{ KB}$.

---

## 2. Chapter 2: Digital Image Fundamentals

### a. Human Visual System
*   **Structure of the Eye**: Light enters through the cornea and lens, and is projected onto the retina. The retina contains two main types of photoreceptors:
    *   **Cones**: 6-7 million cells concentrated in the fovea (center). High resolution, sensitive to color, responsible for photopic (daylight) vision.
    *   **Rods**: 75-150 million cells distributed over the retina. Low resolution, color-blind, highly sensitive to light, responsible for scotopic (night) vision.
*   **Blind Spot**: The point on the retina where the optic nerve exits; it contains no photoreceptors.
*   **Brightness Adaptation**: The human visual system cannot operate over its entire dynamic range ($10^{-6}$ to $10^{10}$ units) simultaneously. It adapts its overall sensitivity level. Brightness perception is a logarithmic function of physical light intensity.
*   **Brightness Discrimination**: The ability to distinguish small changes in illumination. It is characterized by the Weber ratio $\frac{\Delta I_c}{I}$, where $\Delta I_c$ is the minimum detectable change on a background intensity $I$.

### b. Optical Illusions
Optical illusions demonstrate that the human visual system does not see absolute light levels. Examples include:
*   *Mach Bands*: The visual system overshoots and undershoots at intensity transitions, making boundary lines appear darker or brighter.
*   *Simultaneous Contrast*: A gray square looks lighter on a black background than on a white background because the eye perceives brightness relative to the surrounding area.

### c. Image Sampling & Quantization
To transform a continuous analogue signal $f(x, y)$ into a digital image:
1.  **Sampling**: Discretizing the spatial coordinates $(x, y)$. This defines **spatial resolution**.
2.  **Quantization**: Discretizing the intensity value (amplitude). This defines **intensity resolution**. A digital image is represented as an $M \times N$ matrix with intensities ranging from $0$ to $L-1$ ($L = 2^k$ gray levels).

---

### d. Practice Questions & Solutions
**Question 1**: Explain the phenomenon of "Simultaneous Contrast" and its implications for how human beings perceive gray levels.
*   **Solution**:
    *   *Phenomenon*: The perceived brightness of a region depends strongly on its background. A gray target on a dark background appears brighter than the exact same target on a bright background.
    *   *Implication*: This occurs because the human eye is sensitive to local contrast boundaries (lateral inhibition in retinal cells) rather than absolute physical intensity. Therefore, when evaluating images visually, consistent background lighting conditions are essential to prevent subjective bias.

**Question 2**: If an image is sampled on a grid of $1024 \times 1024$ pixels and quantized to 8 bits, and we downsample it to $256 \times 256$ pixels and reduce quantization to 3 bits, what are the names of the visual artifacts that will appear?
*   **Solution**:
    1.  **Pixelation / Aliasing**: Reducing the spatial resolution ($1024 \rightarrow 256$) causes blockiness and jagged diagonal borders.
    2.  **False Contouring**: Reducing the quantization ($8 \text{ bits} \rightarrow 3 \text{ bits}$, or $256 \rightarrow 8$ gray levels) causes smooth gradient transitions to appear as discrete, jagged bands, like a topographic map.

---

## 3. Chapter 3: Intensity Transformations and Histogram Processing

### a. Grayscale & Image Enhancement
*   **Image Enhancement**: The process of highlighting certain features of interest in an image to make it more suitable for a specific application.
*   **Histogram**: A discrete function $h(r_k) = n_k$ representing the number of pixels $n_k$ in an image that have gray level $r_k$.
*   **Normalized Histogram**: $p(r_k) = \frac{n_k}{n}$, which represents the probability of occurrence of gray level $r_k$ in the image.

### b. Histogram Analysis
*   *Dark Image*: Histogram values are concentrated towards the low values (left).
*   *Bright Image*: Histogram values are concentrated towards the high values (right).
*   *Low-contrast Image*: Histogram is narrow and centered in the middle.
*   *High-contrast Image*: Histogram is broad, covering the entire range from $0$ to $L-1$.

### c. Histogram Equalization Algorithm
*   **Objective**: Automatically find a transformation function $s = T(r)$ that produces an output image with a uniform (flat) histogram, maximizing contrast.
*   **Mathematical formulation (Continuous)**:
    $$s = T(r) = (L-1) \int_{0}^{r} p_r(w) dw$$
*   **Mathematical formulation (Discrete)**:
    $$s_k = T(r_k) = (L-1) \sum_{j=0}^{k} p_r(r_j) = \frac{L-1}{n} \sum_{j=0}^{k} n_j, \quad k = 0, 1, \dots, L-1$$
    The resulting $s_k$ values are rounded to the nearest integer.

---

### d. Practice Questions & Solutions
**Question 1**: Explain why discrete histogram equalization does not usually yield a perfectly flat histogram.
*   **Solution**:
    In discrete image processing, gray level values are mapped as indivisible pixel groups. When we apply the transformation function, entire groups of pixels at a specific gray level are shifted to a new gray level. They cannot be split or spread out. Thus, instead of a perfectly continuous flat distribution, we get a stretched histogram with gaps between populated bins, representing an approximation of a uniform distribution.

**Question 2**: A $4 \times 4$ pixel image ($n=16$) has a 4-level gray scale ($L=4$, levels $0, 1, 2, 3$). The histogram is $n_0 = 4, n_1 = 8, n_2 = 2, n_3 = 2$. Compute the mapped equalized gray levels.
*   **Solution**:
    *   *Step 1*: Calculate normalized histogram $p(r_k) = n_k / 16$:
        *   $p(r_0) = 4/16 = 0.25$
        *   $p(r_1) = 8/16 = 0.50$
        *   $p(r_2) = 2/16 = 0.125$
        *   $p(r_3) = 2/16 = 0.125$
    *   *Step 2*: Calculate cumulative distribution function (CDF):
        *   $\text{CDF}(0) = 0.25$
        *   $\text{CDF}(1) = 0.25 + 0.50 = 0.75$
        *   $\text{CDF}(2) = 0.75 + 0.125 = 0.875$
        *   $\text{CDF}(3) = 0.875 + 0.125 = 1.00$
    *   *Step 3*: Compute $s_k = \text{round}(3 \times \text{CDF}(r_k))$:
        *   $s_0 = \text{round}(3 \times 0.25) = \text{round}(0.75) = 1$
        *   $s_1 = \text{round}(3 \times 0.75) = \text{round}(2.25) = 2$
        *   $s_2 = \text{round}(3 \times 0.875) = \text{round}(2.625) = 3$
        *   $s_3 = \text{round}(3 \times 1.00) = \text{round}(3.00) = 3$
    *   *Resulting mapping*: $0 \rightarrow 1, 1 \rightarrow 2, 2 \rightarrow 3, 3 \rightarrow 3$.

---

## 4. Chapter 4: Point Processing in the Spatial Domain

### a. Spatial Domain Transform Function
Point processing operates on individual pixels independently:
$$s = T(r)$$
where $r$ is the input intensity and $s$ is the output intensity.

### b. Basic Intensity Transformations
1.  **Image Negatives**:
    $$s = (L-1) - r$$
    *Use case*: Useful for enhancing white or light detail embedded in dark regions of an image (e.g., medical X-rays or scanning photographic negatives).
2.  **Log Transformation**:
    $$s = c \log(1 + r)$$
    *Use case*: Compresses the dynamic range of images with large variations in pixel values. It expands dark values and compresses bright values (e.g., displaying the Fourier spectrum).
3.  **Power-Law / Gamma Transformation**:
    $$s = c r^\gamma$$
    *Use case*:
    *   $\gamma < 1$: Brightens the image (expands dark values).
    *   $\gamma > 1$: Darkens the image (expands bright values).
    *   *Gamma Correction*: Sells the non-linear relationship between voltage and brightness in monitors.

---

### c. Practice Questions & Solutions
**Question 1**: A display monitor has a device response characterized by a power-law exponent of $\gamma = 2.0$. If we want to display an image with correct linear intensity, what transformation must we apply to the image signal beforehand?
*   **Solution**:
    We must apply a gamma correction step to the image signal. The transformation is:
    $$s = r^{1/\gamma} = r^{1/2.0} = r^{0.5}$$
    When the monitor displays $s$, its physical output will be $s^\gamma = (r^{0.5})^2 = r$, restoring the linear intensity representation.

**Question 2**: For a grayscale image where pixel intensities are normalized in range $[0, 1]$, calculate the output intensity for a pixel with input $r=0.25$ using a power-law transformation with $\gamma = 0.5$ and $c=1$.
*   **Solution**:
    Using the formula $s = c r^\gamma$:
    $$s = 1 \times (0.25)^{0.5} = \sqrt{0.25} = 0.5$$
    The pixel value increases from $0.25$ to $0.5$, which represents image brightening.

---

## 5. Chapter 5: Spatial Filtering 1 - Image Smoothing

### a. Spatial Filtering Mechanism
Spatial filtering applies a filter mask (kernel/template) of odd dimensions over every pixel of the image. The output value at the center is the sum of products of the mask coefficients and the corresponding pixel values.
*   **Correlation**:
    $$g(x, y) = \sum_{s=-a}^{a} \sum_{t=-b}^{b} w(s, t) f(x+s, y+t)$$
*   **Convolution**: Identical to correlation, but the mask is rotated by $180^\circ$ first. For symmetric kernels, correlation and convolution are identical.

### b. Image Smoothing (Blurring) Filters
Smoothing filters reduce noise and blur edges/details for segmentation.
1.  **Averaging / Box Filter**:
    All coefficients are equal and sum to 1. Example ($3 \times 3$):
    $$K = \frac{1}{9} \begin{bmatrix} 1 & 1 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{bmatrix}$$
2.  **Weighted Average Filter**:
    Assigns higher weights to pixels closer to the center of the mask. Example ($3 \times 3$):
    $$K = \frac{1}{16} \begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{bmatrix}$$
3.  **Median Filter (Non-linear)**:
    Replaces the center pixel value with the median of the neighborhood values.
    *Key Advantage*: Highly effective at removing **salt-and-pepper noise** while preserving sharp edge boundaries.

---

### c. Practice Questions & Solutions
**Question 1**: Explain the visual difference between applying a $3 \times 3$ box filter and a $9 \times 9$ box filter to an image.
*   **Solution**:
    *   The $3 \times 3$ filter averages over 9 pixels. It blurs small details and reduces fine noise, keeping overall structures visible.
    *   The $9 \times 9$ filter averages over 81 pixels. It blurs the image significantly, turning sharp edges into wide gradients, and completely removes small details. It is suitable only for coarse features.

**Question 2**: Given the following $3 \times 3$ neighborhood:
$$I = \begin{bmatrix} 12 & 15 & 13 \\ 14 & 250 & 16 \\ 12 & 13 & 15 \end{bmatrix}$$
Find the output value at the center pixel after:
1. A $3 \times 3$ box filter.
2. A $3 \times 3$ median filter.
*   **Solution**:
    1.  *Box Filter*:
        $$\text{Sum} = 12 + 15 + 13 + 14 + 250 + 16 + 12 + 13 + 15 = 360$$
        $$\text{Output} = \frac{360}{9} = 40$$
    2.  *Median Filter*:
        List values: $\{12, 12, 13, 13, 14, 15, 15, 16, 250\}$.
        Sorted: $12, 12, 13, 13, \mathbf{14}, 15, 15, 16, 250$.
        Median (5th value) is $14$.
        *Comparison*: The center pixel was an outlier (value 250). The box filter smoothed it to 40 (still affected), while the median filter completely rejected it, replacing it with the typical background value of 14.

---

## 6. Chapter 6: Spatial Filtering 2 - Image Sharpening

### a. Goal of Image Sharpening
Sharpening highlights transitions in intensity, enhancing edges and fine detail while reducing flat regions.

### b. Differentiation in the Spatial Domain
*   **First Derivative**:
    $$\frac{\partial f}{\partial x} = f(x+1) - f(x)$$
    *Behavior*: Responds strongly to steep transitions (ramps and steps). Used for gradient-based edge detection.
*   **Second Derivative**:
    $$\frac{\partial^2 f}{\partial x^2} = f(x+1) + f(x-1) - 2f(x)$$
    *Behavior*: Responds to fine lines, isolated points, and produces a double-line response across transitions.

### c. The Laplacian Operator
*   The **Laplacian** is an isotropic, linear second-order derivative operator:
    $$\nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}$$
*   Discrete form on a $3 \times 3$ grid:
    $$\nabla^2 f(x, y) = f(x+1, y) + f(x-1, y) + f(x, y+1) + f(x, y-1) - 4f(x, y)$$
*   Common mask templates (with negative center coefficient):
    $$K = \begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix} \quad \text{or diagonals included:} \quad \begin{bmatrix} 1 & 1 & 1 \\ 1 & -8 & 1 \\ 1 & 1 & 1 \end{bmatrix}$$

### d. Image Sharpening with the Laplacian
We sharpen the image by adding the derivative detail back to the original image:
*   If the center coefficient is **negative** (e.g., $-4$ or $-8$):
    $$g(x, y) = f(x, y) - \nabla^2 f(x, y)$$
*   If the center coefficient is **positive**:
    $$g(x, y) = f(x, y) + \nabla^2 f(x, y)$$

---

### e. Practice Questions & Solutions
**Question 1**: Why does the second derivative respond more strongly to noise than the first derivative?
*   **Solution**:
    Noise represents rapid, high-frequency oscillations. The first derivative measures the slope (rate of change). The second derivative measures the curvature (rate of change of slope). Rapid transitions in noise cause steep slopes that reverse direction immediately. The second derivative amplifies these reversals, resulting in a very high output value.

**Question 2**: Given the following image neighborhood:
$$f = \begin{bmatrix} 10 & 10 & 10 \\ 10 & 90 & 10 \\ 10 & 10 & 10 \end{bmatrix}$$
Compute the sharpened center value using a Laplacian mask with a center coefficient of $-4$.
*   **Solution**:
    *   *Step 1*: Calculate the Laplacian value $\nabla^2 f$:
        $$\nabla^2 f = (10 \times 1) + (10 \times 1) + (10 \times 1) + (10 \times 1) + (90 \times -4) = 40 - 360 = -320$$
    *   *Step 2*: Apply the sharpening formula:
        $$g(x, y) = f(x, y) - \nabla^2 f(x, y) = 90 - (-320) = 410$$
    *   *Step 3*: Since $410 > 255$, we clip the output to $255$ for an 8-bit image.

---

## 7. Chapter 7: Filtering in the Frequency Domain

### a. The Fourier Transform
Any periodic function can be expressed as a sum of sines and cosines of different frequencies. For non-periodic digital images, we use the **2D Discrete Fourier Transform (DFT)**.

### b. DFT & IDFT Formulas
*   **2D Discrete Fourier Transform**:
    $$F(u, v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) e^{-j 2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)}$$
*   **2D Inverse Discrete Fourier Transform**:
    $$f(x, y) = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u, v) e^{j 2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)}$$

### c. Frequency Domain Filtering Steps
1.  Multiply the input image by $(-1)^{x+y}$ to center the transform.
2.  Compute the 2D DFT $F(u, v)$ of the image.
3.  Multiply $F(u, v)$ by a filter function $H(u, v)$: $G(u, v) = H(u, v) F(u, v)$.
4.  Compute the 2D IDFT of $G(u, v)$.
5.  Take the real part and multiply by $(-1)^{x+y}$ to obtain the filtered image.

### d. Frequency Domain Filters
Let the distance function be $D(u, v) = \sqrt{(u - M/2)^2 + (v - N/2)^2}$, and let $D_0$ be the cut-off frequency.
The high-pass transfer function is: $H_{hp}(u, v) = 1 - H_{lp}(u, v)$.

| Filter Type | Low-pass (Smoothing - $H_{lp}$) | High-pass (Sharpening - $H_{hp}$) | Characteristics |
| :--- | :--- | :--- | :--- |
| **Ideal** | $H = \begin{cases} 1 & D \le D_0 \\ 0 & D > D_0 \end{cases}$ | $H = \begin{cases} 0 & D \le D_0 \\ 1 & D > D_0 \end{cases}$ | Sharp cutoff causes strong **ringing artifacts** in the spatial domain. |
| **Butterworth** | $H = \frac{1}{1 + [D/D_0]^{2n}}$ | $H = \frac{1}{1 + [D_0/D]^{2n}}$ | Smooth transition. Higher orders $n$ lead to more ringing. |
| **Gaussian** | $H = e^{-D^2/2D_0^2}$ | $H = 1 - e^{-D^2/2D_0^2}$ | **No ringing artifacts** because its spatial representation is Gaussian. |

---

### e. Practice Questions & Solutions
**Question 1**: Explain the relationship between the Fourier transform of an image and the spatial domain representation of its edges.
*   **Solution**:
    Edges represent rapid transitions in intensity over a short distance, which corresponds to high-frequency components. In the Fourier spectrum, these high-frequency components are located far from the origin. Therefore, filtering out high frequencies (low-pass filtering) blurs edges, while filtering out low frequencies (high-pass filtering) isolates edges.

**Question 2**: For a centered $128 \times 128$ image frequency space, compute the value of a Gaussian Low-pass Filter with $D_0 = 10$ at frequency coordinates $(u, v) = (64, 74)$.
*   **Solution**:
    *   The center of the frequency domain is $(64, 64)$.
    *   Distance $D(u,v)$:
        $$D(64, 74) = \sqrt{(64-64)^2 + (74-64)^2} = 10$$
    *   Hvalue:
        $$H(64, 74) = e^{-D^2/2D_0^2} = e^{-10^2/(2 \times 10^2)} = e^{-100/200} = e^{-0.5} \approx 0.6065$$

---

## 8. Chapter 8: Image Segmentation 1 - Point, Line, and Edge Detection

### a. Discontinuities in Grayscale Images
We segment images by detecting three types of gray-level discontinuities:
1.  **Points**: Isolated pixels that differ significantly from their background.
2.  **Lines**: Pixels forming a line of 1-pixel thickness in a specific direction.
3.  **Edges**: Boundaries between two regions of different intensities.

### b. Discontinuity Detection Masks ($3 \times 3$)
*   **Point Detection Mask**:
    $$K = \begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix}$$
*   **Line Detection Masks**:
    *   *Horizontal*: $\begin{bmatrix} -1 & -1 & -1 \\ 2 & 2 & 2 \\ -1 & -1 & -1 \end{bmatrix}$
    *   *Vertical*: $\begin{bmatrix} -1 & 2 & -1 \\ -1 & 2 & -1 \\ -1 & 2 & -1 \end{bmatrix}$

### c. Edge Detection with Gradient (Sobel)
An edge is characterized by local gradient magnitude. We compute directional derivatives $G_x$ and $G_y$:
$$G_x = \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix}, \quad G_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}$$
*   **Gradient Magnitude**:
    $$G(x, y) = \sqrt{G_x^2 + G_y^2}$$

### d. Noise & Laplacian of Gaussian (LoG)
Derivative operators amplify noise. To prevent false edges, we smooth the image first. The **Laplacian of Gaussian (LoG)** combines Gaussian smoothing and Laplacian differentiation into a single filter mask:
$$\text{LoG}(x, y) = \left[ \frac{x^2 + y^2 - 2\sigma^2}{\sigma^4} \right] e^{-\frac{x^2 + y^2}{2\sigma^2}}$$

---

### e. Practice Questions & Solutions
**Question 1**: Compare the behavior of the Sobel operator and the Laplacian operator for edge detection.
*   **Solution**:
    *   *Sobel operator*: Computes the first derivative. It produces a thick edge response where gradient transitions occur. It is less sensitive to noise and provides direction information.
    *   *Laplacian operator*: Computes the second derivative. It produces thin, double-line responses and zero-crossings. It is isotropic (direction-independent) but highly sensitive to noise.

**Question 2**: Given the following pixel neighborhood:
$$J = \begin{bmatrix} 10 & 10 & 10 \\ 10 & 10 & 10 \\ 90 & 90 & 90 \end{bmatrix}$$
Apply the $G_y$ Sobel kernel and compute its output at the center.
*   **Solution**:
    Using the $G_y$ Sobel kernel:
    $$G_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}$$
    $$G_y \ast J = (10 \times -1) + (10 \times -2) + (10 \times -1) + 0 + (90 \times 1) + (90 \times 2) + (90 \times 1) = -40 + 360 = 320$$

---

## 9. Chapter 9: Image Segmentation 2 - Thresholding

### a. Intensity Thresholding
Thresholding converts a grayscale image into a binary image:
$$g(x, y) = \begin{cases} 1 & f(x, y) \ge T \\ 0 & f(x, y) < T \end{cases}$$
where $T$ is a threshold value.

### b. Basic Global Thresholding Algorithm
When the histogram of an image is bimodal, we can iteratively calculate an optimal threshold $T$:
1.  Select an initial estimate for $T$ (typically the average gray level of the image).
2.  Segment the image using $T$ into two groups of pixels: $G_1$ (gray levels $> T$) and $G_2$ (gray levels $\le T$).
3.  Compute the average gray levels $\mu_1$ of $G_1$ and $\mu_2$ of $G_2$.
4.  Compute a new threshold value:
    $$T_{new} = \frac{\mu_1 + \mu_2}{2}$$
5.  Repeat steps 2–4 until the difference in $T$ in successive iterations is less than a predefined limit $T_\infty$.

### c. Limitations & Adaptive Thresholding
*   **Limitation**: Global thresholding fails under uneven illumination.
*   **Adaptive Thresholding**: Divide the image into sub-images and compute a threshold for each sub-image individually.

---

### d. Practice Questions & Solutions
**Question 1**: Explain why uneven illumination prevents global thresholding from working.
*   **Solution**:
    Uneven illumination shifts the gray levels of the background in bright areas to overlap with the gray levels of the foreground object in dark areas. A single global threshold cannot separate them, resulting in false background or foreground pixels.

**Question 2**: Given pixel values $\{1, 3, 5, 11, 13, 17\}$, apply the iterative global thresholding algorithm with an initial threshold $T_0 = 8$ and limit $T_\infty = 0.5$.
*   **Solution**:
    *   *Iteration 1*:
        *   Group $G_1$ ($>8$): $\{11, 13, 17\}$. Mean $\mu_1 = (11+13+17)/3 = 13.67$.
        *   Group $G_2$ ($\le 8$): $\{1, 3, 5\}$. Mean $\mu_2 = (1+3+5)/3 = 3$.
        *   New threshold: $T_1 = (13.67 + 3)/2 = 8.33$.
    *   *Check convergence*: $|T_1 - T_0| = |8.33 - 8| = 0.33 < 0.5$. The algorithm terminates.
    *   *Final Threshold*: $8.33$ (or rounded to $8$).

---

## 10. Chapter 10: Morphological Image Processing

### a. Mathematical Morphology
Morphological image processing extracts image components representing shape or boundary structure. It operates on binary images using set theory.

### b. Structuring Element (SE)
A small binary matrix with an origin. It is placed at every position of the image:
*   **Fit**: All elements of the SE with value 1 overlap with 1-valued pixels in the image.
*   **Hit**: At least one element of the SE with value 1 overlaps with a 1-valued pixel in the image.

### c. Fundamental Morphological Operations
1.  **Erosion ($\ominus$)**:
    $$A \ominus B = \{ z \mid (B)_z \subseteq A \}$$
    *Rule*: Output is 1 if SE **fits** the image. It shrinks foreground objects and removes small noise pixels.
2.  **Dilation ($\oplus$)**:
    $$A \oplus B = \{ z \mid (\hat{B})_z \cap A \neq \varnothing \}$$
    *Rule*: Output is 1 if SE **hits** the image. It expands objects and fills small holes or gaps.
3.  **Opening ($\circ$)**: Erosion followed by Dilation.
    $$A \circ B = (A \ominus B) \oplus B$$
    *Use*: Smooths contours, eliminates small protrusions, and breaks thin connections.
4.  **Closing ($\bullet$)**: Dilation followed by Erosion.
    $$A \bullet B = (A \oplus B) \ominus B$$
    *Use*: Fills small holes, fuses narrow gaps, and joins split components.

---

### d. Practice Questions & Solutions
**Question 1**: Sketch the result of opening a binary image containing a square of $5 \times 5$ pixels and a single noise pixel of $1 \times 1$ using a structuring element of size $3 \times 3$ filled with 1s.
*   **Solution**:
    *   *Erosion*: The $3 \times 3$ SE cannot fit inside the $1 \times 1$ noise pixel, so it is deleted. The $5 \times 5$ square is eroded to a $3 \times 3$ square.
    *   *Dilation*: The remaining $3 \times 3$ square is dilated back to its original $5 \times 5$ size.
    *   *Final Result*: The $5 \times 5$ square remains unchanged, while the $1 \times 1$ noise pixel is completely removed.

**Question 2**: Given binary image $A$ and structuring element $B$ (origin at center):
$$A = \begin{bmatrix} 0 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 0 \end{bmatrix}, \quad B = \begin{bmatrix} 0 & 1 & 0 \\ 1 & 1 & 1 \\ 0 & 1 & 0 \end{bmatrix}$$
Compute the dilation $A \oplus B$ assuming zero-padding.
*   **Solution**:
    Dilation gans a 1 wherever $B$ hits $A$. Since the only 1 in $A$ is at $(1, 1)$, $B$ will hit the image when its origin is at $(1, 1)$, $(0, 1)$, $(2, 1)$, $(1, 0)$, and $(1, 2)$.
    $$\text{Dilation } A \oplus B = \begin{bmatrix} 0 & 1 & 0 \\ 1 & 1 & 1 \\ 0 & 1 & 0 \end{bmatrix}$$

---

## 11. Detailed Solution to Labwork 1 Pen and Paper Exercises

### **Task A1**
Given the following image $I$ (4x4):
$$I = \begin{bmatrix} 0 & 1 & 1 & 2 \\ 2 & 3 & 3 & 4 \\ 4 & 5 & 6 & 6 \\ 5 & 6 & 7 & 7 \end{bmatrix}$$

#### 1. Histogram and Normalized Histogram
Total pixels $n = 16$. Gray scale levels $[0, 7]$ ($L=8$).
*   **Frequencies**:
    *   Level $0$: $1$ occurrence.
    *   Level $1$: $2$ occurrences.
    *   Level $2$: $2$ occurrences.
    *   Level $3$: $2$ occurrences.
    *   Level $4$: $2$ occurrences.
    *   Level $5$: $2$ occurrences.
    *   Level $6$: $3$ occurrences.
    *   Level $7$: $2$ occurrences.
*   **Histogram $h(r)$**:
    $$h(r) = [1, 2, 2, 2, 2, 2, 3, 2]$$
*   **Normalized Histogram $p(r)$**:
    $$p(r) = [0.0625, 0.125, 0.125, 0.125, 0.125, 0.125, 0.1875, 0.125]$$

#### 2. Equalized Histogram and New Image $M$
*   **Cumulative Distribution Function (CDF)**:
    *   $\text{CDF}(0) = 0.0625$
    *   $\text{CDF}(1) = 0.1875$
    *   $\text{CDF}(2) = 0.3125$
    *   $\text{CDF}(3) = 0.4375$
    *   $\text{CDF}(4) = 0.5625$
    *   $\text{CDF}(5) = 0.6875$
    *   $\text{CDF}(6) = 0.875$
    *   $\text{CDF}(7) = 1.00$
*   **Equalization Mapping**: $s_k = \text{round}(7 \times \text{CDF}(r_k))$
    *   $s_0 = \text{round}(7 \times 0.0625) = \text{round}(0.4375) = 0$
    *   $s_1 = \text{round}(7 \times 0.1875) = \text{round}(1.3125) = 1$
    *   $s_2 = \text{round}(7 \times 0.3125) = \text{round}(2.1875) = 2$
    *   $s_3 = \text{round}(7 \times 0.4375) = \text{round}(3.0625) = 3$
    *   $s_4 = \text{round}(7 \times 0.5625) = \text{round}(3.9375) = 4$
    *   $s_5 = \text{round}(7 \times 0.6875) = \text{round}(4.8125) = 5$
    *   $s_6 = \text{round}(7 \times 0.875) = \text{round}(6.125) = 6$
    *   $s_7 = \text{round}(7 \times 1.00) = \text{round}(7.00) = 7$
*   **Inferred Image $M$**:
    Since the mapped values are identical to the input values ($s_k = k$), the equalized image $M$ is identical to $I$:
    $$M = \begin{bmatrix} 0 & 1 & 1 & 2 \\ 2 & 3 & 3 & 4 \\ 4 & 5 & 6 & 6 \\ 5 & 6 & 7 & 7 \end{bmatrix}$$
    *Theoretical Explanation*: The input image $I$ has an almost uniform histogram (each level appears 2 times, except level 0 once and level 6 three times). Because the image already has optimal contrast distribution, the equalization mapping is the identity mapping.

#### 3. Binary Image $B$ using Median Threshold $k$
*   **Find Median**:
    Sorted list of pixels: $0, 1, 1, 2, 2, 3, 3, \mathbf{4, 4}, 5, 5, 6, 6, 6, 7, 7$.
    Since $n=16$, the median is the average of the 8th and 9th values:
    $$k = \frac{4 + 4}{2} = 4$$
*   **Thresholding**: $B(x, y) = 1$ if $I(x, y) \ge 4$, else $0$.
    $$B = \begin{bmatrix} 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \end{bmatrix}$$

#### 4. Negative Image of $I$
Using $s = 7 - r$:
$$\text{Negative } I = \begin{bmatrix} 7 & 6 & 6 & 5 \\ 5 & 4 & 4 & 3 \\ 3 & 2 & 1 & 1 \\ 2 & 1 & 0 & 0 \end{bmatrix}$$

---

### **Task A2**
Given the following image $J$ (5x5):
$$J = \begin{bmatrix} 0 & 2 & 2 & 3 & 6 \\ 1 & 2 & 3 & 3 & 6 \\ 2 & 3 & 3 & 4 & 7 \\ 1 & 2 & 3 & 3 & 7 \\ 0 & 2 & 4 & 5 & 6 \end{bmatrix}$$

#### 1. Histogram and Normalized Histogram
Total pixels $n = 25$.
*   **Frequencies**: $h = [2, 2, 6, 7, 2, 1, 3, 2]$ for levels $0..7$.
*   **Normalized Histogram**: $p = [0.08, 0.08, 0.24, 0.28, 0.08, 0.04, 0.12, 0.08]$.

#### 2. Identify the Gray-Level Mode
The mode is the value with the highest frequency. Level $3$ appears $7$ times, so **mode = 3**.

#### 3. Binary Image $B_J$ using Threshold $k = \text{mode} = 3$
*   $B_J(x, y) = 1$ if $J(x, y) \ge 3$, else $0$.
    $$B_J = \begin{bmatrix} 0 & 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 \end{bmatrix}$$
*   **Pixel Count**:
    *   Foreground ($B_J = 1$): **15 pixels**.
    *   Background ($B_J = 0$): **10 pixels**.

#### 4. Does $k=3$ Separate Low- and High-Intensity Pixels Well?
*   *Evaluation*: The threshold separates them moderately, but not optimally.
*   *Explanation*: The histogram show that $52\%$ of the pixels lie in levels $2$ and $3$ (13 out of 25 pixels). Selecting a threshold $k=3$ places all pixels of level 3 (mid-tones) into the foreground class, making the foreground size larger than the background. If we wanted to separate low-intensity (dark) from high-intensity (bright) pixels, a threshold of $k=4$ or $k=5$ would be better, since it would place the mid-tones in the background class.

---

## 12. Detailed Solution to Labwork 2 Pen and Paper Exercises

### **Task A1**
Given the following image $I$ (3x3):
$$I = \begin{bmatrix} 104 & 100 & 108 \\ 99 & 106 & 98 \\ 95 & 90 & 85 \end{bmatrix}$$

#### 1. Apply 3x3 Averaging Filter $K_1$
$$O_{K1} = \frac{104 + 100 + 108 + 99 + 106 + 98 + 95 + 90 + 85}{9} = \frac{885}{9} \approx \mathbf{98.3333}$$

#### 2. Apply 3x3 Weighted Averaging Filter $K_2 = \frac{1}{16} \begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{bmatrix}$
$$\text{Sum} = 104(1) + 100(2) + 108(1) + 99(2) + 106(4) + 98(2) + 95(1) + 90(2) + 85(1) = 1590$$
$$O_{K2} = \frac{1590}{16} = \mathbf{99.375}$$

#### 3. Comparison
$O_{K2} = 99.375$ is closer to the original center value ($106$) than $O_{K1} = 98.3333$. This is because $K_2$ gives a weight of $4/16 = 25\%$ to the center pixel, whereas $K_1$ gives a weight of only $1/9 \approx 11.1\%$. The weighted filter preserves more original detail, while $K_1$ blurs the center value more.

---

### **Task A2**
Given the following image $I$ (3x3):
$$I = \begin{bmatrix} 12 & 13 & 14 \\ 15 & 255 & 16 \\ 14 & 13 & 12 \end{bmatrix}$$

#### 1. Apply 3x3 Median Filter
*   Collect pixel values: $\{12, 13, 14, 15, 255, 16, 14, 13, 12\}$.
*   Sorted: $12, 12, 13, 13, \mathbf{14}, 14, 15, 16, 255$.
*   Median: **14**.
*   The new center pixel value is **14**.

#### 2. Effectiveness for Salt-and-Pepper Noise
Salt-and-pepper noise appears as isolated extreme values (0 or 255). When we sort the neighborhood values, these extremes are placed at the ends of the sorted list. Since the median filter selects the middle value, it rejects these outliers. Here, the noise value 255 is replaced by 14, restoring the local background value.

---

### **Task A3**
Given the following image $I$ and point detection mask $K$:
$$I = \begin{bmatrix} 10 & 10 & 10 \\ 10 & 50 & 10 \\ 10 & 10 & 10 \end{bmatrix}, \quad K = \begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix}$$

#### 1. Compute Center Output
$$\text{Output} = 50(8) + 10(-1 -1 -1 -1 -1 -1 -1 -1) = 400 - 80 = \mathbf{320}$$

#### 2. Explanation
The mask coefficients sum to 0. In flat areas of constant intensity $C$, the output is $(-8)C + 8C = 0$. However, at an isolated bright point (center is 50, neighbors are 10), the center is multiplied by a large positive coefficient ($8$) and neighbors by negative coefficients ($-1$). This difference produces a strong response ($320$), highlighting point discontinuities.

---

### **Task A4**
Given the following image $J$ and Sobel kernels $G_x, G_y$:
$$J = \begin{bmatrix} 10 & 10 & 10 \\ 20 & 20 & 20 \\ 100 & 100 & 100 \end{bmatrix}$$
$$G_x = \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix}, \quad G_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}$$

#### 1. Compute $G_x, G_y$ and Gradient Magnitude $G$
*   **$G_x$ (Horizontal)**:
    $$G_x = -10 + 10 - 40 + 40 - 100 + 100 = \mathbf{0}$$
*   **$G_y$ (Vertical)**:
    $$G_y = -10 - 20 - 10 + 0 + 100 + 200 + 100 = \mathbf{360}$$
*   **Magnitude $G$**:
    $$G = \sqrt{0^2 + 360^2} = \mathbf{360}$$

#### 2. Determine Edge Direction
*   *Conclusion*: The main edge is **horizontal**.
*   *Explanation*: The gradient component $G_x$ is 0 (no change horizontally), while $G_y = 360$ (significant change vertically). The gradient vector points vertically, which means the edge (orthogonal to the gradient) runs horizontally. This matches the image $J$, where rows are constant horizontally.

---

### **Task A5**
Given the following image $J$:
$$J = \begin{bmatrix} 10 & 10 & 10 \\ 10 & 50 & 10 \\ 10 & 10 & 10 \end{bmatrix}$$
Apply Laplacian kernel $K = \begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix}$.

#### 1. Compute Laplacian Value $\nabla^2 J$ at Center
$$\nabla^2 J = 10 + 10 + 10 + 10 - 4(50) = 40 - 200 = \mathbf{-160}$$

#### 2. Compute Sharpened Center Pixel
Since the center coefficient is negative ($-4$), we subtract the Laplacian:
$$g(x, y) = f(x, y) - \nabla^2 f(x, y) = 50 - (-160) = \mathbf{210}$$

---

## 13. Detailed Solution to Labwork 3 Pen and Paper Exercises

Given binary image $I$ (8x10) and structuring element $S$ (3x3) representing a cross. Assume zero-padding.

$$I = \begin{bmatrix} 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 0 \\ 
0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 
\end{bmatrix}, \quad 
S = \begin{bmatrix} 
0 & 1 & 0 \\ 
1 & 1 & 1 \\ 
0 & 1 & 0 
\end{bmatrix}$$

### **1. Erosion ($I \ominus S$)**
Erosion keeps a 1 at $(r, c)$ only if the cross structuring element $S$ **fits** inside the 1s of $I$:
$$\text{Erosion } (I \ominus S) = \begin{bmatrix} 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 
\end{bmatrix}$$

---

### **2. Dilation ($I \oplus S$)**
Dilation sets a 1 at $(r, c)$ if the structuring element $S$ **hits** at least one 1 in $I$:
$$\text{Dilation } (I \oplus S) = \begin{bmatrix} 
0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 0 \\ 
0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\ 
0 & 0 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\ 
1 & 1 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\ 
1 & 1 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\ 
1 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 
\end{bmatrix}$$

---

### **3. Opening ($I \circ S = (I \ominus S) \oplus S$)**
Perform dilation on the erosion result obtained in step 1:
$$\text{Opening } (I \circ S) = \begin{bmatrix} 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 
\end{bmatrix}$$

---

### **4. Closing ($I \bullet S = (I \oplus S) \ominus S$)**
Perform erosion on the dilation result obtained in step 2:
$$\text{Closing } (I \bullet S) = \begin{bmatrix} 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 0 \\ 
0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\ 
0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 
\end{bmatrix}$$

---
*End of Guide. Good luck with your Digital Image Processing studies and exams!*
