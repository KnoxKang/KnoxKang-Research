# KnoxKang-Research

![Basic of GPS-RTK](https://www.e-education.psu.edu/geog862/sites/www.e-education.psu.edu.geog862/files/images/Lesson07/Real_Time_Kinematic.png)

## GPS-RTK의 정의

  RTK란 Real Time Kinematic의 약자로서, GNSS의 정밀도를 향상시키는 기술중 하나이다.
  이 기술은 GPS 신호에 담긴 정보(C/A 코드, P(Y) 코드 등) 사용하지 않고 GPS의 반송파(carrier wave) 그 자체를 이용하는 기술로서, 비유하자면 m단위 자(C/A 코드)를 사용하는게 아니라 mm단위 자(반송파)를 사용하는것과 같으며, 
  이론상 오차범위를 2mm내로 억제할 수 있다.
  
## 어째서 GPS-RTK같은 기술이 필요한가?

  종전의 방법으로는 민간용 정보의 경우 3m, 군용 정보로는 30cm의 정밀도를 확보할 수 있는데 둘 다 충분히 정밀한 측위가 필요한 플랫폼(측량, 자율주행 차량 등)에는 충분치 않은 정밀도이기 때문에.

## 독립 GPS-RTK시스템은 어떻게 동작하는가?
  
GPS-RTK는 GPS 신호에 담긴 정보를 사용하는 DGPS(Dual-GPS)와는 달리 반송파 추적을 통해 최소 5개 이상의(1개는 예비용) 위성으로부터 거리를 측정하여 위치를 측위한다.
  

엄연히 GPS-RTK도 반송파 추적법을 쓰는 만큼 같은 반송파 추적법을 사용하는 단일 안테나 GPS와 같은 문제점을 안고 있지만([integer ambiguity](https://github.com/KnoxKang/KnoxKang-Research/blob/master/GPS-RTK-KO.md#q2-integer-ambiguity란-무엇인가)), RTK는 모든 조건이 안정적인 경우(멀티 패스 없음, 여러개의 위성 관측 가능. 수신기가 다중 주파수 수신 가능 등) 10초 내외로 문제를 보정해낸다.
  

기본적인 RTK시스템은 두개의 GPS 수신기로 구성되는데. 하나는 한 지점에 머무르는 베이스, 다른 하나는 움직여 다니는 로버 역할이다.
  
이중 베이스는 사전에 이미 측위가 완료된 좌표에 설치되고, 그 후 로버는 베이스로부터 보정신호를 수신해서 자신의 위치를 교정하게 된다.
  
이때 RTK시스템이 정상적으로 동작하려면 RTK 시스템을 구성하고 있는 네트워크 속도는 2.4kb를 0.5초마다 한번씩은 갱신할 수 있는 4.8kbps, 또는 그보다 빠른 속도가 지원되는 네트워크로 연결될 필요가 있다.
  
만약 베이스가 사전에 측위가 완료된 좌표에 놓이지 않는다면 베이스는 PPP(Pricise Point Positioning)을 이용해 자신의 위치를 측위하기 시작하면서 점차 '안정화'되기 시작한다.
  
모든 조건이 좋다는 가정 하에 3~5분 뒤에는 PPP 연산이 끝나고, 그 뒤부터 로버는 보정 신호를 수신해 자신의 위치를 정확히 측위할 수 있다.


  
## GPS-RTK는 어떻게 NTRIP(Network Tranport of RTCM)을 사용하는가?

GPS-RTK가 NTRIP을 사용하는 경우 베이스는 필요가 없어진다. 따라서 RTK시스템을 구성하는 최소 요건은 NTRIP시스템을 사용할 수 있는 GPS-RTK수신기 하나와 인터넷에 접속할 수 있는 장비로 줄어든다.

  
NTRIP을 사용하는 절차는 사실 굉장히 간단하다. 사용자는 그저 NTRIP캐스터의 ID/PW를 알거나, 가입만 하면 되고, 나머지 절차는 로버에 해당 정보(NTRIP캐스터 주소, 포트. ID/PW)를 입력하게 되면 자동적으로 진행된다.
  
  만약 로버가 맞는 정보를 입력 받았다면 로버는 인터넷 망을 통해 NTRIP캐스터에 접속해서 connection point목록을 다운로드 받을것이고, 사용자가 그중 하나를 선택하도록 제시하거나, 가측위된 로버의 위치에서 가장 가까운 connection point에 접속해서 보정 정보를 수신한다.
  
  
## Q&A

### Q1. 어째서 NTRIP은 ID/PW를 사용해야만 보정정보를 수신할 수 있는가?
A1. NTRIP프로토콜 자체는 ID/PW를 요구하지 않는것이 맞다. 그러나 다수의 NTRIP베이스와 다수의 로버를 중간에서 관제하는 NTRIP caster가 ID/PW를 요구하는것 뿐이다.

### Q2. 'Integer ambiguity'란 무엇인가?
A2. '정수 불확실성'으로 번역되는 inetger ambiguity는 GPS수신기가 수신기와 위성간의 거리를 측정할때 NCO(numerically controlled oscillator)를 사용해 GPS신호와 동일한 파장과 위상을 갖는 신호를 생성한 후, 그것을 사용해 거리를 예상하기 때문에 일어나는 현상이다. 이때 NCO는 신호를 생성한 후 NCO로서는 신호 사이클을 구분할 수 없으니 그 신호를 가장 가까운 위상에 맞추려고 시도하게 되고, 따라서 언제나 거리 불확실성은 파장의 정수배로 나타나며, 오차로 남게 된다.
