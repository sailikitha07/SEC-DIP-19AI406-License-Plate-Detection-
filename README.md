# SEC-DIP-19AI406-License-Plate-Detection-
## Aim
To implement a License Plate Detection system using OpenCV and Haar Cascade Classifier, draw bounding boxes, crop the detected region, and blur the license plate to improve privacy. The detection accuracy is improved by tuning Haar Cascade parameters.

## Software Used
Python 3.7 or above  
OpenCV (opencv-python)  
NumPy  
Matplotlib  
Jupyter Notebook (Anaconda)  
Haar Cascade File: haarcascade_russian_plate_number.xml

## Algorithm
Import necessary libraries such as OpenCV and Matplotlib  
Read the input vehicle image  
Convert the original image to grayscale for faster computation  
Load the Haar Cascade classifier for license plate detection  
Detect license plate using detectMultiScale function  
Draw rectangle around detected area  
Crop the detected region using numpy slicing with (x, y, w, h) values  
Apply median blurring on the cropped region  
Replace the original region with blurred version  
Display final result using Matplotlib

## Program & Output :
```
import cv2
import matplotlib.pyplot as plt

# Read the image
img = cv2.imread("car.webp")

# Load license plate Haar Cascade
plate_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_russian_plate_number.xml"
)

# Convert image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Detect license plate
plates = plate_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=4
)

# Blur the detected license plate
for (x, y, w, h) in plates:

    # Extract license plate
    plate = img[y:y+h, x:x+w]

    # Apply blur
    blurred_plate = cv2.GaussianBlur(
        plate,
        (25, 25),
        0
    )

    # Replace original plate with blurred plate
    img[y:y+h, x:x+w] = blurred_plate

# Convert BGR to RGB
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Display
plt.figure(figsize=(10, 6))
plt.imshow(img_rgb)
plt.title("License Plate Detected and Blurred")
plt.axis("off")
plt.show()
```
<img width="642" height="507" alt="image" src="https://github.com/user-attachments/assets/3fe32551-3d5b-496e-8f91-6213c026a2c4" />

 
## Result
The License Plate Detection system was successfully implemented using OpenCV and Haar Cascade. The detected license plate region was blurred using median filtering. The modified values improved overall detection performance and output quality.
