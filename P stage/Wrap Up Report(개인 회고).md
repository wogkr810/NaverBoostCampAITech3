# Wrap UP 리포트(랩업 리포트)

## 개인 회고(개인 당 1장 내외 분량) - 2022.03.05 작성

 ( 팀 wrap -up 리포트에는 분량 때문에 작성했다가 많이 수정함.. 20220306)

---

- **이번 프로젝트에서 나의 목표는 무엇이었는가?**
    - 정량 목표
        - 대회 기간 안에 팀 내 최고(1등) 기록 달성하기 → 달성!
            - f1 loss 도입하면서 기록 달성
            - 대회 1주차 일요일 밤
        
        ![https://user-images.githubusercontent.com/46811558/156871892-1e293b8d-dce5-470f-836b-d4b9e07b3416.JPG](https://user-images.githubusercontent.com/46811558/156871892-1e293b8d-dce5-470f-836b-d4b9e07b3416.JPG)
        
        - 대회 마감 시에 전체 리더보드 안 기록에서 50%안에 들기 → 달성!
            - test data에 center crop 도입하면서 기록 달성
            - 대회 마감 4시간 전 달성
            - 개인 최고 기록도 private 1등
            
            ![https://user-images.githubusercontent.com/46811558/156872178-d3e57139-8c42-4395-8438-0da252bf7fa4.JPG](https://user-images.githubusercontent.com/46811558/156872178-d3e57139-8c42-4395-8438-0da252bf7fa4.JPG)
            
    - 정성 목표
        - 부족함을 인정하고 팀에 융화되기 →달성..?
            - 1주차 때는 많이 느려서 말도 많이 못함(만족도 70)
            - 2주차 때는 기록 달성하면서  자신감도 생기고, 능동적으로 회의 참여(만족도 100)
        - baseline 코드 이해하기 → 달성!
            - 캠퍼분들이 기록 갱신할 때 마다 마음이 급해졌지만, 차분히 이해하려고 노력함!
- **나는 내 학습목표를 달성하기 위해 무엇을 어떻게 했는가?**
    - 강의 → 2일 동안 한번 다 듣고, 1주차 주말에 한번씩 더 듣고 복습
    - 토론게시판 공유 글,슬랙 → 3일에 한번 씩 전체 다 읽기
    - 오피스아워 → 3번 들으면서, 코드 따라 쳐보기
    - 팀 노션,카톡 → 팀원분들의 속도에 맞추기 위해 자기 전에 한번씩 더 봄
- **나는 어떤 방식으로 모델을 개선했는가?**
    - vgg19bn([링크](https://pytorch.org/vision/stable/models.html))
        - 오피스 아워 시간에 시현 해 주시는 것 보고 실제로 적용 → 성능 좋지 않아서 제출 x
    - Efficientnet b6[(링크)](https://github.com/lukemelas/EfficientNet-PyTorch)
        - 서버에 b6이 적절할 것 같다는 의견 수용 + vgg19 코드 참고하여 적용 → f1 : 0.49 , acc : 63  (~~train 99, val 96 나오길래 기록 갱신할 줄..?~~)
    - Vit[(링크)](https://github.com/lukemelas/PyTorch-Pretrained-ViT)
        - 한번 적용해보고 싶어서 시도 했지만, 오래걸려서 epoch 1 → f1 : 0.28 , acc : 37
    - Efficientnet b7[(링크)](https://github.com/lukemelas/EfficientNet-PyTorch)
        - b7의 성능이 b6보다 좋기에 epoch 늘려가면서(최대 40) 시도 → f1 : 0.61 , acc : 68
    - Swin Transformer[(링크)](https://github.com/microsoft/Swin-Transformer)
        - vit와 비교하면 파라미터 수 감소 및 연산량 감소(🙏세연님)
            - baseline에 적용(1 epoch, epoch당 20분..?) → f1: 0.66 , acc : 74
            - 라이트닝에 적용(5 epoch, epoch당 9분) - > f1: 0.77 , acc: 81
- **나는 한 행동의 결과로 어떤 지점을 달성하고, 어떠한 깨달음을 얻었는가?**
    - f1 loss 적용
        - f1 loss : 0.7525 → 0.7763 달성하면서, 1위 재탈환
        - 느낀 점: 대회의 개요 파악 및 데이터에 맞는 loss 와metric에 대한 이해 필요!
    - age 밴드 수정(🙏태일님 아이디어) : (30 / 60) → (25,27,28,29,30 中 1개 /  55,58,59,60 中 1개)
        - f1 loss : 0.7763 → 0.7808
        - 느낀 점 : 배경제거하지 않은 데이터의 경우 (29,58) 이 최적!, EDA의 중요성
    - val ratio 수정
        - f1 loss : 0.7908 → 0.8022 **(태일님 샘플링 데이터)**
        - 실험 공유 노션 보면서, 세팅이 다른 부분 확인 후 제안, 태일님 데이터의 경우 샘플링을 통해 학습 데이터의 부족이 있을 수 있어서 효과가 두드러진 듯
        - 느낀 점 : 학습 데이터의 개수는 다다익선 , 실험 세팅에 맞춘 Hyper Parameter Tuning, 꼼꼼함의 중요성, 실험 결과 공유(커뮤니케이션)의 중요성
    - Test Data Center Crop
        - f1 loss : 0.7808 → 0.7822
        - 느낀 점 : EDA의 중요성 , TTA의 필요성 , ~~Test Data에 Color Jitter는 좋지 않군!~~
- **전과 비교해서, 내가 새롭게 시도한 변화는 무엇이고, 어떤 효과가 있었는가?**
    - Jupyter Notebook → vscode
        - 처음 파이썬을 배우고 접했던 대회에서부터, 주피터 노트북을 배우고 익숙해졌었다. 하지만, 팀원분들도 전부 IDE 환경에서 작업하시고, 오피스아워에서 멘토님이 PyCharm으로 멋지게 작업하시는 모습을 보고 반한 후, 스페셜 미션(‘주피터 노트북 탈출’)이 주어진 후 처음으로 작업해봤다.
        - 굉장히 어렵고, 터미널 환경도 처음이었지만, 팀원분들도 도움을 통해 적응해나갔고 완벽하지 않지만 익숙해진 후에는 작업환경도 훨씬 빨리지고 프로젝트 관리에 굉장한 도움이 됐다.
    - 개인작업 → 팀협업
        - 수학과라는 과 특성상 조별과제를 사실상 해보지 않고, 부스트캠프에 와서 처음 해봤다. 하지만, 팀원분들은 이미 익숙하셨기에 노션,깃허브,슬랙 등의 채널을 통해 굉장히 많이 도움을 받고 팀에 융화됐다. 올릴때 마다 혹시 실수하지 않을까, 두번씩 검토하면서 많은 툴에 대해 다루는 법을 배웠다.
        - 미디어로 ‘조별과제 잔혹사’ 같은 것만 접했는데, 좋은 팀원분들을 만나서 프로젝트 진행하는 것을 a to z 로 경험하며 많은 지식을 배웠다.
- **마주한 한계는 무엇이며, 아쉬웠던 점은 무엇인가?**
    - 한계
        - 처음 1등을 달성한 세팅 기준에서, 많은 아이디어를 시도해봤지만 배경제거하지 않은 데이터로는 f1 : 0.7822를 넘길 수 없었다.
        - XAI(설명가능한 AI)를 할 수 없었다.
            - 텐서보드 상 분명 잘 나와야할 것이 나오지 않음(Eff b7 train 99, val 97.. / epoch 변화)
            - 하이퍼 파라미터 튜닝이 뭐가 정답인지..? →AutoML의 중요성
    - 아쉬운 점
        - 제출할 때, 하이퍼 파라미터들 변화를 줬지만 제출 값이 같을 경우를 대비해서 확실히 체크하고 제출했어야함 (제출기회 2번 날린 꼴)
        - 실험을 진행할 때, 변화를 주고 F1이 상승할 경우에 대한 대비 부족 → 점수가 오르면 다른 인자를 또 변화해야 하나?(Ex : val ratio 변화 → epoch을 다시 늘리거나 줄여봐야 하나?)
        - 부족함에 기인한 남들보다 느린 학습속도(셋째 날에 겨우 서버 연결하고 Training 시작)
        - 실험 관리 기록 늦게 시작한 점 , 코드 리팩토링
- **한계/교훈을 바탕으로 다음 P-stage에서 스스로 새롭게 시도해볼 것은 무엇인가?**
    - 다른 캠퍼분들 보다 늦더라도, EDA 시도하여 토론 게시판에 공유해보기
    - 처음 실험할 때 부터 철저한 실험 관리 기록
    - 코드 리팩토링 → 가독성 높이기
