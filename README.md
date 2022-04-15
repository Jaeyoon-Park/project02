# 설치
가급적 colab 환경(런타임 GPU 가속)으로 실행해주세요.

첫번째 cell은 사용할 라이브러리를 가져옵니다.

두번째 cell은 hyper parameter optimization을 위해 keras-tuner를 설치합니다.
```python
!pip install -q -U keras-tuner
import keras_tuner as kt
```
세번째 cell은 현재 github repository에 있는 파일을 가져옵니다.
```python
!git clone https://github.com/Jaeyoon-Park/project02
%cd project02
```
정상적으로 repository를 가져왔을 경우, 아래의 cell로 샘플 이미지를 확인할 수 있습니다.
```python
os.chdir('./dataset')
print(os.getcwd())
sampleimg = cv2.imread("./test/freshapples/Screen Shot 2018-06-08 at 5.03.40 PM.png")
print(sampleimg.shape)
cv2_imshow(sampleimg)
```
# 사용법
## Data Preprocessing
Model에 입력될 input image는 (28, 28) 크기입니다.

전체 데이터 중 0.8은 train data, 0.2는 validation data로 사용됩니다.

test data는 별도 폴더에 분류되어 있습니다.

## DNN Model
'3-1. Create DNN Model' 제목의 cell은 직접 구성한 DNN 모델입니다.

해당 모델의 learning rate와 첫번째 dense layer unit수를 최적화하려면

'3-2. Create DNN Model (Hyperparameter Tuning)' 제목의 cell을 순서대로 실행해주세요.
## Results
현재는 최적화된 모델을 기반으로 결과를 보여줍니다.

만약 3-2 대신 3-1만 진행했다면, 'history_op' 대신 'history'로 변경해주세요.

아래의 cell에서 test dataset에 대한 loss와 accuracy를 확인할 수 있습니다.
```python
# Test dataset
test_loss, test_acc = model_op.evaluate(test_set, verbose=2)
```
## Save & Load Model
순서대로 cell을 실행하면 현재 train이 완료된 model을 저장할 수 있습니다.

만약 3-1의 model을 저장하고 싶다면 아래의 cell에서 model을,

3-2의 model을 저장하고 싶다면 model_op로 변경해주세요.
```python
# ./saved_model/my_model 폴더 생성 후 저장
!mkdir -p saved_model
model.save('saved_model/my_model')
```
## Test on Video
저장된 모델을 기반으로 사과가 썩어가는 과정을 촬영한 영상에 test를 진행합니다.

첫번째 cell을 실행하면 경로에 저장된 샘플 영상을 불러옵니다.

정상적으로 영상을 불러왔을 경우, 영상의 크기와 프레임수, fps가 출력됩니다.

두번째 cell을 실행하면 사과가 썩었다고 판단되는 시점의 프레임이 출력됩니다.

기준은 0.1로 되어있으며, 0에 가까울수록 신선한 사과, 1에 가까울수록 썩은 사과입니다.

따라서, 경우에 따라 기준을 조정할 수 있습니다. 
