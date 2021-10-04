---
tags : image-processing
---

[purpose of image processing:
* improve pictorial information for human
* redner it for autonomous machine

1. Sharpen : enhacing the edges
![](https://i.imgur.com/Uk82EJU.png)

2. Remove noise
 ![](https://i.imgur.com/H1Twr6K.png)\
 
 3. Remove motion blur
![](https://i.imgur.com/OZBpaCy.png)

4. edge enhancement
![](https://i.imgur.com/GFuhOs0.png)

5. Blurring to remove detail
![](https://i.imgur.com/eOGGyBj.png)

## Image Sampling & Acquisition
### Sample
**Nyquist criterion**
* require sampleing frequency be at least **twice the  highest frequency** in signal
* so we can construct a near continuous function

correct sampleing vs undersampled:
* we get a **aliasing** in undersampled picture
	* e.g.  [moiré pattern](https://en.wikipedia.org/wiki/Moir%C3%A9_pattern)
	* aliasing is an effect that causes different signals to become indistinguishable when sampled.
![](https://i.imgur.com/Ls6ZrtB.png)


### Image Acquisition
using CCD(Charge Coupled Device) camera

### Images vs Digital Images
* digital image : a array of sampled point from real image
	* these point are **pixels**
	* neighborhood : some pixels around the pixel
	* ![](https://i.imgur.com/Ct3cyJx.png)

each pixel have a color value from 0 ~ 255
* for example, gray scale: 
![](https://i.imgur.com/GuyjHrK.png)

applications:
* Medicine
* Ariculture
* Indusrty
* Law enforcement


---
Computer Vision vs Image Processing vs Image Analysis
![](https://i.imgur.com/bctvmyu.png)


Image Analysis
* Feature Extraction
* Pattern Classification

### Applications
* Image Resotration
	* Remove motion blue 
	* Remove *distortions*
	* Remove *periodic interference*
* Image Enhancement
	* Sharpen or deblur
	* Highlight edges
	* Improve image constrast
	* Remove noise
* Image Segmentation
	* finding the shape of objects in an image
* Image Compression

face detection:
![](https://i.imgur.com/eyUueud.png)

### Image type
![](https://i.imgur.com/GMKNqa8.png)

binary image:
![](https://i.imgur.com/FjyYySH.png)


Grayscale:
![](https://i.imgur.com/8W0963v.png)

True color/red-green-blue:
* we have 3 channels here
![](https://i.imgur.com/CFd22ja.png)

Indexed
* images's **indeices** correspoding to elements in **color map**
![](https://i.imgur.com/jCynIpg.png)](<# What is image processing

## Preview
### purpose of image processing
* improve pictorial information for human
* redner it for autonomous machine

### Computer Vision vs Image Processing
Computer Vision vs Image Processing vs Image Analysis
![](https://i.imgur.com/bctvmyu.png)


Image Analysis
* Feature Extraction
* Pattern Classification
* Image Resotration
* Image Enhancement
* Image Compression

### Image type
![](https://i.imgur.com/GMKNqa8.png)

binary image:
![](https://i.imgur.com/FjyYySH.png)


Grayscale:
![](https://i.imgur.com/8W0963v.png)

True color/red-green-blue:
* we have 3 channels here
![](https://i.imgur.com/CFd22ja.png)

Indexed
* images's **indeices** correspoding to elements in **color map**
![](https://i.imgur.com/jCynIpg.png)

### Applications
* Image Resotration
	* Remove motion blue 
	* Remove *distortions*
	* Remove *periodic interference*
* Image Enhancement
	* Sharpen or deblur
	* Highlight edges
	* Improve image constrast
	* Remove noise
* Image Segmentation
	* finding the shape of objects in an image
* Image Compression

## Usage
### Sharp the image 
* edge is an important part to a picture
* sharpen edge is good for us(or machine) to understand the imformation in  
* Sharpening edges is a vital component of printing
![](https://i.imgur.com/1NR8GzU.png)

### removing noise
* noise : random error in the image
![](https://i.imgur.com/eXJluef.png)
* remove motion blur
![](https://i.imgur.com/astbVpe.png)

### Obtaining the edges of an image
* Once we have the edges we can measure their spread and the area contained within them

* We can also use edge-detection algorithms as a first step in edge enhancement
* right picture call **edge image**
![](https://i.imgur.com/oAUfXAY.png)

### Enhance or blur specific detail
* for some purposes,we may not interested in all the detail in an image
* for example , we could measure the size and shape of the animal with picture rightside
 
![](https://i.imgur.com/ZhgNm21.png)


## Image Sampling & Acquisition
### Sample
**Nyquist criterion**
* require sampleing frequency be at least **twice the  highest frequency** in signal
* so we can construct a near continuous function

correct sampleing vs undersampled:
* we get a **aliasing** in undersampled picture
	* e.g.  [moiré pattern](https://en.wikipedia.org/wiki/Moir%C3%A9_pattern)
	* aliasing is an effect that causes different signals to become indistinguishable when sampled.
![](https://i.imgur.com/Ls6ZrtB.png)


### Image Acquisition
we can use CCD(Charge Coupled Device) camera to get digital image
![](https://i.imgur.com/YKKddqY.png)



### Images vs Digital Images
* digital image : a array of sampled point from real image
	* these point are **pixels**
	* neighborhood : some pixels around the pixel
	* ![](https://i.imgur.com/Ct3cyJx.png)

each pixel have a color value from 0 ~ 255
* for example, gray scale: 
![](https://i.imgur.com/GuyjHrK.png)

applications:
* Medicine
* Ariculture
* Indusrty
* Law enforcement


## Image File Size
**binary**
size: 512x512 = 512x512x1 (bit) = 262144 bits = 32768 bytes

**grayscale image**
size: 512x512 = 512x512x1 (bytes) = 262144 bytes

**Color image**
size: 512x512 = 512x512x3 (bytes) = 786432 bytes

## Image Perception
- Rods(桿狀體)
    - 夜間視力
    - 人體的感光
    - 分布在 Retina(視網膜)
- Cone(錐狀體)
    - 人體的感色
    - 集中在人體的眼睛中間。
![](https://i.imgur.com/7AgagTS.png)>)