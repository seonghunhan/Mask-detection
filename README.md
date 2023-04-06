# COVID-19 Face Mask Detection

Face and mask detection using CNN

![마스크찍은사진](https://user-images.githubusercontent.com/88662101/230330671-a13f9fc8-a168-408f-851f-b8bbb62b8bc7.jpg)

## Requirement

- TensorFlow 2+ (2.2v) -> CPU, GPU 2가지를 함께 설치해야 한다.
- OpenCV
- numpy
- matplotlib

## 코드 설명
![image](https://user-images.githubusercontent.com/88662101/230339435-e2c3a85c-832e-4ae4-83e8-980f94763acd.png)
- tensorflow 2.2v을 Anaconda에다가 설치


![image](https://user-images.githubusercontent.com/88662101/230339809-04628efe-2066-42bb-8992-dfb8467e5a11.png)
- facenet -> face detection model을 load (사진에서 얼굴을 찾는 작업)
- model -> mask detector model을 load (그 얼굴에서 마스크를 찾는 작업)


![image](https://user-images.githubusercontent.com/88662101/230340043-28a654d2-2ba1-4e60-8b83-45beba2af360.png)
- openCV의 facenet을 사용함으로 학습시키기 위한 Parameter를 입력해준다.
- Face Detection의 결과가 dets에 저장된다.


![image](https://user-images.githubusercontent.com/88662101/230340203-ff6648c9-c0e5-4485-9545-24141eae66b2.png)
- 여러 개의 얼굴이 Detection될수도 있으므로 for문으로 반복시킨다.
- detection한 결과가 confidence(자신)없으면 넘긴다.(0.5기준으로)
- x와 y의 bounding값을 추출한다.
- 원본에서 bounding한값을 얼굴만 잘라서 face에 저장한다.
- 여러 face를 faces에 저장한다.
- faces에 저장된 값들이 잘 출력 되는지 imshow를 통해서 확인한다.


![image](https://user-images.githubusercontent.com/88662101/230340382-fa7cdeb8-2e9d-4794-bd13-4065fe516417.png)
- faces의 개수만큼 loop를 돌면서 Mask착용 여부를 예측한다.
- size를 224, 224로 resize시킨다.
- cvtColor를 통해서 BGR을 RGB로 바꿔준다.
- shape이 (224, 224, 3)라서 model에 넣을 때는 (1, 224, 224, 3)이어야 한다. 그러므로 expand_dims를 통해서 0번 axis에 1차원 늘려준다.
- model에 predict함수를 통해서 2개의 output을 추출한다.
- 사진위에 마스크를 썼을 확률을 추출한다.


## 느낀 점
- 가로비율이 세로비율보다 높아야 코드가 정상적으로 실행된다.
- 마스크 착용시 대부분 90%이상의 결과값이 도출된다.
- 마스크 미 착용시 대부분 5%미만의 결과값이 도출된다.
- 불특정 장애물을 얼굴에 가릴 경우 얼굴을 인지 못하거나 낮은 결과값이 도출된다.
- 실험3과 실험6을 비교시에 같은 사이즈의 물체로 얼굴을 가려도 같은 결과가 도출되지 못한다.
- 실험5와 같이 마스크와 비슷한 크기의 물체를 대입하면 높은 확률의 결과값이 도출된다.
- 실험4와 같이 투명한 물체일 경우 마스크 미 착용시보단 높은 확률의 결과값이 도출된다.
- 같은 사진을 반복하여도 같은 결과값이 도출된다.



## Reference
- Dataset: https://github.com/prajnasb/observations
- Code: https://www.pyimagesearch.com/2020/05/04/covid-19-face-mask-detector-with-opencv-keras-tensorflow-and-deep-learning/
