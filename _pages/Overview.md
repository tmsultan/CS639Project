---
layout: single
title: Overview
permalink: /Overview/
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

# Problem Statement
<!-- In this project, we seek to fuse images from two different sensors to create a hybrid image which encodes a large range of scene brightnesses (high dynamic range) and contains high spatial resolution. We work with the following sensors:

### (i). CMOS Sensor 

Complementary metal–oxide–semiconductor (CMOS) sensors are the current industrial standard, and are used in most modern smart phones. These sensors produce images with high spatial resolution, but the images produced are 8-bit since the sensor . 


### (ii). SPAD Sensor

Single-Photon-Avalanche Diode (SPAD)  32-bit image from a Suign -->


High Dynamic Range (HDR) imaging is widely used to extend the range of intensity values of an image. Single-photon avalanche diodes (SPADs), when ran passively, are able to capture 2D intensity images with extremely high dynamic range, ideally spanning a range of 106:1 [1]. We propose a single-photon guided high dynamic range imaging pipeline that augments the dynamic range of a conventional sensor. We intend to show that an intensity map guided HDR neural network [2] can take a low-spatial-resolution, high-dynamic-range SPAD image and a high-spatial-resolution, limited-dynamic-range image from a conventional sensor, and construct a high-quality HDR image as output.   

# Solution Approach 

## Simulation Pipeline

We simulate a high-resolution CMOS image and an HDR SPAD image from a high-resolution, HDR ground truth image (figure 1). We simulated approximately 50 images, and used them for our downstream methods described below. 


<figure>
  <img src="/CS639Project/assets/images_project/Selection_752.png" alt="this is a placeholder image">
  <figcaption>Fig 1. Summary of the Simulation Pipeline.</figcaption>
</figure>

## Upsampling SPAD Image and Weighted Fusion
We upsample the SPAD image using bilinear interpolation. We fuse the CMOS and upsampled SPAD image using the following weighting scheme:


$$I_{fusion} = W (I_{CMOS}, I^{SR }_{SPAD} )=  \frac{w_{CMOS}I_{CMOS} + w_{SPAD}I_{SPAD}}{w_{CMOS} w_{SPAD}}$$

Where the $$w_{CMOS} \in [0, 1], \qquad w_{SPAD} = 1 - w_{CMOS}$$. 

The SR superscript denotes that the SPAD image has been upsampled. Then we calculate the weight for each pixel value as:

$$w=\frac{0.5 - \max{(|I - 0.5|, \tau - 0.5)}}{ 1 -\tau}$$

Where $$ \tau \in [0, 1] $$ is a threshold set manually. This weighting scheme has been adapted from [4].

## Comparison to Other Methods

We compare these images with other HDR images produced from the following methods: 

1. Exposure Bracketing: This method merges CMOS images with varying exposures to get a HDR image. 
2. ExpandNet - A Deep Convolutional Nueral Network which has been trained to produce HDR outputs from single image LDR inputs.


## Quantitative Evaluation
For this project, we used the SSIM metric to generate a quantitative assessment of the metrics. This is a well known metric which assesses perceptual image quality using known properties of human visual system based on the structural similarity of a reference image (ground truth) and it's distorted (measured) counterpart. (Add formula if you have time on the end)[5] 


# Results
First we demonstrate some qualitative results.  The first gif demonstrates the result of our fusion method, and highlights the saturated region where we use information from SPAD data to augment the original CMOS image. We can see that the image does not saturate even in extremely bright regions. 


<figure>
  <img src="/CS639Project/assets/images_project/FusionHDR.gif" alt="this is a placeholder image">
  <figcaption>Fused Image has a High Dynamic Range.</figcaption>
</figure>


Next, we compare our method to the original CMOS image. As expected, CMOS saturates near the sunlit window while the fused image recovers details in the same area. 

<figure>
  <img src="/CS639Project/assets/images_project/FusionVsCMOS.gif" alt="this is a placeholder image">
  <figcaption>Fused Image vs CMOS Output.</figcaption>
</figure>


Next we compare our method to Exposure Bracketing (EB) and ExpandNet (EN). As expected,ExpandNet performs the worse, since it relies on a single image and pretrained models. It seems that Exposure bracketing performs better than our methods since the image produced using EB is slower to saturate. 



<figure>
  <img src="/CS639Project/assets/images_project/FusionVsEBVsEN.gif" alt="this is a placeholder image">
  <figcaption>This is a figure caption.</figcaption>
</figure>

## EDSR SuperResolution Network

We attempted to use a deep learning based super-resolution method called EDSR [6] to upsample the low-res SPAD images. Since the network was designed to do super-resolution on 8-bit LDR images, we modified the network to read, write, and upsample 32-bit HDR SPAD images. 



<figure>
  <img src="/CS639Project/assets/images_project/EDSROutput.gif" alt="this is a placeholder image">
  <figcaption>Comparison of Interpolation Methods.</figcaption>
</figure>

As seen in the image, EDSR seems to create aritifacts near saturated regions, while qualitatively improving upon image quality in other regions. We believe that these artifacts occur because EDSR is pre-trained on LDR images and does not know how to interpolate correctly for extremely high pixel values. Since these are the very regions where the upsampled SPAD image would be most useful, we decided against fusing this with our CMOS image. 


# Limitations



# Lessons Learned, Future Work


# References
[1] 


[5] Zhou, W., A. C. Bovik, H. R. Sheikh, and E. P. Simoncelli. "Image Qualifty Assessment: From Error Visibility to Structural Similarity." IEEE Transactions on Image Processing. Vol. 13, Issue 4, April 2004, pp. 600–612.