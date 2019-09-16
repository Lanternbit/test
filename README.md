# 19-2 0916 창의공학 3주차 과제
1. 아두이노와 브레드보드를 활용하여 조도센서를 통해 센싱한 것을 프로세싱으로 값을 받아 모니터에서
조도값이 높을 때는 초록색, 낮을 때는 빨간색이 출력되게 코딩을 하였습니다. 컴파일 시키면 모니터
속의 원이 조도센서에 들어오는 빛을 양에 따라 색이 변하도록 하였습니다. 

과제를 하면서 제가 코딩한 값이 눈에 바로바로 즉각적으로 결과가 따르니까 평소에 공부하던 것보다 더
흥미를 붙이고 할 수 있었던 것 같습니다. 4차 산업혁명이라는 말이 입학하고 많이 들었지만 별로 와닿지
않는 말 중에 하나였는데 창의공학수업을 들으면서 IOT에 대해 깊게 생각하게되고 4차산업혁명을 준비하게 되는
한 사람의 공학도가 되는 것 같아 기쁘게 느껴집니다. 오늘부터 집에가서도 꾸준히 반복하여 제 머릿속에 확실하게 
넣고 다음 수업에도 적극적으로 참여하도록 하겠습니다. 성실하고 열정적인 학생이 되겠습니다!!

-------------------------------------------------------------------------------------------------------------

2. 아두이노 코드

void setup() {

 Serial.begin(9600);
 
}

int a;

void loop() {

  a = analogRead(A0);
  
  Serial.println(++a);
  
  delay(500);
  
}

-------------------------------------------------------------------------------------------------------------

3. 프로세싱 코드

import processing.serial.*;

Serial p;

void setup(){

  size(300,300);
  
  p = new Serial(this, "COM5", 9600);
  
}

void draw(){

  if(p.available()>0){
  
    String m=p.readString();
    
    int a = int(m.trim());
    
    println(a);
    
    if(a>305) fill(0,255,0);
    
    else      fill(255,0,0);
    
    ellipse(150,150,200,200);
    
  }
  
}
