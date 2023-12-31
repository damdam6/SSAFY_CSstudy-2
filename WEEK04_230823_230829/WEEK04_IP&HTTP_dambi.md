# CS 2장 네트워크(3)

날짜: 2023/08/29
태그: study
세부항목: CS스터디, SSAFY, study
velog/blog/git: git

# 2장 네트워크

## 2.4 IP 주소

### 2.4.1 ARP

- ARP
    - IP주소에서 ARP를 통해 MAC 주소를 찾아 MAC 주소를 기반으로 통신
    - Address Resolution Protocol - IP 주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜
        
        ⇒ 가상의 주소 IP → MAC주소 사이의 변환을 담당함(반대는 RARP)
        

** 브로드캐스트

송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전송되는 방식

** 유니캐스트

고유 주소로 식별된 하나의 네트워크 목적지에 1:1로 데이터를 전송하는 방식

### 2.4.2 홉바이홉 통신

- 홉바이홉 통신
    - IP 주소를 통해 통신하는 과정
    - 각 패킷이 여러 개의 라우터를 건너는 모습을 비유적으로 표현
    - 통신 잧이에 있는 ‘라우팅 테이블’의 IP를 통해 시작주소부터 시작하여 다음 IP로 계속해서 이동하는 라우팅 과정 → 패킷이 최종 목적지까지 도달
- 라우팅 테이블
    - routing table
    - 송신지에서 수신지까지 도달하기 위해 사용됨
    - 목적지 정보들과 그 목적지로 가기 위한 방법이 들어있는 리스트
- 게이트웨이
    - 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 관문 역할을 하는 컴퓨터나 소프트웨어를 두루 일컫음
    - 게이트 웨이 → 서로 다른 네트워크 상의 통신 프로토콜을 변환해주는 역할을 하기도 함

### 2.4.4 IP 주소 체계

- IPv4 vs IPv6
    - IPv4 : 32비트를 8비트 단위로 점을 찍어 표기
    - IPv6 : 64비트를 16비트 단위로 점을 찍어 표기

