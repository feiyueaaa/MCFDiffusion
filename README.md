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

## Image denoising

## Result

### Image quality

### Image classification

### Image Image segmentation

