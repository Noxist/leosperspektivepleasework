+++
title = "AI Lächelerkennung"
date = "2023-07-03"
draft = false
pinned = false
+++
```
<iframe width="110" height="200" src="https://www.myinstants.com/instant/scout-alarm-11373/embed/" frameborder="0" scrolling="no"></iframe>
```

Ich habe eine AI entwickelt in Google Colab programmiert, welche in einem Bild lächelnde Personen erkennt.

Dieser Code kann in Google Colab eingefügt werden und danach ein Bild URL eingefügt werden.

```
!wget https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade_frontalface_default.xml
!wget https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade_smile.xml
!pip install opencv-python

import cv2 
import urllib.request
import numpy as np

image_url = input('Enter an image URL: ')

def detect_smiles(image_url):
    """Detect smiles in an image."""
    try:
        # Read the image from the URL
        with urllib.request.urlopen(image_url) as url:
            s = url.read()
        arr = np.asarray(bytearray(s), dtype=np.uint8)
        img = cv2.imdecode(arr, -1)
        
        # Convert the image to grayscale
        gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        
        # Detect faces 
        face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
        faces = face_cascade.detectMultiScale(gray, scaleFactor=1.2, minNeighbors=6)
        
        # Align face images 
        aligned_faces = []
        for (x, y, w, h) in faces:
            face_roi = gray[y:y+h, x:x+w]
            aligned_faces.append(face_roi)
        
        # Detect smiles 
        smile_cascade = cv2.CascadeClassifier('haarcascade_smile.xml')
        
        for face in aligned_faces:
            smiles = smile_cascade.detectMultiScale(face, scaleFactor=1.7, minNeighbors=11) 
            
            if len(smiles) > 0:
                return True 
            
        return False
            
    except Exception as e:
        print(f"Error: {e}")
        return False

smiles_detected = detect_smiles(image_url)

if smiles_detected:
  print('Smiles detected! :)')
else: 
  print('No smiles detected. :(')
```