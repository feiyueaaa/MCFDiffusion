#  The author is currently organizing the relevant code and data. Please wait patiently.
# MFCDiffusion
 This is the codebase for Multi Channel Fusion Diffusion Models for Brain Tumor MRI Data Augmentation
## Model prototype
 The model prototype of this project is guided-diffusio, and this project does not perform any other operations on the network. It merely changes the input channels to 9 channels.
 
## Data processing flow
First, use cat_image.ipynb to combine three consecutive images with consecutive masks to form a large side-by-side image, such as:

![img](./img/img1.png)

![img](./img/img2.png)

Then Extract the abnormal area through extract the tumor area.ipynb:

![img](./img/img3.png)

## Image fusion and denoising

### Fusion Method 1
![img](./img/img4.png)

First, add the T-step noise to the tumor area and the healthy brain MRI image (since the noise level needs to be halved after this), then add the two images to obtain the middle image, and finally denoise the middle image to obtain the final result.
The code is located in fusion/fusion1.ipynb

### Fusion Method 2
![img](./img/img5.png)

First, add the tumor area to the MRI images of a healthy brain, then add the denoising T-step to obtain the middle image, and finally denoise the middle image for the T-step to obtain the final result.
The code is located in fusion/fusion2.ipynb

## Algorithm workflow
### MCFDiffusion Algorithm


**Algorithm 1 MCFDiffusion**

1: **input**₁: Three adjacent healthy brain MRI images were randomly selected as \( \mathbf{a} \).

2: **input**₂: The tumor regions of three randomly adjacent brain tumor MRIs were extracted as \( \mathbf{b} \).

3: \(\mathbf{x}_L \leftarrow \sqrt{\bar{\alpha}_L} \mathbf{a} + \frac{1}{2}\sqrt{1 - \bar{\alpha}_L} \boldsymbol{\epsilon} + \sqrt{\bar{\alpha}_L} \mathbf{b} + \frac{1}{2}\sqrt{1 - \bar{\alpha}_L} \boldsymbol{\epsilon}\)

4: **for** \( t = L, L-1, \ldots, 1 \) **do**

5: $$\(\quad \boldsymbol{\epsilon}' \leftarrow \epsilon_{\theta}^{(t)}(\mathbf{x}_t) - w\sqrt{1-\bar{\alpha}_t} \nabla \log p_{\phi}(y|\mathbf{x}_t)\)$$

6: \(\quad \mathbf{x}_{t-1} \leftarrow \sqrt{\alpha_{t-1}} \left( \frac{\mathbf{x}_t - \sqrt{1 - \alpha_t} \boldsymbol{\epsilon}'}{\sqrt{\alpha_t}} \right) + \sqrt{1 - \alpha_{t-1} - \sigma_t^2} \cdot \boldsymbol{\epsilon}'\)

7: **end for**

8: **return** \(\mathbf{x}_0\)
![img](./img/img6.png)
## Result

### Image quality

### Image classification

### Image Image segmentation
