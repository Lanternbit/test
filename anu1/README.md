#IoT 실습(스마트폰으로 LED 제어하기)

## [과제 내용]

### 1. 아두이노 보드를 서버에 연결하고

### 2. LED를 부착한다.

### 3. 스마트폰으로 On, Off 버튼을 만들고 와이파이로 LED를 제어하자.

### 4. 서버 프로그램을 작성한다. (스마트폰에서 0과 1을 수신하고, 아두이노의 LED를 제어하는 서버 프로그램)

### 5. 아두이노와 프로세싱의 코드를 Github에 올린다.

### 6. 시연 동영상을 youtube에 올린다.
### * 앱인벤터는 블록을 스마트 LMS에 제출한다.

### 7. 두개의 링크를 스마트 LMS에 제출한다.


## [과제 실습]

### 1. 아두이노 코드

```
void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
}
void loop() {
  String m;
  if(Serial.available()>0) {
    String m=Serial.readString();
    if(m.indexOf('0')==0) digitalWrite(13, LOW);
    if(m.indexOf('1')==0) digitalWrite(13, HIGH);
  }
}
```

### 2. 프로세싱 코드

```
import processing.serial.*;
import processing.net.*;
Serial p;
Server s;
Client c;
void setup(){
  p = new Serial(this, "COM6", 9600);
  s = new Server(this,12345);
}
void draw(){
  c = s.available();
  if(c!=null){
    String msg = c.readString();
    msg = msg.substring(msg.length()-1);
    println(msg);
    p.write(msg);
  }
}
```

### 3. 앱인벤터 (

#### -Designer

![앱인벤터 디자인](C:\Users\서승윤\Desktop\학업\19-2\창의공학\과제 사진.png)

#### -Blocks

![앱인벤터 블럭]()

### 4. 유튜브

<>


