- 현재까지의 키 입력에는 단순히 키보드를 누른것에 대한 처리만 함
- 게임에서는 다음과 같은 상황을 고려해야함
1. 키가 눌려있을때
2. 키가 내려갔을때
3. 키가 올라왔을때


<br>

- 따라서 이것을 관리할 인풋 매니저라는 클래스를 설계
![alt text](Note/imgs/inputMan.png)

### enum class에서, 마지막 원소를 End로 표시하여 size얻음
#### Enum class는 Enum과 다르게 정수형으로 암시적 형변환 불가. static_cast를 통해 변환해야함. 또한 이넘클래스명::원소 형태로 접근해야함


<br>

---
- UpdateKeys에서 모든 종류의 eky들의 상태를 확인
![alt text](Note/imgs/upk.png)



- 만들어진 키 입력도 Application 레벨에서 초기화 및 매 프레임마다 체크해야함
![alt text](Note/imgs/apiaru.png)