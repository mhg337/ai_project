# 관절길이 자동 조절 AI

- Pose Tracking

      import cv2
      import mediapipe as mp
      import time

      mpDraw = mp.solutions.drawing_utils
      mpPose = mp.solutions.pose
      pose = mpPose.Pose()

      cap = cv2.VideoCapture('pose_video.mp4')
      pTime = 0

      while True:
          success, img = cap.read()
          imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
          results = pose.process(imgRGB)

          if results.pose_landmarks:
              mpDraw.draw_landmarks(img, results.pose_lanmarks, mpPose.POSE_CONNECTIONS)
              for id, lm in enumerate(results.pose_landmarks.landmark):
                  h, w, c = img.shape
                  print(id, lm)
                  cx, cy = int(lm.x*w), int(lm.y*h)
                  cv2.circle(img, (cx,cy), 5, (255,0,0), cv2.FILLED)
  
      cTime = time.time()
      fps = 1/(cTime-pTime)

https://github.com/mhg337/ai_project/issues/1#issue-2008038926
      pTime = cTime

      cv2.putText(img, str(int(fps)), (70,50), cv2.FONT_HERSHEy_PLAIN, 3,
      (255,0,0), 3)
      cv2.imshow("Image", img)
      cv2.waitKey(1)
