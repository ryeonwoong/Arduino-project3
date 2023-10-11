# 아두이노 센서 회로

![KakaoTalk_20231011_221731414](https://github.com/ryeonwoong/Arduino-project3/assets/127822756/6b5fec80-5062-4280-a706-aba0de049701)

# 실행화면

![화면 캡처 2023-10-11 224722](https://github.com/ryeonwoong/Arduino-project3/assets/127822756/9918913b-dcfa-43e1-b33b-1f3610737348)

# 아두이노 코드
```
void setup(){
  Serial.begin(9600);

}
 double th(int v) {
double t;
t = log(((10240000/v) - 10000));
t = 1 /(0.001129148 + (0.000234125*t) + (0.0000000876741*t*t*t));
t = t - 273.15; // 화씨를 섭씨로 바꾸어줌
return t;
}
void loop() {
  int a=analogRead(A0);
  Serial.println(th(a));
  delay(200);
}
```
# 프로세싱 코드
```
import processing.serial.*;
Serial p;
void setup() {
  p= new Serial(this, "COM4", 9600);
  textSize(64);
  size(200, 100);
}
String m;
void draw() {
  if (p.available()>0) {
    m = p.readStringUntil('\n');
    if (m!=null) {      
      print(m);
      background(0);
      float a =float(m.trim()); 
      if (a>27) background(255, 0, 0);
      text(m, 10, 64);
    }
  }
}
```
# 설명

일단 아두이노 코드에서 화씨를 출력하는 코드를 작성하고 화씨를 섭씨로 바꾸는 코드를 추가로 작성해준다. 위와 같이 코드를 작성함으로써 아두이노 시리얼 모니터에서는 온도가 실시간으로 측정되기시작한다. 이런 프로그램을 아두이노에 옮겨놓은 상태에서 프로세싱화면에 온도를 출력하기 위해 프로세싱 코드를 추가로 작성해준다. 프로세싱 코드에서는 일단 아두이노와 연결될수있게 Serial을 이용하여 서버를 만들어준다. 그 후 void draw 부분에서 평소에는 검은색 배경에 섭씨온도가 텍스트로 계속해서 출력되고 아두이노 온도 센서에 손을 대서 온도를 높이면 실시간으로 출력되다가 27도를 넘기면 배경이 빨간색으로 바뀌도록 설정해놓았다.

