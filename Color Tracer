import cv2
import numpy as np

cap = cv2.VideoCapture(0)# 0 is id for webcam
cap.set(3, 640) #pixels
cap.set(4, 480)
cap.set(10,150) # 10 is id for brightness 150 is value

myColors = [[88,164,122,97,255,255],# green, blue,red
           [97,177,53,115,255,255],
           [123,82,125,179,255,255]]
#[64,161,27,179,255,255] #purple
# HUE_min, SAT_min, VALUE_min, HUE_max, SAT_max, VALUE_max           
          
myColorValues = [[0,255,0],## BGR
                [255,0,0],
                [0,0,255]]

myPoints =  []  ## [x , y , colorId ]

def findColor(img,myColors,myColorValues):
    imgHSV = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
    count = 0
    newPoints=[]
    for color in myColors:
        lower = np.array(color[0:3])
        upper = np.array(color[3:6])
        mask = cv2.inRange(imgHSV,lower,upper)
        x,y=getContours(mask)
        cv2.circle(imgResult,(x,y),5,myColorValues[count],cv2.FILLED) #fills in color based on detected color
        if x!=0 and y!=0:
            newPoints.append([x,y,count])
        count +=1
        
    return newPoints

def getContours(img):
    contours,hierarchy = cv2.findContours(img,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_NONE)
    x,y,w,h = 0,0,0,0
    for cnt in contours:
        area = cv2.contourArea(cnt)
        if area>500:
            
            peri = cv2.arcLength(cnt,True)
            approx = cv2.approxPolyDP(cnt,0.02*peri,True)
            x, y, w, h = cv2.boundingRect(approx)
    return x+w//2,y

def draw(myPoints,myColorValues):
    for point in myPoints:
        cv2.circle(imgResult, (point[0], point[1]), 10, myColorValues[point[2]], cv2.FILLED)


while True:
    success, img = cap.read()
    imgResult = img.copy()
    newPoints = findColor(img, myColors,myColorValues)
    if len(newPoints)!=0:
        for newP in newPoints:
            myPoints.append(newP)
    if len(myPoints)!=0:
        draw(myPoints,myColorValues)


    cv2.imshow("Result", imgResult)
    if cv2.waitKey(1) & 0xFF == ord('q'): #q closes webcam
        break
