# IP 전송 특징의 보완: ICMP(Internet Control Message Protocol)

## ICMP의 존재 이유

IP는 신뢰할 수 없는 프로토콜이고, 비연결형 프로토콜이다. (참고로, 해당 이유는 성능 때문이다)<br/>
그렇지만, 이러한 특징을 보완해야 할 경우도 있는데 이를 해결하기 위해서는 크게 2가지 방법이 있다.

1. TCP 사용
2. ICMP 사용

`ICMP`는 **IP패킷의 전송 과정에 대한 피드백 메시지를 얻기 위해 사용하는 프로토콜로, ICMP 메시지를 통해 패킷이 상대방에게 어떻게 전송되었는지를 알려줄 수 있어서 IP전송의 결과를 엿볼 수 있다.**

참고로, 그렇다고 ICMP가 IP의 신뢰성을 완전히 보장하지는 못한다는 점을 기억하자.<br/>
**결국 신뢰성 있는 통신을 하기 위해서는 L4에서 제공하는 TCP 통신을 진행해야 한다.**

## 주요 메시지 유형

크게 `전송과정에서 발생한 오류 보고`와 `네트워크에 대한 진단 정보`로 유형을 나눌 수 있다.

- `오류 보고`
  - 네트워크 도달 불가 (Destination Network Unreachable)
  - 호스트 도달 불가 (Destination Host Unreachable)
  - 프로토콜 도달 불가, 수신지에서 특정 프로토콜을 사용할 수 없음 (Destination Protocol Unreachable)
  - 포트 도달 불가 (Destination Port Unreachable)
  - 단편화가 필요하지만 DF(Don't Fragment) 플래그가 설정되어 있어서 단편화 할 수 없음 (Fragmentation Required, and DF flag set)
  - TTL 만료 (TTL expired in transit) (TTL: Time To Live -> Packet의 수명을 의미하는 것으로 라우터를 하나 거칠때(홉) 마다 1씩 감소함)
- `네트워크 상의 정보 제공`
  - ECHO 요청
  - ECHO 응답

## 사용 예시

- `traceoute`: 네트워크 상의 경로를 확인하는 명령어
- `ping`: 네트워크 상태를 점검하기 위해 패킷을 송신하는 명령어로, ICMP를 기반으로 구현된 대표적인 명령어

## 특징

- L3의 일부로 취급된다.
- TCP 처럼 연결을 맺는 과정 없이 바로 메시지를 던진다.
- 네트워크 공격자들은 ICMP를 이용해서 서버가 살아있는지 확인하거나, 가짜 ICMP 메시지를 보내서 통신을 방해한다.
