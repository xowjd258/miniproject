# 물고기 도감 프로젝트
+ 물고기 사진을 받으면 물고기 종류를 구별해주는 프로젝트입니다
+ 계속해서 버전을 업데이트 할것입니다.
+ 현재 이미지는 classification으로 진행되고있는데, custom dataset을 이용한 object detction으로 바꿀 예정입니다
+ object detction은 조금 오래 걸릴것 같습니다 

## 이미지 크롤링 하고 dataset을 train/validation으로 나누기(Window 기준)
---

+ 이미지 크롤링 하기에 앞서 필요 라이브러리를 다운 받습니다.

```
pip3 install selenium bs4
```
+ 이후 chromedriver.chromium.org/downloads 에 접속해 크롬 브라우저 버전에 맞는 크롬 드라이버를 설치해주세요(설치 폴더는 c:에 해주세요. 기본적으로 소스코드가 c:로 설정되어있습니다)
+ 크롬 브라우저 버전은 chrome://version에서 확인 할 수 있습니다.
+ 설치가 완료되고 나면 에디터로 crawl.py를 열어, dataset을 어디다 받을지 정해주세요
+ 기본 설정 폴더는 c:/crawling/ 입니다

+ 이제 크롤링을 시작합니다. 아래의 파일을 실행하면, 검색 키워드와 몇 장 크롤링 할 것인지에 대해 입력을 해주세요. 그럼 크롤링이 시작됩니다.
+ 크롤링이 진행됨과 동시에 train폴더와 val폴더가 생성됩니다. training 할 머신에 크롤링 폴더 전체를 옮겨주세요

```
python3 crawl.py
```
---
## 이미지 training 및 validation(리눅스 기준)
+ 이미지 training과 validation에 필요한 라이브러리를 받습니다.
```
pip3 install torch torchvision matplotlib
```
+ 에디터로 36번 라인에서 dataset 위치를 자신의 데이터셋 위치로 바꾸어주세요
+ 기본적으로 '/home/kim/crawling'으로 설정되어있는데, 이 부분을 수정하면 됩니다.
+ 이제 테스트와 validation을 시작합니다.
```
python3 img_train_and_validation.py
```
+ 정상적으로 training이 됐다면 다음과 같은 이미지가 뜨고, 이미지를 모두 닫으면 프로그램이 종료됩니다.
![Figure_1](https://user-images.githubusercontent.com/55902342/111029839-382b4580-8442-11eb-8a82-1871aaca2fa8.png)
![Figure_2](https://user-images.githubusercontent.com/55902342/111029869-627d0300-8442-11eb-9f32-0daba48fe726.png)
![Figure_3](https://user-images.githubusercontent.com/55902342/111029871-63ae3000-8442-11eb-8944-a41b779b2ff6.png)


---
## (작업중) customdataset YOLO v5
+ https://curiousily.com/posts/object-detection-on-custom-dataset-with-yolo-v5-using-pytorch-and-python/ 를 참고하여 만들어 졌습니다.
+ file 구조 확인 및 annotation 확인
```
!tree clothing -L 2
!cat clothing/labels/train/0.txt
```
+ YOLO setup + dataset
```
!pip install torch==1.5.1+cu101 torchvision==0.6.1+cu101 -f https://download.pytorch.org/whl/torch_stable.html
!pip install numpy==1.17
!pip install PyYAML==5.3.1
!pip install git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI
!git clone https://github.com/NVIDIA/apex && cd apex && pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" . --user && cd .. && rm -rf apex
!gdown --id 1uWdQ2kn25RSQITtBHa9_zayplm27IXNC
!git clone https://github.com/ultralytics/yolov5
%cd yolov5
!git checkout ec72eea62bf5bb86b0272f2e65e413957533507f
```
+ model용 configuration file 하나, dataset용  configuration files하나 준비
```
!gdown --id 1ZycPS5Ft_0vlfgHnLsfvZPhcH6qOAqBO -O data/clothing.yaml
!gdown --id 1czESPsKbOWZF7_PkCcvRfTiUUJfpx12i -O models/yolov5x.yaml
```
+ train with custom dataset
```
!python custom_dataset.py --img 640 --batch 4 --epochs 30 \
  --data ./data/clothing.yaml --cfg ./models/yolov5x.yaml --weights yolov5x.pt \
  --name yolov5x_clothing --cache
```

