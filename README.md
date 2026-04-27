# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM
To write a Python program using OpenCV to perform the following tasks:

1) Read and display an image  
2) Adjust the brightness of the image  
3) Modify the contrast of the image  
4) Create a new image using bitwise operations  

---

## SOFTWARE REQUIRED
- Anaconda (Python 3.7)  
- Jupyter Notebook  

---

## ALGORITHM

### Step 1:
Read an image from the local folder and display it.

### Step 2:
Create a matrix of ones (float64 type) to change the brightness.

### Step 3:
Increase and decrease the brightness by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Adjust the contrast of the image using scaling factors of 1.1 and 1.2.  
Display the original image along with the contrast-adjusted images.

### Step 5:
Split the image (boy.jpg) into Blue, Green, and Red channels and display each one.

---
## Environment Setup
### Create Conda Environment
```
Create a new environment:
 conda create --name opencv-env python=3.11

Activate the environment:
 conda activate opencv-env

Verify the Python version in the environment:
python --version

Check and Upgrade pip
Check pip version:
pip --version

Upgrade pip:
pip install --upgrade pip

Install OpenCV and all the required libraries:
pip install opencv-contrib-python streamlit moviepy jupyter matplotlib ipykernel 
or 
Create a requirements.txt file:

opencv-contrib-python==4.10.0.84
streamlit==1.38.0 
moviepy==1.0.3 
jupyter==1.1.1 
matplotlib==3.9.2 
pyautogui
mediapipe
mime
pip install -r requirements.txt
```
---

## PROGRAM DEVELOPED BY

### Name: *UDHAYA PRAKASH V*
### Register Number: *212224240177*
 
---

### Import OpenCV, NumPy, and Matplotlib libraries
```PY
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
image = cv2.imread('Eagle_in_Flight.jpg', cv2.IMREAD_GRAYSCALE)
```

### 2. Print the image width, height & Channel.
```python
height, width = image.shape
channels = 1
print("Width:", width)
print("Height:", height)
print("Channels:", channels)
```

### 3. Display the image using matplotlib imshow().
```python
plt.imshow(image, cmap='gray')
plt.title('Grayscale Image')
plt.axis('off')   # Hide axes
plt.show()
```

### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite('Eagle.png', image)
```

### 5. Read the saved image above as a color image using cv2.cvtColor().
```pythonimg_color = cv2.imread('Eagle_in_Flight.jpg')
img_rgb = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)
```

### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img_rgb)
plt.title("Color Image (RGB)")
plt.axis('off')
plt.show()
height, width, channels = img_rgb.shape
print("Width:", width)
print("Height:", height)
print("Channels:", channels)
```

### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
cropped = img_rgb[20:420, 210:540]
plt.imshow(cropped)
plt.title("Cropped Eagle")
plt.axis('off')
plt.show()
```

### 8. Resize the image up by a factor of 2x.
```python
resized = cv2.resize(cropped, None, fx=2, fy=2)
plt.imshow(resized)
plt.title("Resized 2x")
plt.axis('off')
plt.show()
```

### 9. Flip the cropped/resized image horizontally.
```python
flipped = cv2.flip(resized, 1)
plt.imshow(flipped)
plt.title("Flipped Eagle")
plt.axis('off')
plt.show()
```

### 10. Read in the image ('Apollo-11-launch.jpg').
```python
apollo = cv2.imread('Apollo-11-launch.jpg')
```

### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font = cv2.FONT_HERSHEY_PLAIN
(h, w, _) = apollo.shape
(text_w, text_h), _ = cv2.getTextSize(text, font, 2, 2)
x = (w - text_w) // 2
y = h - 20
cv2.putText(apollo, text, (x, y), font, 2, (255, 255, 255), 2, cv2.LINE_AA)
```

### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
x1, y1 = 300, 100
x2, y2 = 900, 1800
cv2.rectangle(apollo, (x1, y1), (x2, y2), (255, 0, 255), 3)
apollo_rgb = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)
```

### 13. Display the final annotated image.
```pythonplt.imshow(apollo_rgb)
plt.title("Apollo 11 with Rectangle")
plt.axis('off')
plt.show()
```

### 14. Read the image ('Boy.jpg').
```python
img = cv2.imread('boy.jpg')
```

### 15. Adjust the brightness of the image.
```python
matrix = np.ones(img.shape, dtype='uint8') * 50
```

### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(20,10))
plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original"); plt.axis('off')

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker"); plt.axis('off')

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter"); plt.axis('off')
plt.show()

```

### 18. Modify the image contrast.
```python
img_higher1 = cv2.convertScaleAbs(img, alpha=1.1, beta=0)
img_higher2 = cv2.convertScaleAbs(img, alpha=1.2, beta=0)
```

### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original"); plt.axis('off')

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.1"); plt.axis('off')

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.2"); plt.axis('off')
plt.show()
```

### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img)

plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis('off')

plt.subplot(1,3,2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis('off')

plt.subplot(1,3,3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis('off')

plt.show()
```

### 21. Merged the R, G, B , displays along with the original image
```python
merged = cv2.merge([b, g, r])
    
plt.imshow(cv2.cvtColor(merged, cv2.COLOR_BGR2RGB))
plt.title("Merged BGR")
plt.axis('off')
plt.show()
```

### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv)

plt.figure(figsize=(10,5))
plt.subplot(1,3,1); plt.imshow(h, cmap='gray'); plt.title("Hue"); plt.axis('off')
plt.subplot(1,3,2); plt.imshow(s, cmap='gray'); plt.title("Saturation"); plt.axis('off')
plt.subplot(1,3,3); plt.imshow(v, cmap='gray'); plt.title("Value"); plt.axis('off')
plt.show()
```
### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([h, s, v])
merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV")
plt.axis('off')
plt.show()
```
---
## Output:
- **i)** The image was successfully read and displayed  
- **ii)** The brightness of the image was adjusted  
- **iii)** The contrast of the image was modified  
- **iv)** A new image was created using bitwise operations  

---

## Result:
Thus, the image processing tasks such as reading, displaying, brightness adjustment, contrast modification, and bitwise operations were successfully completed using Python and OpenCV.
