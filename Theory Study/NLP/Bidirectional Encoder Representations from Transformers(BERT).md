2018년 구글에서 공개한 pre-trained model.

pretrained-model을 downstream task에 적용하는 방식은 크게 두가지
1. feature-based
	1. pre-trained representation을 architecture의 추가적인 feature로 사용하는 방법론
2. fine tuning
	1. pre-trained parameter 전체를 가지고 downstream task에서 학습하여 task-specific parameter를 최소화하는 방법

얘네들은 unidirectional language model(단방향 언어 모델)을 사용했다는 공통점이 있음.

단방향 언어 모델의 한계점
1. 사용할 수 있는 architecture의 선택 제한
2. pre-trained representation 성능 제한

이를 MLM을 활용해 deep bidirectional transfer architecture를 pre-trained하도록한 모델이 BERT다.

