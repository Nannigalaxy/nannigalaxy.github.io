---
layout: post
title:  "Image Center Crop and Scaling using OpenCV in Python"
date:   2022-04-03
categories: Python OpenCV
---
## [TLDR;](/center-crop-scale#h-full-code)
## a. Center Crop  
X-Y Coordinate SystemCenter crop is cropping an image from center which gives an equal padding on both sides vertically and horizontally. It is useful when dealing with many images with different resolutions, say for the computer vision or machine learning applications.  
I was working on a webcam and pi camera that had different resolutions. So I created a function to crop from center to maximum dimension without exceeding the available dimension of the original image.  


Let's create a function center_crop() with parameters as image and crop dimensions as a tuple (width, height).

```Python
def center_crop(img, dim):
  """Returns center cropped image

  Args:Image Scaling
  img: image to be center cropped
  dim: dimensions (width, height) to be cropped from center
  """
  width, height = img.shape[1], img.shape[0]
  # crop width and height for max available dimension
  crop_width = dim[0] if dim[0]<img.shape[1] else img.shape[1]
  crop_height = dim[1] if dim[1]<img.shape[0] else img.shape[0] 
```

The first line gets the width and height of the original image. Crop dimensions passed in arguments may exceed the original dimension, this results in improper image cropping. The last two lines choose the maximum dimension without exceeding the original image dimension.

```Python
  mid_x, mid_y = int(width/2), int(height/2)
  cw2, ch2 = int(crop_width/2), int(crop_height/2) 
  crop_img = img[mid_y-ch2:mid_y+ch2, mid_x-cw2:mid_x+cw2]
  return crop_img
```
The first two lines will get coordinates required for slicing numpy array i.e. image array.  
RGB image read in OpenCV will be in shape: (height, width, channel). Example: (920, 1280, 3).  
Thrid line slices from the original image array that becomes cropped image array. Finally returns the center cropped image.

---

## b. Image Scaling
Image Scaling is resizing by keeping the image ratio intact i.e. downscaling and upscaling.

Let's define function scale_image() with parameters image and scaling factor.  
```Python
def scale_image(img, factor=1):
  """Returns resize image by scale factor.
  This helps to retain resolution ratio while resizing.
  Args:
  img: image to be scaled
  factor: scale factor to resize
  """
return cv2.resize(img,
                (int(img.shape[1]*factor),
                int(img.shape[0]*factor)))   
```
We'll use the resize function to scale an image by multiplying the scale factor with the original image dimension and return the scaled image.  
Downscaling can be done by passing the factor argument between 0 to 1. And above 1 for Upscaling.

---

## Full Code

```Python
# Center Crop and Image Scaling functions in OpenCV
# Date: 11/10/2020
# Written by Nandan M

import cv2

def center_crop(img, dim):
	"""Returns center cropped image
	Args:
	img: image to be center cropped
	dim: dimensions (width, height) to be cropped
	"""
	width, height = img.shape[1], img.shape[0]

	# process crop width and height for max available dimension
	crop_width = dim[0] if dim[0]<img.shape[1] else img.shape[1]
	crop_height = dim[1] if dim[1]<img.shape[0] else img.shape[0] 
	mid_x, mid_y = int(width/2), int(height/2)
	cw2, ch2 = int(crop_width/2), int(crop_height/2) 
	crop_img = img[mid_y-ch2:mid_y+ch2, mid_x-cw2:mid_x+cw2]
	return crop_img

def scale_image(img, factor=1):
	"""Returns resize image by scale factor.
	This helps to retain resolution ratio while resizing.
	Args:
	img: image to be scaled
	factor: scale factor to resize
	"""
	return cv2.resize(img,(int(img.shape[1]*factor), int(img.shape[0]*factor)))


if __name__ == "__main__":
	image = cv2.imread('Kuvempu.jpg')

	ccrop_img = center_crop(image, (500,400))
	scale_img = scale_image(image, factor=1.5)

	cv2.imwrite("Kuvempu_center_crop.jpg", ccrop_img)
	cv2.imwrite("Kuvempu_scaled.jpg", scale_img)
```