# OpenCV

Checked: No
Property: In-Progress

ref : [tacademy.skplanet.com](http://tacademy.skplanet.com) → OpenCV

- 1. OpenCV 개요 - Intel지원
    - 컴퓨터비전
        - 색상 or 모양으로 분류, 기준은?
        - 이미지프로세싱 유사의미
        - 수학,신호처리(2차원신호처리)
        - 이미지전처리 : blur, sharpening
        - 검출 : Object Detection
        - 분할 : Segmentation
        - 인식 : Recognizion ex.사람구분,OCR
        - ex. Amazon Go, 자율주행차
    - 영상데이터
        - 영상 : 가로x세로 ↔ 행렬 : 세로(행)x가로(열)
        - 그레이스케일 영상(Grayscale)
            - 0:가장어두움(검정), 255:가장밝은밝기(흰색)
            - 색상정보가 밝기정보만으로 구성
            - 밝기정보를 256단계로 표현
            - C/C++ - unsigned char (1byte)
            - python - numpy.uint8
        - 트루컬러영상(True Color)
            - 컬러진처럼 색상정보를 가지고 있어 다양한 색상을 표현하는 영상
            - Red,Green,Blue 색성분을 256단계로 표현 1600만가지로 표현
        - 픽셀(pixel) : 영상의 기본단위, 화소
        - 색상표현
            - 픽셀당 RGB 3개 element로 표현가능
            - 색상별(R,G,B) 3차원 행렬 표현
        - 영상데이터 크기
            - 흑백이미지(512x512) : 512x512=262144Byte
            - 컬러이미지(1920x1080) : 1920x1080x3=6220800 Bytes=6MB 1분 60프레임 → 360MB 처리필요
        - 영상파일 형식

            영상처리에 유리한 형식 : PNG,TIF(무손실압축) > BMP(무압축) > JPG(손실압축)

            - BMP
                - MSS, 압축하지않음,용량이큼
                - 파일구조 단순
            - JPG
                - 주로 사진 컬러영상 저장
                - 손실압축(Lossy Compression)
                - 압축률이 좋아서 파일 용량 크게 감소 - 디지털카메라
            - GIF
                - 256 색상이하 영상
                - 무손실압축(lossless compression)
                - 움직이는 GIF 지원
            - PNG
                - Portable Network Graphics
                - 무손실압축(트루컬러도 무손실압축)
                - 알파채널(투명도) 지원

    - 환경설정

        ```jsx
        # 패키지
        $ apt-get update
        $ apt-get install python3 python3-pip
        $ pip3 install opencv-python==4.1.0.25
        $ apt-get install libsm6 libxrender1 libxext6

        # unicodeencodeError
        $ export LANG=C.UTF-8
        # IDE
        visual studio code, pycharm,jupyter notebook
        ```

    - Matplotlib ↔ OpenCV
        - Matplotlib : RGB
        - OpenCV : BGR

        ```jsx
        imgBGR = cv2.imread('image.jpg')
        imgRGB = cv2.cvtColot(imgBGR,cv2.COLOR_BGR2RGB)

        cv2.imwrite(filename,img,params=None) -> retval // 정상시 True,실패시 False
        ```

        ref : http:docs.opencv.org/master

    - virtualenv

        ```jsx
        # virtualenv 설치
          $ pip install virtualenv
          $ pip3 install virtualenv

        # 가상환경 생성
          $ virtualenv [가상환경명] -p python=

        # 가상환경 실행
          $ source [env 경로]/activate
          $ pip list

        # 설치경로 확인
          $ which python 
        ```

- 2. OpenCV 프로그래밍 기초
    - IDE 가상환경 연결&설정
    - imshow
- 3. 명함 검출 및 인식 1 - 이진화
    - 영상의 이진화(Binarization) :  픽셀값을 0 또는 1(255)로 변환
    - 히스토그램, 임계값
    - cvtColor BGR 각 8bit X 3=3byte →  565=2byte
    - 이진화, 임계값함수 : threshold

        ```jsx
        # 흑백 이진화
        cv2.THRESH_BINARY # 흑,백
        cv2.THRESH_BINARY_INV # 흑,백+반전
        # 밝기 유지
        cv2.THRESH_TRUNC
        cv2.THRESH_TOZERO

        # 이미지마다 임계값이 다름 -> 임계값 자동추출 otsu 법 사용(분산의 합이 최소)
        # 자동 임계치 설정
        cv2.THRESH_OTSU
        cv2.THRESH_TRIANGLE

        src = cv2.imread('/code/opencv/lec3/namecard1.jpg')
        src = cv2.resize(src,(640,480))
        src = cv2.resize(src,(0,0),fx=0.5,fy=0.5)
        src_gray = cv2.cvtColor(src, cv2.COLOR_BGR2GRAY)
        _, src_bin = cv2.threshold(src_gray,130,255,cv2.THRESH_BINARY)
        th , src_bin = cv2.threshold(src_gray,0,255,cv2.THRESH_BINARY | cv2.THRESH_OTSU)
        print(th)

        ```

- 4. 명함 검출 및 인식 2 - 레이블링,외곽선검출,투시변환
    - 객체 단위 분석
        - 흰색으로 표현된 객체를 분할하여 특징분석
        - 객체 위치 및 크기정보,ROI 추출
    - 레이블링(Connected Component labeling)
        - cv2.connectedComponent(), cv2.connectedComponentWithStats()
        - 서로연결된 객체 픽셀에 고유한 번호 지정
        - 객체 바운딩 박스, 중심좌표 함께 반환
    - 외곽선 검출(Contour Tracing)
        - cv2.findContours()
        - 객체 외곽선 좌표 모두 검출
        - 파라미터
            - image : 입력영상, non-zero 픽셀  객체로 간주
            - mode : 외곽선 검출모드
                - RETR_EXTERNAL : 가장바깥 외곽선만검출
                - RETR_LIST : 계층관계없이 모든 외곽선 검출
                - RETR_CCOMP : 2레벨 계층구조로 외곽선 검출 상위(흰색 객체 외곽선), 하위(검정색 구멍 외곽
                - RETR_TREE : 계층적 트리구조로 모든 외곽선 검출
            - method : 외곽선 근사화 방법
                - CHAIN_APPROX_NONE : 근사화x (범용적)
                - CHAIN_APPROX_SIMPLE : 수직,수평,대각선에 대해 끝점 압축
            - contours : 검출된 외곽선 좌표
            - hierarchy : 외곽선 계층정보
    - 외곽선 근사화
        - cv2.approxPolyDP(curve,epsilon,closed,approxCurve=None)
            - curve : 입력곡선 좌표 numpy.ndarray.shape=(K,1,2)
            - epsilon : 근사화 정밀도조절, 입력곡선과 근사화 곡선간 최대거리
            - closed : True=폐곡선
            - approxCurve : 근사화된 곡선좌표
    - 라인그리기 : cv2.polylines(src,pts,True,(0,0,255)) # 외곽선 그리기
    - 기하학적 변환
        - affine : translation,shear,scaling,rotate,combination
        - perspective :
            - 투시변환 : cv2.getPerspectiveTransform(src,dst,solveMethod=None) → retval
                - src : 4개 원본좌표점 numpy.ndarray.shape=(4.,2)
                - dst : 4개 결과 좌표점 numpy.ndarray.shape=(4,2)
                - 반환값 : 3x3 크기 투시변환 행렬

    ```jsx
    # 외곽선 검출

    import sys
    import cv2
    import numpy as np

    # 영상 불러오기
    img = cv2.imread('../image2.jpg')

    if img is None:
        print('Image load failed!')
        sys.exit()

    src = cv2.resize(img,(640,480)) # 픽셀숫자
    # src = cv2.resize(src,(0,0),fx=0.5,fy=0.5) # 배율
    src_gray = cv2.cvtColor(src, cv2.COLOR_BGR2GRAY)

    # _, src_bin = cv2.threshold(src_gray, 130, 255, cv2.THRESH_BINARY)
    th , src_bin = cv2.threshold(src_gray,0,255,cv2.THRESH_BINARY | cv2.THRESH_OTSU)
    print(th)

    contours, _ = cv2.findContours(src_bin,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROXP_NONE)
    print(len(contours))

    for pts in contours:
    	if cv2.contourArea(pts) < 1000: 
    		continue
    	
    	approx = cv2.approxPolyDP(pts,cv2.arcLength(pts,True)*0.02,True)
    	if len(approx) != 4:
    		continue
    	w,h=900,500
    	srcQuad = np.array([[approx[0,1,:],[approx[1,1,:],[approx[2,1,:],[approx[3,1,:]]
    	dstQuad = np.array([[0,h],[w,h],[w,0],[0,0]]).astype(np.float32)

    	pers = cv2.getPerspectiveTransForm(srcQuad,dstQuad)
    	dst = cv2.warpPerspective(src,pers)
    	cv2.polylines(src,pts,True,(0,0,255)) # 외곽선 그리기

    # 영상 화면 출력
    # cv2.namedWindow('image')
    cv2.imshow('original', src)
    cv2.imshow('gray_scale', src_gray)
    cv2.imshow('Binary',src_bin)
    cv2.waitKey()

    # 창 닫기
    cv2.destroyAllWindows()
    ```

- 5. 명함 검출 및 인식 3 - Tesseract를 이용한 문자인식(구글에서 관리)
    - https://github.com/tesseract-ocr/tesseract
    - [https://github.com/UB-Mannheim/tesseract/wiki](https://github.com/UB-Mannheim/tesseract/wiki) : Windows Pre-built 설치파일
    - pytesseract : https://github.com/madmaze/pytesseract
        - OpenCV,Numpy와 사용 시 ndarray 지원
        - Tesseract는 RGB컬러포맷
        - pip install pytesseract

        ```jsx
        # OpenCV 컬러변환 사용
        img = cv2.imread('digit.png')
        img_rgb = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
        print(pytesseract.image_to_string(img_rgb))
        ```

- 6. OpenCV 얼굴검출
    - Harr cascade 얼굴검출 : 얼굴에 있는 명암을 활용해 찾아냄
    - DNN 알고리즘
    - 활용 : classification(분류), segmentation(픽셀단위검출), super-resolution/`image-inpainting(가려진부분채우기)
    - 신경망 개요
        - 퍼셉트론 (Perceptron) + 다층퍼셉트론
            - 입력 → *가중치들의 합 → 전달함수 → 출력
        - 컨볼루션 신경망(CNN)
            - 컨볼루션 + 풀링레이어 → Fully Connected layer → 출력(분류)
            - ex. LeNet(7),AlexNet(7),GoogleNet(in:224x224,BGRmean:(104,117,123)),VGG16
            - OpenCV Net class
                - cv2.dnn.readNet(model,config=None, framework=None) → ret
                    - model : 훈련된 가중치를 저장하고 있는 이진파일명
                    - config : 네트워크구성을 저장하고있는 텍스트파일명
                    - framework : 명시적인 딥러닝 네트워크명
                    - retval : cv2.dnn_Net 클래스 객체

                    ![OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled.png](OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled.png)

                    ![OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled%201.png](OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled%201.png)

                    ![OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled%202.png](OpenCV%20c6419de60ab84d2c8c1bc80cce504e21/Untitled%202.png)

                - cv2.dnn.blobFromImage(imagef,scalefactor=None,size=None,mean=None,swapRB=None, crop=None,ddepth=None) → ret
                    - image : 입력영상
                    - scalefactor : 입력영상 픽셀값에 곱할 값, 기본값=1
                    - size : 출력영상크기 : 기본값(0,0)
                    - mean : 입력영사 각채널에서 뺄 평균 기본값=(0,0,0,0)
                    - swapRB : R과B 채널 서로 바꿀지여부 기본값=False
                    - crop : 크롭수행여부 기본값=False
                    - ddepth : 출력 블롭 깊이 CV_32F or CV_8U 기본값=CV_32F
                    - retval : 영상에서 구한 블록 객체
                -
