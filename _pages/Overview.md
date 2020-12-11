---
layout: single
title: Overview
permalink: /Overview/
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

# Problem Statement
<!-- In this project, we seek to fuse images from two different sensors to create a hybrid image which encodes a large range of scene brightnesses (high dynamic range) and cotains high spatial resolution. We work with the following sensors:

### (i). CMOS Sensor 

Complementary metal–oxide–semiconductor (CMOS) sensors are the current industrial standard, and are used in most modern smart phones. These sensors produce images with high spatial resolution, but the images produced are 8-bit since the sensor . 


### (ii). SPAD Sensor

Single-Photon-Avalanche Diode (SPAD)  32-bit image from a Suign

 -->

High Dynamic Range (HDR) imaging is widely used to extend the range of intensity values of an image. Single-photon avalanche diodes (SPADs), when ran passively, are able to capture 2D intensity images with extremely high dynamic range, ideally spanning a range of 106:1 [1]. We propose a single-photon guided high dynamic range imaging pipeline that augments the dynamic range of a conventional sensor. We intend to show that an intensity map guided HDR neural network [2] can take a low-spatial-resolution, high-dynamic-range SPAD image and a high-spatial-resolution, limited-dynamic-range image from a conventional sensor, and construct a high-quality HDR image as output.   

# Solution Approach 
We simulate an LDR CMOS image and HDR SPAD image from a ground truth image. We upsample the SPAD image using different interpolation methods, and then fuse the two images using the following weighting scheme:


<figure>
  <img src="/CS639Project/assets/images/unsplash-image-10.jpg" alt="this is a placeholder image">
  <figcaption>This is a figure caption.</figcaption>
</figure>

Add formula later
$$I_{fusion} = W (I_{CMOS}, I^{SR }_{SPAD} )=$$

We then compare these images with other HDR images produced from the following networks: 

1. Exposure Bracketing
2. ExpandNet
3. EDSR Network


# Results
Here are some results: 




# Lessons Learned, Future Work