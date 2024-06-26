---
title: "IP 주소 정리"
date: 2023-11-19 14:01:40 +0900
categories: [Study, Data Communication Network]
tags: [network]
math: true
---

### **개요**

주소 공간

- 인터넷에 연결된 각 장치 식별자: IP 주소

- IPv4 주소: 32비트 길이

- 주소 공간: $2^{32}$ = 4,294,967,297 (약 43억 개)

- 인터넷 상에서 유일한 식별자로, 두 개 이상의 장치가 같은 주소를 가질 수 없음. (다만 사설 IP의 경우 해당 망 내부에선 공용될 수 없으나 다른 망 내의 사설 IP와 겹칠 수 있음)

- 2/16/점-10진 표기법 사용

<br>

### **클래스 기반 주소 지정**

IP 주소는 클래스(class) 개념을 이용하며, 클래스는 A, B, C, D, E 총 5개로 구분한다. IPv4 주소 체계에서는 32비트를 사용하고, 보통 8비트씩 4개로 묶어서 이야기 한다. 이때 8비트를 **Octet**이라고 부른다.

(image)

클래스에 따라 Netid와 Hostid가 다르다.

(image)

① 클래스 A에 있는 블록

- 1바이트(=8비트) Netid 지정

- 가장 왼쪽 비트가 0이고, 7비트로 나타내는 블록의 수는 $2^7$ = 128. 이는 곧 네트워크를 만들 수 있는 블록의 개수와 같음. (Netid가 0부터 127까지 존재하며 이 숫자는 Octet 1이 나타내는 수. 예컨대 Netid가 0이면 Octet 1이 10진수로 0, 2진수로는 00000000인 것)

- 각 블록에 속한 주소 수 $256^3$ = 16,777,216개
  
  (image)

② 클래스 B에 있는 블록

- 2바이트(=16비트) Netid 지정

- 왼쪽부터 처음 두 비트는 10이고, 14(= 16 - 2)비트로 지정할 수 있는 블록 수는 $2^{14}$ = 16,384

- 각 블록에 속한 주소 수 $256^2$ = 65,536개

③ 클래스 C에 있는 블록

- 3바이트(=24비트)가 Netid 지정

- 처음 세 비트는 110이고, 21(= 24 - 3)비트로 지정할 수 있는 블록 수 $2^{21}$ = 2,097,152

- 각 블록에 속한 주소 수 256개

④ 클래스 D에 있는 단일 블록

- 멀티캐스팅용

- 인터넷 상에서 호스트들의 그룹을 지정하는데 사용

⑤ 클래스 E에 있는 단일 블록

- 나중에 사용하기 위해 예약

<br>

#### **2계층 주소 지정**

네트워크 내의 모든 주소는 한 블록에 속한다. 클래스 기반 주소 지정에서 각 주소는 Netid와 Hostid 부분을 포함하며, Netid는 네트워크를 정의하고 Hostid는 네트워크에 연결된 특정 호스트를 정의한다.

(image)

주소가 주어지면 블록에 대한 정보를 추출할 수 있다. 이때, 블록에서 네트워크의 첫 번째 주소는 네트워크 주소로, 마지막 주소는 브로드캐스트 주소로 이미 할당되어 있어 호스트에게 할당할 수 없다.

블록의 첫 번째 주소는  네트워크 주소이다. 네트워크 주소는 목적지로 패킷을 전송하는데 사용하는 네트워크의 식별자이다. 라우터 입장에서는 네트워크 주소를 알아야 어떤 네트워크로 패킷을 보낼지 결정할 수 있기 때문이다. 임의의 호스트로부터 패킷이 라우터에 도착하면 라우터는 패킷을 어떤 인터페이스로 보내야 하는지 알아야 한다. 목적지 주소로 패킷이 전송되면 라우터는 네트워크 주소를 찾고, 라우터 안에 있는 라우팅 테이블 알고리즘에 따라 네트워크 주소를 인터페이스 번호로 나눈다.

