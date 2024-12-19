# FinalProject
이 프로젝트 파일을 구동하기 위해서 torch, torchvision, numpy, yfinance, scikit-learn, matplotlib이 필요합니다.

이 프로젝트는 LSTM 모델을 이용하여 지난 10일 간의 주가 종가가 주어졌을 때 그 다음 날의 주가 종가를 예측하는 프로젝트입니다. 10일이 아니라 더 짧거나 긴 기간을 주는 것도 가능하지만, 기간이 길어질수록 모델의 예측 정확도가 떨어집니다.

모델 정의 : HedgeLSTM 클래스는 LSTM 모델 구조를 정의합니다. 시간순 데이터의 마지막 시기 정보만 출력합니다.

데이터셋 준비 : 주가 데이터를 얻기 위해 yfinance 라이브러리를 이용합니다. Yahoo Finance에서 주가 데이터를 다운로드하고, StockDataset 커스텀 클래스를 사용하여 주가 시계열 데이터를 처리합니다. 데이터는 정규화되고 학습 및 테스트 세트로 분리됩니다.

학습 및 평가 : train_model 함수는 모델을 학습시킵니다. evaluate_model 함수는 모델을 테스트합니다.
학습에 사용하는 loss function은 MSELoss를, optimizer는 adam을 이용했습니다.

시각화 : 실제 주가와 예측된 주가를 비교하여 그래프로 출력합니다.

주가 데이터는 다음과 같은 변수로 관리됩니다.
ticker = 'AAPL'
start_date = '2020-01-01'
end_date = '2023-01-01'
sequence_length = 10

ticker는 주식의 이름, start_date는 학습시키고자 하는 데이터의 첫 날짜, end_date는 마지막 날짜입니다. sequence_length는 며칠 동안의 종가를 주고 그 다음날 종가를 예측할지를 결정하는 변수입니다.

LSTM 모델과 관련된 변수는 다음과 같습니다.
input_size = sequence_length # 직전 n일간 주가
hidden_size = 64
num_layers = 2
output_size = 1  # 종가 예측
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

input_size는 입력받을 직전 n일간 주가의 갯수와 동일합니다. output_size는 출력할 종가의 갯수이므로 1입니다. gpu가 사용가능하다면 gpu를, 아니라면 cpu에서 연산을 합니다.
