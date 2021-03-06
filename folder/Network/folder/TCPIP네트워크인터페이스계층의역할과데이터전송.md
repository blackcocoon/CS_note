# TCP/IP 네트워크 인터페이스 계층의 역할과 데이터 전송(ft. 랜카드와 MAC 주소)

출처 : [쉽게 이해하는 네트워크](https://better-together.tistory.com/101?category=887984)


> 랜카드와 MAC 주소를 중심으로 이해하는 네트워크 인터페이스 계층


- [TCP/IP 네트워크 인터페이스 계층의 역할과 데이터 전송(ft. 랜카드와 MAC 주소)](#tcpip-네트워크-인터페이스-계층의-역할과-데이터-전송ft-랜카드와-mac-주소)
  - [네트워크 인터페이스 계층의 역할](#네트워크-인터페이스-계층의-역할)
  - [네트워크 인터페이스 계층의 핵심 하드웨어 - 랜카드(NIC)](#네트워크-인터페이스-계층의-핵심-하드웨어---랜카드nic)
  - [랜카드와 장치 드라이버](#랜카드와-장치-드라이버)
  - [네트워크 인터페이스 계층과 프로토콜](#네트워크-인터페이스-계층과-프로토콜)
  - [네트워크 인터페이스 계층의 프레임 전송](#네트워크-인터페이스-계층의-프레임-전송)
  - [MAC 주소와 랜카드](#mac-주소와-랜카드)
  - [스위치](#스위치)
  - [MAC 주소에 의한 데이터 전송 과정](#mac-주소에-의한-데이터-전송-과정)
    - [이더넷 프로토콜에 따른 통신](#이더넷-프로토콜에-따른-통신)
    - [무선 LAN 프로토콜에 따른 통신](#무선-lan-프로토콜에-따른-통신)


<br/><br/><br/>

## 네트워크 인터페이스 계층의 역할
앞서 살펴본 것처럼 TCP/IP 모델의 최하층에 위치한 네트워크 인터페이스 계층은 물리적으로 직접 연결된 네트워크 기기 간에 데이터의 전송을 제어하는 역할을 합니다. 즉, 전송 매체로 연결되어 전기 신호나 전파 같은 물리적 신호가 도달하는 범위 내에서 데이터를 제대로 전송하기 위한 규칙을 정한 계층이라고 할 수 있습니다.

네트워크 인터페이스 계층의 역할 자세히 ⇒ [TCP/IP 계층의 특징과 역할](TCPIP계층의특징과역할및프로토콜.md)

네트워크 인터페이스 계층에 속한 물리적인 네트워크 장비, 즉 하드웨어에는 랜카드(NIC), 스위치, 무선 AP 등이 있습니다. 이러한 하드웨어를 랜 케이블 같은 전송 매체로 연결하여 데이터의 물리적 신호 전송이 가능한 유선 LAN이나 무선 LAN과 같은 물리 네트워크를 만듭니다.

 


<br/><br/><br/>

## 네트워크 인터페이스 계층의 핵심 하드웨어 - 랜카드(NIC)
유선이든 무선이든 컴퓨터가 전송 매체와 연결될 수 있는 것은 컴퓨터에 랜카드(NIC)가 장착되어있기 때문입니다. 컴퓨터에 랜카드가 장착되어야 랜 케이블을 연결할 수 있는 랜포트(또는 외부 포트)가 생기고, 랜포트에 랜 케이블을 꽂음으로써 다른 컴퓨터나 네트워크 장비를 연결하는 유선 네트워크를 만들 수 있습니다. 컴퓨터에 무선 랜카드가 장착되어야 무선랜 인터페이스가 생기고, 무선랜 인터페이스와 무선 AP가 연결되는 무선 네트워크를 만들 수 있습니다. 따라서 네트워크에 연결하는 컴퓨터에는 반드시 하나 이상의 랜카드가 있어야 합니다.

또한 네트워크 인터페이스 카드(Network Interface Card, NIC)라고도 불리는 랜카드는 컴퓨터와 네트워크의 물리적 연결 기능뿐만 아니라 컴퓨터가 만든 디지털 데이터를 전기 신호나 전파같은 물리적 신호로 변환하여 네트워크로 내보내거나, 네트워크로부터 받은 물리적 신호를 디지털 데이터로 변환하는 기능을 갖고 있습니다. 즉, 랜카드는 서로 다른 형태의 데이터를 전송하는 컴퓨터와 네트워크 간에 상호작용이 가능하도록 하는 네트워크 인터페이스입니다.

랜카드에 대해 자세히 ⇒ [네트워크의 구성](컴퓨터네트워크의구성요소3가지.md)

이처럼 랜카드는 컴퓨터와 전송 매체를 연결하는 장치로 컴퓨터와 네트워크 사이에서 인터페이스 역할을 하며 프로토콜의 처리를 담당하는 네트워크 인터페이스 계층의 핵심적인 하드웨어입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxY0cQ%2FbtqM5UyVe3q%2FyVtGL2b1oq58IadnEUVESK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 1> 랜카드</b></sup>
</p><br/>



<br/><br/><br/>

## 랜카드와 장치 드라이버
컴퓨터에 랜카드(NIC)를 장착한다고 해서 저절로 작동하지는 않습니다. 물리적 장비인 하드웨어를 그 용도에 맞게 사용하기 위해선 **하드웨어를 관리하고 제어할 수 있는 소프트웨어**가 필요하기 때문입니다.

예를 들어 컴퓨터를 사용해 문서를 작성할 수 있는 것은 컴퓨터에 하드웨어를 제어하는 운영체제(Operating System, OS)라는 시스템 소프트웨어가 설치되고, 그 위에 한글이나 MS 워드 같은 응용 소프트웨어가 설치되었기 때문입니다. 또한, 프린터 같은 주변 기기를 컴퓨터와 연결할 때도 '장치 드라이버(또는 디바이스 드라이버, Device Driver)'라는 소프트웨어를 컴퓨터에 설치해야만 컴퓨터를 통해서 프린터 기능을 사용할 수 있게 됩니다. 운전자(Driver)가 자동차를 제어하듯 컴퓨터 **운영체제(OS)에 설치되는 장치 드라이버**라는 **소프트웨어를 통해 컴퓨터가 장치를 제어할 수 있게 되는 것입니다.**

마찬가지로 컴퓨터 운영체제(OS)에 **랜카드(NIC)를 작동시키기 위한 장치 드라이버가 설치**되어야 컴퓨터가 랜카드를 제어하고 프로토콜을 처리하며 네트워크 인터페이스 계층의 역할을 구현할 수 환경이 만들어집니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb3RzdG%2FbtqM38xTxAT%2Fh0XqVkZLHCLePhkiokj820%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 2> 랜카드와 장치 드라이버</b></sup>
</p><br/>


아마 프린터 장치 드라이버를 설치해 본 적은 있어도 랜카드 장치 드라이버를 설치해본 적은 없는 경우가 대부분일 것입니다. 그건 대부분의 컴퓨터에 플러그 앤 플레이(Plug and Play)기능이 있어 컴퓨터에 기기를 연결하면 자동으로 그 기기를 이용할 수 있게 설정되어 있기 때문입니다. 즉, 운영체제(OS)에 처음부터 자주 사용되는 표준적인 기기들을 제어할 수 있는 장치 드라이버가 내장되어 있습니다. 랜카드(NIC) 장치 드라이버가 대표적이고, 자주 사용하는 USB 장치 드라이버도 마찬가지로 대부분의 컴퓨터에 내장되어 있습니다.

 


<br/><br/><br/>

## 네트워크 인터페이스 계층과 프로토콜
TCP/IP에서는 네트워크의 하드웨어적인 연결에 대해 특정 프로토콜을 규정하지 않고 모든 표준 규격과 기술적인 프로토콜을 지원하지만, 이더넷(IEEE 802.3*) 프로토콜과 무선 LAN(IEEE 802.11**) 프로토콜이 사실상의 표준으로 사용되고 있습니다. 랜 케이블을 따라 전기 신호로 데이터를 전송하는 유선 LAN은 이더넷 프로토콜을, 공기 중에서 전파로 데이터를 전송하는 무선 LAN은 무선 LAN 프로토콜에 따라 데이터를 전송합니다.

*. IEEE 802.3은 LAN(근거리 통신망)을 구축하기 위해 개발한 이더넷(Ethernet)이라는 네트워크 통신 기술을 IEEE가 표준화한 규약을 의미합니다. 이 규약이 정한 케이블과 외부 포트의 사양에 따라 만들어진 것이 랜 케이블(또는 이더넷 케이블), 랜 포트(또는 이더넷 포트)입니다.

**. IEEE 802.11는 IEEE가 무선 랜 기술을 표준화한 규약을 의미합니다. 이 표준 규약을 기반으로 무선 AP가 설치된 곳의 일정 거리 안에서 무선 인터넷에 접속할 수 있는 기술 또는 이 기술에 따라 만들어진 제품들의 브랜드명을 와이파이(Wi-Fi)라고 합니다. 참고로 와이파이라는 이름은 무선(Wireless)방식으로 유선랜과 같이 뛰어난 품질(Fidelity)을 제공한다는 뜻의 'Wireless Fidelity'에서 나왔습니다. 무선 LAN, IEEE 802.11, 와이파이는 사실상 동의어로 사용되고 있습니다.

<참고> IEEE(Institute of Electrical and Electronics Engineers, 미국 전기전자학회)

IEEE는 I-Triple-E(아이 트리플 이)라고 발음하며 전기전자공학에 관한 기술의 표준화를 추진하는 비영리 단체입니다. 미국뿐만 아니라 전 세계 각국의 학자와 전문 기술자들이 가입하고 있는 전문가 단체로서 산하에 있는 하부 기술 위원회를 통하여 주요 활동이 이루어집니다. LAN의 접속 방법 및 프로토콜의 표준화 작업을 추진하기 위해 만든 하부 기술 위원회가 IEEE 802 위원회입니다. '802'라는 숫자는 1980년 2월에 LAN 표준화 프로젝트가 시작되었다는 데에서 유래합니다. IEEE 802 위원회가 만든 표준은 IEEE 802.1, 802.2와 같이 IEEE 802에 번호가 붙는 IEEE 802 시리즈로 발표됩니다. IEEE 802 시리즈 중 이더넷에 대한 표준이 IEEE 802.3이고, 무선 LAN에 대한 표준이 IEEE 802.11입니다.

 


<br/><br/><br/>

## 네트워크 인터페이스 계층의 프레임 전송
네트워크에 데이터를 전송하기 위해 연결된 물리적인 기기를 노드(Node)라고 합니다. 우리 집에서 우편물을 주고받기 위해 다른 집과 우리 집을 구별할 수 있는 주소가 필요한 것처럼 데이터를 주고받는 노드도 다른 노드와 구별할 수 있는 주소가 있어야 합니다. 따라서 노드를 보다 정확히 표현하면 네트워크에 연결된 주소가 있는 물리적인 기기를 의미합니다.

노드에 대해 자세히 ⇒ [<개발자의 단어> 노드, 호스트, 서버와 클라이언트의 구별](https://better-together.tistory.com/74?category=887984)

물리적으로 직접 연결된 기기 간에 데이터 전송을 제어하는 네트워크 인터페이스 계층의 역할을 다른 말로 표현하면 같은 네트워크에 연결된 노드와 노드 간의 데이터 전송을 제어하는 것이라고 할 수 있습니다. 따라서 네트워크 인터페이스 계층의 프로토콜은 인접한 노드 간에 데이터가 제대로 전송될 수 있도록 전송을 제어하고, 전송 도중에 발생한 오류를 교정하는 일 등을 규정합니다.

데이터의 전송을 제어한다는 것은 ① **데이터를 순차적으로 전송하기 위해 데이터에 번호를 부여**하여 데이터 전송의 순서를 제어하며, ② **수신지가 감당할 수 있을 정도의 전송 속도를 유지하기 위해 한 번에 전송하는 데이터 양을 조절하고 데이터를 전송할 때 수신 여부를 확인하는 기능을 수행**하여 데이터의 흐름을 제어하는 것을 의미합니다.

네트워크 인터페이스 계층에서는 인접한 노드 중에서 데이터 수신지를 식별하기 위해 노드마다 갖고 있는 주소를 사용합니다. 송신지 노드(또는 송신 호스트)에서는 이 주소를 포함하여 데이터 전송을 제어하는데 필요한 여러 정보를 헤더에 추가해서 **프레임**이라는 데이터 단위를 만들어 네트워크로 전송합니다(보다 구체적으로는 프레임을 전기 신호로 변환하여 랜 케이블로 전송합니다). 네트워크에서 이 프레임을 받은 최종 수신지 노드(또는 수신 호스트)에서는 헤더의 정보를 읽고 프로토콜에 따라 데이터를 처리한 후 헤더를 제거한 데이터를 인터넷 계층으로 넘깁니다.

*. **프레임**은 인터넷 계층에서 받은 데이터(IP 패킷)와 데이터 앞에 추가하는 헤더, 데이터 뒤에 추가하는 **트레일러**(Trailer)로 구성되어 있습니다. 모든 계층에서 추가되는 헤더와 달리 **트레일러**는 **네트워크 인터페이스 계층에서만 추가되는 정보**입니다. **FCS**(Frame Check Sequence)라고도 하는 트레일러는 **데이터 송신 도중에 오류가 발생하는지 확인하는 용도로 사용**됩니다.

프레임 전송 과정에 대해 자세히 ⇒ [TCP/IP에서의 데이터 통신](인터넷의TCPIP데이터전송과정.md)

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FM3kRi%2FbtqNgsV8Ish%2FWZFznRHJ7fcrX2TRQUoSR0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 3> 네트워크 인터페이스 계층의 프레임 전송</b></sup>
</p><br/>

**LAN의 표준화 규칙**인 이더넷 프로토콜과 무선 LAN 프로토콜은 **노드를 식별하기 위한 주소로 MAC 주소를 사용**하여 전송 매체를 통해 프레임을 전송합니다. Media Access Control Address를 의미하는 MAC 주소는 이름처럼 **전송 매체(Media)에 대한 접근(Access)을 제어(Control)하는 주소**, 즉 **전송 매체와 연결된 노드 중에 데이터의 수신지 노드를 식별하여 접근할 수 있게 하는 주소**입니다.

 



<br/><br/><br/>

## MAC 주소와 랜카드
컴퓨터를 네트워크에 연결하기 위해 반드시 필요하고, 네트워크 인터페이스 계층에서 핵심적인 역할을 담당하는 장치가 랜카드라고 했습니다. 이더넷 규격에 따라 만들어지는 각 랜카드에는 사람의 주민등록번호처럼 고유한 식별 번호가 할당됩니다. 이렇게 랜카드에 할당된 식별 번호가 바로 MAC 주소(Media Access Control Address)입니다.

랜카드를 제조하는 제조업체(또는 벤더, Vendor)가 제조 단계에서 랜카드에 붙이는 MAC 주소는 전 세계에서 유일한 번호로 할당됩니다. MAC 주소는 기본적으로 주민등록번호처럼 **한 번 만들면 변경할 수 없는 주소**이기에 **'물리 주소'나 '하드웨어 주소'**라고 불리기도 합니다.

*. **MAC 주소**는 ① 랜카드를 제조한 업체를 식별하는 번호인 **벤더 코드**(Organizationally Unique Identifier, OUI)와 ②제조한 업체가 **제품에 붙이는 일련번호**로 구성되어 전 세계에서 동일한 MAC 주소로 설정된 랜카드 제품은 하나밖에 없다는 것을 보증합니다. 그러나 MAC 주소가 반드시 세계에서 유일한 값이라고는 할 수 없습니다. 1대의 컴퓨터에서 여러 개의 OS를 동시에 작동시키는 '가상 머신'이라는 기술에서는 물리적인 인터페이스가 없기 때문에 소프트웨어적으로 MAC 주소를 만들어 가상 머신의 각종 인터페이스에 할당하여 사용하기 때문입니다.

랜카드뿐만 아니라 **네트워크 인터페이스의 역할**을 하는 **무선 AP**(서로 다른 유선 네트워크와 무선 네트워크를 연결하는 인터페이스), **라우터**(서로 다른 네트워크와 네트워크를 연결하는 인터페이스)도 제조 과정에서 **고유한 MAC 주소를 할당받습니다.** MAC 주소는 네트워크 인터페이스마다 할당된 번호이기 때문에 여러 개의 네트워크 인터페이스를 갖는 네트워크 장비에는 여러 개의 MAC 주소가 할당될 수도 있습니다.

 


<br/><br/><br/>

## 스위치
여러 대의 컴퓨터를 연결하여 LAN이라는 소규모 네트워크를 만들 때 스위치라는 네트워크 장비가 사용됩니다.

스위치 자세히 ⇒ [네트워크의 구성](컴퓨터네트워크의구성요소3가지.md)

랜포트가 여러 개인 스위치를 중간에 두고 스위치와 여러 대의 컴퓨터를 랜 케이블로 연결하여 스위치를 거쳐 여러 대의 컴퓨터가 동시에 통신이 가능한 소규모 네트워크를 구축합니다. 스위치가 두 대의 컴퓨터를 연결하는 랜 케이블을 분할하고 여러 대의 컴퓨터가 공유할 수 있게 하는 역할을 하는 것입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtZaal%2FbtqM2HURM8J%2F3o8F6dTC6zABT5BerfFbj1%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 4> 스위치의 역할</b></sup>
</p><br/>

이렇게 스위치는 여러 개의 랜포트를 통해 **네트워크 인터페이스를 확장하는 역할**을 하지만 **서로 다른 기기나 네트워크가 상호 작용하도록 돕는 인터페이스는 아닙니다.** 따라서 **스위치에는 네트워크 인터페이스에만 할당되는 MAC 주소를 갖고 있지 않습니다.** 이런 면에서 스위치는 네트워크 인터페이스로서 고유한 MAC 주소가 할당되어 송신지 호스트와 수신지 호스트 사이에서 중간 노드 역할을 하는 무선 AP나 라우터와는 차이가 있습니다.

**스위치는 자신의 포트에 연결되어 있는 컴퓨터의 MAC 주소를 학습하고 기억하는 기능이 있습니다.** 이 기능을 통해 스위치로 **전송되는 데이터를 제어하고 올바른 수신지로 데이터를 전달**합니다.

스위치가 **포트 번호와 그 포트에 연결되어 있는 컴퓨터의 MAC주소를 기억**하기 위해 만드는 데이터베이스를 **MAC 주소 테이블**이라고 합니다. 초기화된 스위치의 전원을 켠 상태에서는 MAC 주소 테이블에 아무것도 기록되어 있지 않지만, **스위치에 프레임이 수신될 때마다 학습 로직에 따라 MAC 주소와 포트 번호에 관한 정보를 수집하여 MAC 주소 테이블을 갱신**합니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIe6vr%2FbtqM5UZ5Qqj%2FQVEQMdRUtVFX0SnIsvQoj1%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 5> 스위치와 MAC 주소 테이블</b></sup>
</p><br/> 




<br/><br/><br/>

## MAC 주소에 의한 데이터 전송 과정

<br/>

### 이더넷 프로토콜에 따른 통신
이더넷 프로토콜을 따르는 네트워크 인터페이스 계층에서는 MAC 주소로 수신지를 식별합니다. 따라서 상위 계층(인터넷 계층)으로부터 데이터(IP 패킷)를 넘겨받은 송신지 네트워크 인터페이스 계층은 수신지 MAC 주소와 송신지 MAC 주소를 담은 이더넷 헤더를 데이터에 추가한 이더넷 프레임을 만들어 네트워크로 내보냅니다.

*. 통신은 보통 데이터를 주고받는 양방향으로 이루어지기 때문에 데이터를 전송할 때는 일반적으로 수신지 주소와 함께 송신지 주소를 알려줍니다.
 
<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FerjcrB%2FbtqM4za3p1N%2Ftm4ulkmUQRodbB8KfRx5kK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 6> 이더넷과 MAC 주소에 의한 데이터 전송 과정</b></sup>
</p><br/> 

네트워크에서 이더넷 프레임은 랜 케이블을 거쳐 스위치에 도착합니다. 이더넷 프레임을 수신한 스위치는 이더넷 프레임의 수신지 MAC 주소를 보고, MAC 주소 테이블을 확인하여 수신지 MAC 주소가 있는 포트로 이더넷 프레임을 전송합니다. 위 <그림 6>에서 스위치의 ①번 포트와 연결된 송신지 컴퓨터에서 보낸 프레임을 받은 스위치는 이더넷 헤더의 수신지 MAC 주소를 읽고 MAC 주소 테이블을 확인하여 ④번 포트로 이더넷 프레임을 전송합니다.

만약 MAC 주소 테이블에 송신지(수신지아님?) MAC 주소가 등록되어 있지 않으면 송신 포트인 ①번 포트 외에 아직 MAC 주소가 등록되지 않은 나머지 포트에 프레임이 전송되는데, 이러한 프레임 전송을 **플러딩**(Flooding)이라고 합니다.

스위치로부터 랜 케이블을 거쳐 이더넷 프레임을 받은 수신지 네트워크 인터페이스 계층은 이더넷 헤더에서 수신지 MAC 주소를 읽고 자신의 MAC 주소와 일치하는지 비교하여 자신에게 온 데이터가 맞는지를 확인합니다. 자신에게 온 데이터가 맞으면 이더넷 프레임에서 이더넷 헤더를 삭제한 데이터(IP 패킷)를 상위 계층(인터넷 계층)으로 넘깁니다. 만약 자신에게 온 데이터가 아니면 프레임을 폐기합니다.

이렇게 스위치가 **MAC 주소를 기준으로 수신지를 선택하는 것**을 **MAC 주소 필터링**이라고 합니다.




<br/><br/>

### 무선 LAN 프로토콜에 따른 통신
무선 LAN 프로토콜에 따라 통신을 할 경우에는 송신지와 수신지 사이를 **무선 AP**가 중계하게 됩니다. 따라서 프레임에는 **송신지와 수신지의 MAC 주소 외에 무선 AP의 MAC 주소에 대한 정보가 헤더에 추가됩니다.**

무선 AP에 대해 자세히 ⇒ [네트워크의 구성](컴퓨터네트워크의구성요소3가지.md)

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdQLXXn%2FbtqM2HtUcj7%2F4sFtfZAwfz80IK6RqXnGG0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 7> 무선 LAN과 MAC 주소에 의한 데이터 전송</b></sup>
</p><br/>