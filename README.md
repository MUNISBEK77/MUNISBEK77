import cv2

# Load the cascade /Kaskadlarni chaqirib olish
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

# To capture video from webcam. /kamradan video olish
cap = cv2.VideoCapture(0)
# To use a video file as input. /Video faylni yuklash
#cap = cv2.VideoCapture('filename.mp4')

while True:
    # Read the frame. /ramkaga olish
    _, img = cap.read()
    # Convert to grayscale. /rangni tanlash
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    # Detect the faces./ yuzni aniqlash
    faces = face_cascade.detectMultiScale(gray, 1.1, 4)
    # Draw a circle around each face with a green color. /Har bir yuzning atrofida yashil rangda yumaloq shakl chizing
    for (x, y, w, h) in faces:
        # Coordinates for the center of the circle
        center = (x + w//2, y + h//2)
        # Radius of the circle (half of the width or height)
        radius = int((w + h) / 4)
        # Draw the circle
        cv2.circle(img, center, radius, (0, 255, 0), 2)
    # Display
    cv2.imshow('Rasm', img)
    # Stop if escape key is pressed. /Escape tugmasi bosilsa, to'xtating
    k = cv2.waitKey(30) & 0xff
    if k == 27:
        break
# Release the VideoCapture object. /Jarayon tugallanganidan so'ng resurslarni tozalash
cap.release()

