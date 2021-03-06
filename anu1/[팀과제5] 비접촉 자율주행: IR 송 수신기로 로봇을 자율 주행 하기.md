# 비접촉 자율주행: IR 송 수신기로 로봇을 자율 주행 하기

## [과제 내용]

### 학습내용: IR 송 수신기로 로봇을 자율 주행 하기

>1. 회로 만들기
  - IR 송신 후 반사 회로 만들기
  - 송신회로/수신회로
  - IR센서 구분하기
  - 저항 구분하기
>2. 기본적인 테스트
  - 송신 수신을 확인 하기 (최소 코드를 만든다)
>3. 영혼을 불어 넣기
  - 코드 작성 및 업로드하기
>4. 과제 제출
  - 팀별 과제를 보고서를 작성한다.
  - 소스코드와 보고서는 Github에 올린다.
  - 동영상을 유튜브에 올린다.
  - 작성 소감을 적는다.
#### □ 유튜브 동영상 1분 이내로 작성하여 올리기 (채널을 만들고 올리세요.)
>1. 목소리나 음악을 꼭 넣는다.
   * 무엇을 데모하는 영상이며. 어떤 원리로 되는지 등을 ...
   *  A4용지에 큰 글씨로 적어서 보여 주는 것도 괜찮아요.
 
>2. 테스트 환경을 책, 박스 등으로 만들고, 깨끗한 환경에서 잘 촬영을 한다.
 
>3. 친구들에게 카톡 등으로 홍보하여, 유튜브를 클릭하여 5회 이상 조회수를 만든다.
#### □ 구현시 주의
>1. 배터리가 충분하지 않으면 작동 되지 않습니다.
>2. 저항이 알맞지 않으면 센싱하는 거리가 달라 집니다.
>3. 뒤로 전진하는 경우 13번과 12번 "서보모터" 핀을 서로 바꾸거나, 소스코드에서 수정을 한다.
>4. 팀원 모두가 함께 학습하도록 합니다.


<hr/>


## [과제 실습]

### 시나리오

- IR LED가 1초에 38kHz로 신호를 보낸다.
- 1초 후 IR receiver가 부딪혀 돌아온 신호를 받는다. 
- 다시 1초 후 0이나 1로 변환시켜준다. 
- 그 신호를 바탕으로 진행방향의 벽이나 장애물을 인식해 피해간다.

### 소스코드

```
#include <Servo.h> 
 
Servo servoLeft;
Servo servoRight;
 
void setup() {
  pinMode(10, INPUT);  pinMode(9, OUTPUT);   // 왼쪽 IR LED & 수신기
  pinMode(3, INPUT);  pinMode(2, OUTPUT);    // 오른쪽 IR LED & 수신기

  servoLeft.attach(13);
  servoRight.attach(12);
}  
 
void loop() {
  int irLeft = irDetect(9, 10, 38000);       // Check for object on left
  int irRight = irDetect(2, 3, 38000);       // Check for object on right

  if((irLeft == 0) && (irRight == 0)) {      // If both sides detect
    backward(1000);                          // Back up 1 second
    turnLeft(800);                           // Turn left about 120 degrees
  }
  else if(irLeft == 0) {                     // If only left side detects
    backward(1000);                          // Back up 1 second
    turnRight(400);                          // Turn right about 60 degrees
  }
  else if(irRight == 0) {                    // If only right side detects
  
    backward(1000);                          // Back up 1 second
    turnLeft(400);                           // Turn left about 60 degrees
  }
  else {                                     // Otherwise, no IR detected
  
    forward(20);                             // Forward 1/50 of a second
  }
}

int irDetect(int irLedPin, int irReceiverPin, long frequency) {
  tone(irLedPin, frequency, 8);              // IRLED 38 kHz for at least 1 ms
  delay(1);                                  // Wait 1 ms
  int ir = digitalRead(irReceiverPin);       // IR receiver -> ir variable
  delay(1);                                  // Down time before recheck
  return ir;                                 // Return 1 no detect, 0 detect
}  

void forward(int time) {                     // Forward function
  servoLeft.write(1700);         // Left wheel counterclockwise
  servoRight.write(1300);        // Right wheel clockwise
  delay(time);
}

void turnLeft(int time) {                    // Left turn function
  servoLeft.write(1300);         // Left wheel clockwise
  servoRight.write(1300);        // Right wheel clockwise
  delay(time);
}

void turnRight(int time) {                   // Right turn function
  servoLeft.write(1700);         // Left wheel counterclockwise
  servoRight.write(1700);        // Right wheel counterclockwise
  delay(time);
}

void backward(int time) {                    // Backward function
  servoLeft.write(1300);         // Left wheel clockwise
  servoRight.write(1700);        // Right wheel counterclockwise
  delay(time);
}
```

### 회로도 ( 피에조 스피커 제외 )

![브레드보드](https://user-images.githubusercontent.com/50915637/68905408-6b918d80-0784-11ea-9096-69c6887d5dd7.PNG)

### 유튜브

https://youtu.be/Byyw9zJp2Uw


<hr/>


### 소감

> 서경호 : IR을 처음 만나서 사용해보는 과제였습니다. 이번 과제를 하면서 평소에 가지고 있던 궁금증을 어느정도 채울 수 있었던 것 같습니다. 아두이노는 이미 여러 곳에 사용되고 있다는 말을 듣고 사실 처음에는 실감이 안났는데 이번 과제를 하면서 그걸 더 체감할 수 있는 기회가 되었습니다. 심지어 저와 동기들이 이것을 이용할 수 있다는게 정말 신기한 것 같습니다. 앞으로도 열심히 하겠습니다.

> 이주협 : 아두이노 접촉식에 이어 비접촉식으로 방해물을 피해가는 로봇을 만들어 봤습니다. 비접촉식도 신기했지만 우리가 흔히 쓰는 리모콘등 사람 눈으로 볼 수 없는 빛으로 식별 한다는데서 신기함을 느꼈고 흔히 쓰는 사물을 다시 보는 기회가 됐습니다. 코드를 수정해 가며 마침내 성공하는 기분이 아두이노 공부를 하게 만드는 원동력 인거 같고 매우 재밌게 과제를 수행 했습니다. 교수님 사랑합니다♥

> 김동해 : 아두이노 로봇이 처음에는 생각대로 잘 움직여지지 않아 고민이었습니다. 하지만 팀원들과의 상호작용을 통해 코드수정을 거듭하면서, 마침내 저희들이 원하는대로 나름 움직이는걸 보니, 매우 큰 뿌듯함을 느꼈습니다. 앞으로도 열심히 머리를 굴려서 교수님의 열정적인 가르침 아래에서 아두이노의 전문가가 될 수 있도록 노력하겠습니다.

> 이호현 : ir송/수신기를 통해 방해물을 접촉하지 않고도 피해갈 수 있는 것이 매우 신기하였고 a bot이 처음에는 반대로 가여서 어리둥절 했었는데 교수님의 도움으로 어렵지 않게 해결 할 수 있었습니다. 늘 새롭고 재밌는 수업을 가르쳐 주셔서 감사합니다!

