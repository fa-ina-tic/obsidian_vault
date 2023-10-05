---
reference: https://gbdai.tistory.com/37
---

Seq2Seq
- 입력된 시퀀스로부터 다른 도메인의 시퀀스를 출력하는 모델
- 기계번역, 챗봇, text summarization 등 다양한 분야에서 사용됨

크게 세 가지 부분으로 나뉨
- Encoder
- Decoder
- Generator

### Encoder
입력되는 sequence의 정보를 최대한 보존하도록 압축을 진행하는 역할을 한다. **즉, 문장의 의미가 잘 담겨있는 상태로 높은 차원에 있던 data를 낮은 차원의 latent space에 투영시키는 것** 

seq2seq에서 encoder는 입력을 받은 뒤, 정보를 보존하도록 압축을 진행하고, 이렇게 압축한 정보인 context vector를 decoder에게 넘겨준다.

### Decoder
encoder로 압축된 정보를 입력하는 sequence와 같아지도록 압축 해제하는 역할을 한다. **즉, encoder가 압축한 정보를 받아서 단어를 하나씩 뱉어내는 역할**
seq2seq에서의 decoder는 encoder로부터 정보를 받아온 뒤, encoder의 마지막 hidden state를 decoder의 initial state로 넣어준다.
이러한 decoder는 encoder로부터 문장을 압축한 context vector를 바탕으로 문장을 생성, [[auto-regressive model]] 이기에 bi-directional RNN을 사용하지 못함

### Generator
decoder의 hidden state를 받아 현재 timestemp의 출력 token에 대한 확률 분포를 반환

![[Pasted image 20231005160437.png]]
generator의 output은 decoder에서 다음 timestep의 hidden state를 구하는 대에 사용됨