---
title: "QuickDraw로 플레이 - 웹캠으로 인식시키기"

categories:
  - QuickDraw
tags: 
  - QuickDraw
  - Comment
  - Hanium
last_modified_at: 2020-08-30
---

드디어 웹캠이 아닌 그림판을 통해 퀵드로우 프로그램을 완성했다.

그림판을 리셋하는 버튼에서 자잘한 오류가 있어서 블로그를 자주 갱신하지 못했다.

이번 시간에는 [gautamkumarjaiswal](https://github.com/gautamkumarjaiswal/QucikDraw) 님의 코드를 내 나름대로 해석할 것 이다.

## QuickDraw 문서

   * Step 1. [QuickDraw로 플레이- 번역](https://jee00609.github.io/quickdraw/QuickDraw-Translation/)
   * Step 2. [QuickDraw로 플레이 - import 에러 해결](https://jee00609.github.io/quickdraw/QuickDraw-import-error/)
   * Step 3. [QuickDraw로 플레이 - 웹캠으로 인식시키기](https://jee00609.github.io/quickdraw/QuickDraw-code-comment/)

## 이 포스트를 보기전에 알아둘 것

   * 이 포스트 자체는 [gautamkumarjaiswal](https://github.com/gautamkumarjaiswal/QucikDraw)의 코드를 기반으로 합니다.
      * 2020년 7월 기준으로 import 에러등이 발생해서 약간의 코드 변경이 있습니다.
   * 코드의 원작성자가 아니기 때문에 틀린 설명이 존재할 수도 있습니다.
      * 이 포스팅에서 주로 다룰 파일은 runWebCam.py 입니다.
   * 프로젝트 실행 순서 순으로 파일의 코드를 설명할 것입니다.

## readDataset.py

readDataset 은 사용자가 원하는 오브젝트에 대한 npy 파일이 들어있는 data 폴더의 리스트를 읽는 기능을 합니다.

   ```ruby
# npy 파일이 있는 data 폴더의 위치를 알려주는 코드로 절대경로, 상대경로 모두 가능합니다.
# files = os.listdir("E:\QuickDraw_Project\data")
# files = os.listdir("data/")
   ```

   ```ruby
def load_data():
    count = 0
    for file in files:
        # 여기서도 자기 프로젝트에 맞춰서 경로를 설정합니다.
        # file = "E:\QuickDraw_Project\data\\" + file
        # file = "data/" + file
        print("file : "+file)
   ```

   ```ruby
def load_data():
    count = 0
    for file in files:
        # 여기서도 자기 프로젝트에 맞춰서 경로를 설정합니다.
        # file = "E:\QuickDraw_Project\data\\" + file
        # file = "data/" + file
   ```

파일이 제대로 실행되면 자기 data 파일 속의 파일들이 아래처럼 출력됩니다.

   ```ruby
file : data/full_numpy_bitmap_apple.npy
file : data/full_numpy_bitmap_bowtie.npy
file : data/full_numpy_bitmap_candle.npy
   ```

## trainModel.py

학습 및 모델 아키텍처와 모델 가중치를 h5 파일 형식으로 저장하는 파일 입니다.

   ```ruby
def keras_model(image_x, image_y):
    # npy 파일 즉 컴퓨터가 학습할 파일의 개수를 의미 
    num_of_classes = 3
   ```

## runWebCam.py

코드들에 주석을 설명하기 전에 먼저 프로그램이 어떻게 작동하는 가에 대해 먼저 이야기 하겠습니다.

이 프로그램은 말그대로 웹캠을 통해 사용자가 <span style="color:blue">파란색</span> 의 물체를 인식시켜서 선을 그려야 합니다.

웹캠에서 선이 사라지기 전까지는 계속해서 그림을 그리고 있다고 생각합니다.

따라서 파란색 물체로 그림을 다 그린 후 남은 손으로 파란색 물체를 가려줘야 합니다.

이후 학습 모델을 통해 사용자가 그린 그림을 판단해서 자신이 알고있는 물체 중 가장 비슷한 물체의 아이콘을 출력합니다.

<figure class="align-center">
  <img src="/assets/images/2020-08-30-mask-and-thresh.jpg">
  <figcaption>파란색만을 인식하고 있는 mask 와 그림을 파란색 선을 가렸을 경우 보이는 thresh 화면</figcaption>
</figure>

   ```ruby
def main():
    emojis = get_QD_emojis()
    # 내장 카메라 번호는 0번
    cap = cv2.VideoCapture(0)
    
    #사용자가 그림을 그릴 때 인식시킬 선의 색상을 정해준다. 
    #파란색 물체를 인식시켜 그림을 그릴것
    #HSV에서 BGR로 가정할 범위를 정의함
    Lower_blue = np.array([110, 50, 50])
    Upper_blue = np.array([130, 255, 255])
    pts = deque(maxlen=512)
    blackboard = np.zeros((480, 640, 3), dtype=np.uint8)
    digit = np.zeros((200, 200, 3), dtype=np.uint8)
    pred_class = 0

    while (cap.isOpened()):
        ret, img = cap.read()
        img = cv2.flip(img, 1)
        
        #BGR을 HSV 모드로 전환
        hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
        
        #픽셀 이미지는 주변 픽셀의 영향을 받게 되므로 가중치를 가진 행렬을 이용해서 이미지에 여러가지 효과를 줄 수 있는데 
        #이 행렬을 커널이라고 한다
        #3 *3 커널이라 함은 이미지를 변환하기 위한 9개의 행렬을 의미하게 된다
        kernel = np.ones((5, 5), np.uint8)
        
        #cv2.inRange(hsv, Lower_blue, Upper_blue) -> 색 추적
        #HSV 이미지에서 청색만 추출하기 위한 임계값
        #범위에 해당하는 부분만 오리지널 값으로 남기고, 이외는 0으로 채워서 반환
        #참고 : http://m.blog.naver.com/samsjang/220504633218
        mask = cv2.inRange(hsv, Lower_blue, Upper_blue)
        
        #cv2.erode(mask, kernel, iterations=2) -> 침식 연산
        #원래 있던 객체의 영역을 깍아 내는 연산
        #아주 작은 노이즈들을 제거할 때 사용
        #참고 : https://webnautes.tistory.com/1257
        mask = cv2.erode(mask, kernel, iterations=2)
        
        #cv2.dilate(mask, kernel, iterations=1) -> 팽창 연산
        #노이즈(작은 흰색 오브젝트)를 없애기 위해 사용한 Erosion에 의해서 작아졌던 오브젝트를 원래대로 돌림
        mask = cv2.dilate(mask, kernel, iterations=1)
        #mask = cv2.morphologyEx(mask, cv2.MORPH_OPEN, kernel)
        #Erosion 연산 다음에 Dilation 연산을 적용
        #이미지 상의 노이즈(작은 흰색 물체)를 제거하는데 사용
        #cv2.MORPH_OPEN -> 열림 연산
        mask = cv2.morphologyEx(mask, cv2.MORPH_OPEN, kernel)
        
        #cv2.MORPH_CLOSE -> 닫힘 연산
        #오브젝트 안의 노이즈들(검은색) 제거하는데 사용
        mask=cv2.morphologyEx(mask,cv2.MORPH_CLOSE,kernel)
        #mask = cv2.dilate(mask, kernel, iterations=1)
        # mask 를 보여주기 위한 윈도우 창입니다. 삭제해도 아무런 영향 없음.
        cv2.imshow("mask", mask)
        
        res = cv2.bitwise_and(img, img, mask=mask)
        cnts, heir = cv2.findContours(mask.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)[-2:]
        center = None

        if len(cnts) >= 1:
            print("파란색 점이 있는 상태, 즉 선이 존재")
            cnt = max(cnts, key=cv2.contourArea)
            if cv2.contourArea(cnt) > 200:
                ((x, y), radius) = cv2.minEnclosingCircle(cnt)
                cv2.circle(img, (int(x), int(y)), int(radius), (0, 255, 255), 2)
                cv2.circle(img, center, 5, (0, 0, 255), -1)
                M = cv2.moments(cnt)
                center = (int(M['m10'] / M['m00']), int(M['m01'] / M['m00']))
                pts.appendleft(center)
                for i in range(1, len(pts)):
                    if pts[i - 1] is None or pts[i] is None:
                        continue
                    cv2.line(blackboard, pts[i - 1], pts[i], (255, 255, 255), 7)
                    cv2.line(img, pts[i - 1], pts[i], (0, 0, 255), 2)
        elif len(cnts) == 0:
            print("파란색 점이 없는 상태, 즉 선이 존재치 않음")
            if len(pts) != []:
                #cv2.cvtColor(blackboard, cv2.COLOR_BGR2GRAY)
                #흑백 색상으로 바꿈
                blackboard_gray = cv2.cvtColor(blackboard, cv2.COLOR_BGR2GRAY)
                blur1 = cv2.medianBlur(blackboard_gray, 15)
                blur1 = cv2.GaussianBlur(blur1, (5, 5), 0)
                
                #https://hoony-gunputer.tistory.com/entry/opencv-python-%EC%9D%B4%EB%AF%B8%EC%A7%80-Thresholding
                #검은 화면에 사용자가 그린 흰색선이 존재하는 이미지가 뜰 것
                thresh1 = cv2.threshold(blur1, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)[1]
                #thresh 를 보여주기 위한 윈도우창입니다. 지워도 아무런 영향 없음
                cv2.imshow("thresh",thresh1)
                
                blackboard_cnts= cv2.findContours(thresh1.copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_NONE)[0]
                if len(blackboard_cnts) >= 1:
                    cnt = sorted(blackboard_cnts, key=cv2.contourArea, reverse=True)[0]
                    #cnt = max(blackboard_cnts, key=cv2.contourArea)
                    print(cv2.contourArea(cnt))
                    if cv2.contourArea(cnt) > 2000:
                        x, y, w, h = cv2.boundingRect(cnt)
                        digit = blackboard_gray[y:y + h, x:x + w]
                        pred_probab, pred_class = keras_predict(model, digit)
                        print("hey!",pred_class, pred_probab)

            pts = deque(maxlen=512)
            blackboard = np.zeros((480, 640, 3), dtype=np.uint8)
            img = overlay(img, emojis[pred_class], 400, 250, 100, 100)
        cv2.imshow("Frame", img)
        
        k = cv2.waitKey(10)
        if k == 27:
            cv2.destroyAllWindows()
            break
   ```

   ```ruby
def overlay(image, emoji, x, y, w, h):
    print("function overlay start")
    #실제 코드에선 여기에 emoji 를 resize 하지만 실행시키면 except 오류 발생합니다.
    #현재 처럼 try except 구문 안에서 resize 를 실행시키면 제대로 구동됩니다.
    #emoji = cv2.resize(emoji, (w, h))
    try:
        emoji = cv2.resize(emoji, (w, h))
        image[y:y + h, x:x + w] = blend_transparent(image[y:y + h, x:x + w], emoji)
    except :
        pass
    return image
   ```

## 비고

   * 사용자의 행동이 끝났다는 것을 인식시키기 위해선 파란색 물체가 사라지는 특정 행동을 취해야 합니다.
   * 주석이 달린 코드들의 전문을 보고 싶으시다면 아래 사이트에서 참조하시길 바랍니다.
      * readDataset.py
      * runWebCam.py
      * trainModel.py
   * 다음 포스팅에선 이 프로젝트를 참조해서 그림판을 통해 물체를 인식시키는 방법을 소개하겠습니다.

## 사이트

[이 포스팅의 기반이 되는 프로젝트 - gautamkumarjaiswal](https://github.com/gautamkumarjaiswal/QucikDraw)

[주석이 달린 프로젝트 코드들](https://github.com/jee00609/Hanium_2020/tree/master/quick%20draw)