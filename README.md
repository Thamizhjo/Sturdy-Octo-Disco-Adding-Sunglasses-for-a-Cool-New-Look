# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## PROGRAM & OUTPUT:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

```
faceImage = cv2.imread('Karsa.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![SS1](https://github.com/user-attachments/assets/9881c2fa-6a5d-4fb8-833b-068586e13028)


```
faceImage.shape
```
![ss2](https://github.com/user-attachments/assets/4c3bca6d-953f-45bc-b97d-a183fad1ae36)


```
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
![ss3](https://github.com/user-attachments/assets/816a5b0d-c034-40c3-a145-2b33f313f61c)



```
glassPNG = cv2.resize(glassPNG,(590,250))
print("image Dimension ={}".format(glassPNG.shape))
```
![ss4](https://github.com/user-attachments/assets/46e5967c-701d-4e1e-a9d1-ca5648ae40f8)



```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

```
plt.figure(figsize=[35,35])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![ss5](https://github.com/user-attachments/assets/9a68f6ab-6493-4fc7-90d4-213a129da943)


```
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[750:1000, 710:1300]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

```

![ss6](https://github.com/user-attachments/assets/c05602c7-a57a-41b6-88be-d1ac8cc912be)


```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[750:1000, 710:1300]

maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

![ss7](https://github.com/user-attachments/assets/268d5690-c6b7-4ecf-bf4c-5ace0cfade46)

```
faceWithGlassesArithmetic[750:1000, 710:1300]=eyeRoiFinal

plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![ss8](https://github.com/user-attachments/assets/4601f8b1-cfc5-42aa-92d1-8a13e02953f7)

## Result:
Thus, the creative project designed to overlay sunglasses on individual passport size photo has been successfully executed.
