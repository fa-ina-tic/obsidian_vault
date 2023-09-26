Transformers in NLP : novel architecture that aims to solve sequense-to-sequence tasks while handling long-range dependencies with ease.

### Background
seq2seq : 입력 시퀀스를 하나의 벡터로 압축하면서 입력시퀀스의 정보가 일부 손실됨. -> 이를 보정하기 위해 attention을 활용함.
만약 attention을 보정 용도가 아니라 attention만으로 encoder, decoder를 구현한다면 성능이 어떻게 될까?
### Structure
**encoder=1, decoder=1**
![[transformer_structure_1.png]]

**encoder=6, decoder=6**
![[transformer_structure_2.png]]

RNN이 유용했던 이유는 단어가 위치에 따라 순차적으로 입력받아 처리되므로 각 단어의 위치정보를 가질 수 있다는 특성 때문.

하지만 트랜스포머는 순차적으로 단어를 받는 형식이 아니므로, 단어의 위치 정보를 다른 방식으로 전달해야 함. 보통 각 단어의 임베딩 벡터에 위치 정보들을 더하여 모델의 입력으로 사용하는데, 이를 Positional Encoding이라고 한다.

### Attention
Transformer에서는 세 가지의 어텐션이 사용됨.
![[attentions_in_transformer.png]]