(image)

이러한 네트워크 주소를 찾는 방법 중 하나로 네트워크 마스크가 있다. 디폴트 마스크라고도 부르며, 목적지 주소를 이용하여 네트워크 주소를 찾아낸다. Netid로 쓰는 비트는 1로, Hostid로 쓰는 비트는 0으로 세팅하고 목적지 주소와 AND 연산을 수행하면 네트워크 주소를 찾아낼 수 있다.

(image)

<br>

#### **3계층 주소 지정**

**서브넷팅**(subnetting)은 블록을 작은 블록으로 나누는 개념이다. 즉, 네트워크를 더 작은 네트워크로 쪼개는 것이다. 서브넷팅에서 각 서브네트워크는 자신만의 주소를 가진다.

(image)

위 그림은 서브넷팅한 네트워크를 보여주고 있다. 전체 네트워크는 여전히 같은 네트워크를 통하여 연결되어 있지만, 네트워크를 사설 라우터를 이용하여 4개의 서브네트워크로 나누었다. 각 서브네트워크는 $2^{14}$개의 호스트를 가질 수 있다. 그림에서 /16과 /18은 Netid와 Subnetid의 길이를 나타낸다.

(image)

네트워크를 같은 수의 호스트를 가지는 s개의 서브넷으로 나누면 다음과 같이 각 서브넷의 Subnetid를 구할 수 있다. 이때 n은 Netid의 길이이고 $n_{sub}$는 각 Subnetid의 길이이며 s는 2의 거듭제곱인 서브넷의 개수이다.

$$
n_{sub} = n + log_2s
$$

Netid와 Subnetid를 아는 경우에는 s(서브넷의 개수)를 알 수 있다.

<br>

### **클래스 없는 주소 지정**

사실 클래스 기반 주소 지정에서 서브넷팅은 주소 고갈 문제를 실질적으로 해결하지 못한다. 그에 대한 장기적 해결책으로써 IPv6가 개발되었는데, 여전히 IPv4 주소를 사용하며 각 기관에 대해 주소를 분배하는 방법을 변경하는 단기간 해결책 또한 존재한다. 이것를 클래스 기반이 아닌 주소 지정 방식이라고 부른다.

각 기관은 가변 길이 블록으로 $2^0$, $2^1$, $2^2$, $2^3$, $2^4$, $2^5$, …, $2^{32}$개의 주소를 갖는 블록을 지정할 수 있다. 이러한 경우 Netid와 동일한 기능을 하는 **프리픽스**(prefix)와 Hostid와 동일한 기능을 하는 **서픽스**(suffix)가 있다.

 **CIDR**(Classless Inter-Domain Routing)는 IP 주소의 영역을 여러 네트워크 영역으로 나누기 위해 IP를 묶는 방식이다. 여러 개의 사설망을 구축하기 위해 망을 나누는 방법으로써 사용하기도 한다.

<br>

### **IPv6 주소**

인터넷 상에서의 IPv4 주소 체계의 공간 한계로 인해 등장한 주소 체계이다. 128비트 길이이며 주로 16비트씩 끊어서 표현하는 콜론-16진 표기법을 사용한다.

주소 유형으로는 1:1의 유니캐스트, 1:nearest의 애니캐스트, 1:many의 멀티캐스트가 있다.

<br>

##### ***용어 정리**

공인(공용) IP

- 유동 IP: 고정적으로 IP를 부여하지 않고 장비를 사용할 때 남아 있는 IP 중에서 돌아가면서 부여하는 IP 주소

- 고정 IP: 고정적으로 부여된 IP로 한번 부여되면 IP를 반납하기 전까지는 다른 장비에 부여할 수 없는 IP 주소

사설(로컬/가상) IP: 일반 가정이나 회사 내에 할당된 네트워크의 IP 주소. 서브넷팅된 IP이므로 사설 IP 주소만으로는 인터넷에 직접 연결할 수 없음.

<br>
