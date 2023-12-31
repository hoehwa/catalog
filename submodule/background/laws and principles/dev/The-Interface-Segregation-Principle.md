---
title:
tab: dev 
mood: # cactus | pizza | star | cupid | cheese | frog
command: # optional. require only to folders
---
### 인터페이스 분리 원칙

[위키피디아의 인터페이스 분리 원칙](https://ko.wikipedia.org/wiki/인터페이스_분리_원칙)

> 어떠한 클라이언트도 자신이 사용하지 않는 메소드에 의존하도록 강요당하면 안 된다.

'[솔리드](#솔리드)' 원칙의 네 번째이다. 이 원칙에 따르면 구성 요소의 소비자는 구성 요소가 가진 함수들 중에서 실제로 사용하지 않는 것들에 의존하면 안 된다.

예를 들면, 파일을 나타내는 구조로부터 XML 문서를 읽어들이는 메소드가 있다고 하자. 그 메소드는 오직 파일에서의 바이트 읽기, 전진, 그리고 후진 기능만이 필요하다. 만약 이 메소드가 파일 구조의 연관 없는 기능(파일 보안을 위한 권한 업데이트와도 같은)이 변하였다고 해서 업데이트가 필요하다면, 이 원칙은 무효가 된 것이다. 파일이 '탐색 가능 스트림' 인터페이스를 구현하고, XML 리더기가 사용하도록 하는 편이 나을 것이다.

이 원칙은 특히 [객체지향 프로그래밍](#todo)에서 적용되어, 인터페이스, 계층 구조, 그리고 추상 자료형을 통해 구성 요소 간의 [결합도의 최소화](#todo)를 이루려고 한다. [덕 타이핑](#todo)은 명시적 인터페이스를 제거함으로써 이 원칙을 강제한다.

<br>

참고 :

- [객체지향 프로그래밍](#todo)
- [솔리드](#solid)

- [덕 타이핑](#todo)
- [디커플링](#todo)

<br>

