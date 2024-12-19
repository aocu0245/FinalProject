# FinalProject
이 프로젝트 파일을 구동하기 위해서 torch, torchvision, numpy, yfinance, scikit-learn, matplotlib이 필요합니다.

이 프로젝트는 LSTM 모델을 이용하여 지난 10일 간의 주가 종가가 주어졌을 때 그 다음 날의 주가 종가를 예측하는 프로젝트입니다. 10일이 아니라 더 짧거나 긴 기간을 주는 것도 가능하지만, 기간이 길어질수록 모델의 예측 정확도가 떨어집니다.

모델 정의 : HedgeLSTM 클래스는 LSTM 모델 구조를 정의합니다. 시간순 데이터의 마지막 시기 정보만 출력합니다.

데이터셋 준비 : 주가 데이터를 얻기 위해 yfinance 라이브러리를 이용합니다. Yahoo Finance에서 주가 데이터를 다운로드하고, StockDataset 커스텀 클래스를 사용하여 주가 시계열 데이터를 처리합니다. 데이터는 정규화되고 학습 및 테스트 세트로 분리됩니다.

학습 및 평가 : train_model 함수는 모델을 학습시킵니다. evaluate_model 함수는 모델을 테스트합니다.
학습에 사용하는 loss function은 MSELoss를, optimizer는 adam을 이용했습니다.

시각화 : 실제 주가와 예측된 주가를 비교하여 그래프로 출력합니다.
