Block Chain Develop
------


### 블록체인 개발자의 역할
- 주된 역할은 어플리케이션, 스마트 컨트랙트의 개발(Application, Smart Contract)
- 블록체인과 원장의 상호관계나 타 시스템과의 연동과 관련한 개발(Ledger, Traditional Processing platforms, Data Source, Event, Systems Integration)
- 블록체인 동작 구조에 대해 반드시 알 필요는 없음(Peers,Consensus,Security)

### 블록체인 운영자의 역할
- 블록체인 동작 구조에 대해 상세히 파악해야함(Peers,Consensus,Security)
- 블록체인 개발을 할 수 있어야 하는건 아님(Application, Smart Contract)

최근에는 DevOps등 운영과 개발이 합쳐지는 경향

### 블록체인 아키텍트의 역할
- 개발과 운영관점에서 많은 지식을 보유해야 함
- Business concerns, Design Tradeoffs 등의 영역도 고려



![hyperledger fabric](https://media.vlpt.us/images/dsunni/post/f4f8152a-6b5b-4db1-9b06-953021f8c78d/644df7d73a0a4b7086f98c4a885cdf3b.jpg)
[Ref](https://leeminki.github.io/blockchain/2018/09/07/Youtube_hyperledger_2.html)

![](https://user-images.githubusercontent.com/28076542/45217911-cad25300-b2e0-11e8-90fc-910afa08198a.png)
- 레저(ledger) + 전체 상태(world state)
- 블록들은 연결됨, 블록에는 거래정보가 있다
- 체인코드를 실행한 결과는 이더리움은 State Tree에 저장, 하이퍼레저는 World State(전체 상태 자료구조)에 저장
- 상태 정보를 유지하는 방식은 일반적
- 이더리움은 계좌정보를 저장, 하이퍼레저 패브릭은 어떤 정보라도 버전별로 저장
- Key-Value 방식으로 저장하며 같은 Key에 대하여 값이 계속 달라지므로 버전 방식으로 관리

### world state

- 거래 실행 결과에 따라 변경되는 블록체인의 상태 변화 정보를 저장
- 버전형 키-값 저장소(vKVS-versioned Key-Value Store) 형태로 모델링
- 키(Key): 체인코드(chaincode)가 사용하는 정보 이름
- 값(value): 이름에 대응되는 정보
- 버전(version)은 특정 키, 값 쌍의 상태를 번호(number)로 표시
- 값이 갱신될 때마다 새로운 version number가 부여되어 기존의 키-값 쌍의 상태 구분


#### 상태 변화 

(car.no = 1234, car.owner = park, car.maker = Hyundai)
–> (car.no = 1234, car.owner = kim, car.maker = Hyundai)

- 같은 차를 다른 사람에게 판 상황
- 상태 정보가 변경된 것

#### 키 버전 변화

(s(car.owner.value) = park, s(car.owner.version) = 5)
–> (s(car.owner.value) = kim, s(car.owner.version) = 6)

- 이 때 차에 대한 버전을 5에서 6으로 변화
- 변경되는 상태 정보를 유지할 수 있게 함
- (key, version, value) 형태로 만든 것
- 전체 상태 = 블록체인의 모든 거래가 접근하는 키 집합에 대한 현재의 값과 버전 정보 집합

### 레저(ledger)

- 시스템 운영 과정에서 발생하는 모든 거래 정보를 해시체인(hash chain) 형태로 저장
- 블록에 포함되는 거래의 수는 응용의 요구사항에 따라 달라질 수 있음
- 레저를 통해 전체 상태 변경의 이력 추적 가능

### 하이퍼레저 패브릭의 거래 처리 순서 (Consensus)

![](https://user-images.githubusercontent.com/28076542/45219920-6a92df80-b2e7-11e8-92ef-f9d3feee06b8.png)

- CC = ChainCode
- 체인코드의 실행 결과는 몇몇의 endorser에게 의뢰하고 그 결과를 받음
- 실행결과와 거래 정보를 Order Tx에서 합의함
- Ordering service는 다른 블록체인에서는 Consensus 프로토콜이라 함
- 순서가 결정되면 committer에게 보내며 문제가 없는지 검증함
- 검증이 완료되면 Ledger에 저장

### Application 흐름

![](https://d1.awsstatic.com/blockchain_assets/Hyperledgerfabricdiagram.83ce5564e344459d113343595b2152d31791f79b.png)
- 발생된 트랜잭션을 클라이언트 SDK를 Endorsor peer에 전달
- Endorsor peer가 트랜잭션을 체인코드를 통해 검증하고, 실행한 후 결과(R/W Set)를 클라이언트레 반환
- 반환된 응답을 Orderer에 전달
- Orderer(kafka 등)는 전달된 트랜잭션을 전달받고 트랜잭션이 검증되면 모든 Peer에 전달된다.
- WorldStateDB에 값이 저장되고 원장이 업데이트 된다.

- 
![](https://miro.medium.com/max/1400/1*2m8OvLXa6leRE52Usiuh-Q.png)

Chaincode

- hyperledger fabric의 smartcontract
- 체인코드는 Endorsing Peer 프로세스로 부터 격리된 안전한 Docker Container에서 실행됨
- Application에 의해 전송된 트랜잭션을 통해 초기화하고 원장의 상태를 관리
- 체인코드에 의해 생성된 원장 상태는 해당 체인코드로만 범위가 지정되어 다른 체인코드에 직접 Acess할 수 없지만 접근권한이 주어지면 동일한 네트워크안에 다른 체인코드를 호출할 수 있음
-  