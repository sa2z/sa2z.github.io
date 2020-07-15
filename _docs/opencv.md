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
    - 영상의 이진화(Binarization) : 영상의 픽셀값을 0 또는 1(255)로 연산
    - 히스토그램, 임계값 기준 흑백으로 변환
    - cvtColor BGR 각 8bit X 3=3byte →  565=2byte
    - 이진화, 임계값함수 : threshold

        ```jsx
        # 흑백 이진화
        cv2.THRESH_BINARY # 흑,백
        cv2.THRESH_BINARY_INV # 흑,백+반전
        # 밝기 유지
        cv2.THRESH_TRUNC
        cv2.THRESH_TOZERO
        # 자동 임계치 설정
        cv2.THRESH_OTSU
        cv2.THRESH_TRIANGLE
        
        BGR565 : 비트수
        HSV : 컬러스페이스

        src = cv2.imread('/code/opencv/lec3/namecard1.jpg')
        src = cv2.resize(src,(640,480)) // 픽셀숫자
        src = cv2.resize(src,(0,0),fx=0.5,fy=0.5) // 배율
        src_gray = cv2.cvtColor(src, cv2.COLOR_BGR2GRAY)
        _, src_bin = cv2.threshold(src_gray,130,255,cv2.THRESH_BINARY)

        ```

        - 이진화 임계값 자동추출 : Otsu