- 클래스 기반 할당 방식
    - 주소를 5개의 클래스로 구분하는 방식
    - 앞을 네트워크 주소 - 뒤를 호스트 주소
    
    [[네트워크] IP,IP 클래스, IPv4, IPv6이란? | IP 클래스 구분](https://code-lab1.tistory.com/33)
    

- DHCP
    - Dynamic Host Configuration Protocol
    - IP 주소 및 기타 통신 매개 변수를 자동으로 할당하기 위한 네트워크 관리 프로토콜

- NAT
    - Network Address Translation
    - 패킷이 라우팅 장치를 통해 전송되는 동안 패킷의 IP 주소 정보를 수정하여 IP주소를 다른 주소로 매핑하는 방법
        
        → IPv4 주소 체계만으로 많은 주소들을 모두 감당하지 못하는 단점을 보완
        
        → NAT로 공인 IP와 사설 IP로 나눠서 많은 주소처리
        
    - 공유기와 NAT
        - 여러 대의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위해 NAT을 사용함
    - NAT을 이용한 보안
        - 내부 네트워크에서 사용하는 IP와 외부에 드러나는 IP 주소를 다르게 유지 가능
    - NAT의 단점
        - 여러 명이 동시에 접속하게 되므로 실제 접속하는 호스트 숫자에 따라 접속 속도가 느려질 수 있음
        

### 2.4.4 IP 주소를 이용한 위치 정보

- IP 주소는 위치 추적이 가능함…

---

## 2.5 HTTP

- HTTP
    - 전송 계층 위에 있는 애플리케이션 계층
    - 웹서비스 통신에 사용됨

### 2.5.1 HTTP/1.0

→ 한 연결 당 하나의 요청을 처리하도록 설계

- RTT 증가
    - RTT : 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간
        
        ⇒ 패킷 왕복 시간
        
    
- RTT의 증가를 해결하기 위한 방법
    - 이미지 스플리팅, 코드 압축, 이미지 Base64 인코딩을 사용하곤 함
    
    - 이미지 스플리팅
        - 많은 이미지가 합쳐잇는 하나의 이미지를 다운 → 이를 기반으로 background-image의 position을 이용하여 이미지 표기
    - 코드 압축
        - 코드를 압축해서 개행 문자, 빈칸을 없애서 코드 크기 최소화
    - 이미지Base64 인코딩
        - 64진법으로 이루어진 문자열로 인코딩하는 방법
        - BUT 크기가 커지는 단점이 있음
        

### 2.5.2 HTTP/1.1

- HTTP/1.1
    - 매번 TCP에 연결하는것이 아니라 한 번에 TCP초기화를 한 이후에 keep-alive라는 옵션으로 여러 개의 파일을 송수신할 수 있음
    - 기존에도 존재는 했으나.. 이때부터 표준화 됨

- HOL Blocking
    - Head of Line Blocking
    - 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능저하 현상
- 무거운 헤더 구조
    - 쿠키 등 많은 메타 데이터 → 압축되지 않아 무거음

### 2.5.3 HTTP/2

- HTTP/1.x 대비
    - 지연시간을 줄이고 응답 시간을 빠르게
    - 멀티플렉싱, 헤더 압축, 서버 푸시, 요청의 우선순위 처리 지원

- 멀티플렉싱
    - 여러 개의 스트림을 사용하여 송수신한다는 것
    - 특정 스트림 패킷이 손실되었다고 해도 해당 스트림에만 영향을 미치고 나머지 스트림은 멀쩡하게 동작
    - 병렬적 스트림 서빙 / 스트림 내의 데이터도 쪼개져 있음
    
    ⇒ HOL Blocking 해결 가능
    

- 헤더 압축
    - 허프만 코딩
        - 문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트 수, 낮은 정보는 많은 비트 수 → 전체 비트 양 줄이기

- 서버 푸시
    - HTTP/2 클라리언트 요청 없이 서버가 바로 리소스를 푸시할 수 있음

### 2.5.4 HTTPS

- HTTPS
    - HTTP/2는 HTTPS 위에서 동작
    - 애플리케이션 계층과 전송 계층 사이에 신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP요청을 말함
    - 통신을 암호화 함.

- SSL/TLS
    - SSL
        - TLS의 이전버전 → TLS로 통합 되었으나 통칭해서 부름
    - 전송 계층에서 보안을 제공하는 프로토콜
        - 클라이언트와 서버가 통신할 때 제 3자가 메시지를 도청하거나 변조하지 못하도록 도움
    - 보안 세셴을 기반으로 데이터를 암호화하며 보안 세션이 만들어질 때 인증 메커니즘, 키 교환 암호화 알고리즘, 해싱 알고리즘이 사용됨
- 보안 세션
    - 세션
        - 운영체제가 어떠한 사용자로부터 자신의 자산 이용을 허락하는 일정한 기간을 뜻한다
    - 클라이언트에서 사이퍼 슈트cypher suites를 서버에 전달하면 서버는 받은 사이퍼 슈트의 암호화 알고리즘 리스트를 제공할 수 있는지 확인
        - 서버에서 클라이언트로 인증서를 보내는 인증 매커니즘이 시작 되고 이후 해싱 알고리즘 등으로 암호화된 데이터 송수산
    
    - 사이퍼 슈트
        - 프로토콜, AEAD 사이퍼 모드, 해싱 알고리즘이 나열된 규약
        - 다섯개 존재
    - AEAD  사이퍼 모드
        - 데이터 암호화 알고리즘
- 인증 매커니즘
    - CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이루어짐
    - 인증서 ⇒ 안전한 연결을 시작하는데 있어 필요한 공개키를 클라이언트에 제공 / 사용자가 접속한 서버가 신뢰할 수 있는 서버임을 보장
    - 공인된 기업에서 CA발급

- 암호화 알고리즘
    - 대수곡선 기반의 ECDHE
    - 모듈식 기반의 DHE
    
    - 디피-헬만 키 교환 암호화 알고리즘
        
        [만난 적 없어도 서로를 믿게 해주는 디피 헬만 키 교환 알고리즘의 마법](https://injae-kim.github.io/dev/2020/08/07/diffie-hellman-algorithm.html)
        
    - 해싱 알고리즘
        - 데이터를 추정하기 힘든 더 작고, 섞여있는 조각으로 만드는 알고리즘
        - SSL/TLS는 해싱 알고리즘 -  SHA-256, SHA-384 알고리즘을 씀
        
        - SHA-256 알고리즘
            - 해시 함수의 결괏값이 256비트
            - 비트코인을 비롯, 많은 블록체인 시스템에서 사용
        
        <aside>
        💡 해시
        -다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 매핑한 값
        해싱 
        -임이의 데이터를 해시로 바꿔주는 일 - 해시 함수가 이를 담당
        해시 함수
        -임의의 데이터를 입력으로 받아 일정한 길이의 데이터로 바꿔주는 함수
        
        </aside>
        
    

---

## SEO에도 도움이 되는 HTTPS

- SEO
    - 검색 엔진 최적화

- 캐노니컬 설정
    - link에 canonical
    
    [캐노니컬 태그 (Canonical tag)로 검색엔진 최적화하기 - 재밌는 그로스해킹](https://growthacking.kr/캐노니컬-태그-canonical-tag로-검색엔진-최적화하기/)
    
- 메타 설정
    - html 파일의 가장 윗부분

- 페이지 속도 개선

- 사이트맵 관리
    - sitemap.xml

- HTTPS 구축 방법
    - CA에서 구매한 인증키를 기반으로 HTTPS서비스 구축
    - 서버 앞단의 HTTPS를 제공하는 로드 밸런서
    - 서버 앞단에 HTTPS를 제공하는 CDN을 두기
    

### 2.5.5 HTTP

- QUIC라는 계층 위에서 돌아감 / UDP 기반

- 초기 연결 설정 시 지연 감소
    - 1 - RTT 소요(첫 연결 설정)
        - 클라이언트가 서버에 어떤 신호를 한 번 주고, 서버도 거기에 응답하기만 하면 바로 본 통신 시작 가능
    - 순방향 오류 수정 메커니즘 적용