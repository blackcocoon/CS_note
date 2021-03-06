# IP 주소 의미와 체계 및 서브넷 마스크

출처 : [쉽게 이해하는 네트워크](https://better-together.tistory.com/118?category=887984)

> IPv4 IP주소의 의미와 서브넷 마스크의 이해


<br/>

- [IP 주소 의미와 체계 및 서브넷 마스크](#ip-주소-의미와-체계-및-서브넷-마스크)
  - [IP 주소](#ip-주소)
  - [IPv4란?](#ipv4란)
    - [IP 주소의 구성 - 네트워크 부와 호스트 부](#ip-주소의-구성---네트워크-부와-호스트-부)
    - [IP 주소의 클래스](#ip-주소의-클래스)
      - [① 클래스 A](#-클래스-a)
      - [② 클래스 B](#-클래스-b)
      - [③ 클래스 C](#-클래스-c)
    - [특수 목적을 위한 IP 주소 - 네트워크 주소와 브로드캐스트 주소](#특수-목적을-위한-ip-주소---네트워크-주소와-브로드캐스트-주소)
      - [네트워크 주소](#네트워크-주소)
      - [브로드캐스트 주소](#브로드캐스트-주소)
  - [서브넷팅과 서브넷](#서브넷팅과-서브넷)
    - [서브넷 마스크](#서브넷-마스크)
      - [서브넷 마스크 표기법](#서브넷-마스크-표기법)
        - [① 십진수 표기법](#-십진수-표기법)
        - [② 프리픽스 표기법](#-프리픽스-표기법)
      - [서브넷 마스크의 유용성](#서브넷-마스크의-유용성)




<br/><br/><br/>

## IP 주소

인터넷 계층의 IP 프로토콜은 IP 주소를 사용하여 호스트나 네트워크 장비를 식별합니다. 인터넷에 접속한 컴퓨터와 라우터에 고유한 IP 주소를 할당하고, 그 IP 주소를 사용해서 컴퓨터를 특정하거나 통신 상대방으로 지정합니다.

따라서 인터넷에 연결된 모든 컴퓨터나 라우터의 IP 주소는 유일해야 합니다. 그래서 IP 주소는 전 세계에서 유일하게 할당되어야 하므로 전 세계 인터넷 주소를 관리하는 인터넷할당번호관리기관*(IANA, Internet Assigned Numbers Authority)에서 통합 관리하고 있습니다.

*. 현재 인터넷할당번호관리기관은 ICANN(아이칸, Internet Corporation for Assigned Names and Numbers, 국제인터넷주소관리기구)입니다. 1998년에 설립된 ICANN은 전 세계 IP 주소와 도메인명을 관리하고 있습니다. ICANN에서는 전 세계 인터넷 주소의 구조를 정하고 아시아태평양 지역의 네트워크 정보센터(APNIC, Asia Pacific NIC)와 같은 각 지역별 네트워크정보센터(NIC, Network Information Center)에 세부 주소 할당 방안을 위임합니다. 지역별 네트워크정보센터는 각 국가별 네트워크정보센터들로 구성되어 있습니다. 우리나라는 한국인터넷정보센터(KRNIC, Korea NIC)가 IP 주소를 할당하고 관리하고 있습니다.

IP 프로토콜에서는 현재 IPv4(Internet Protocol version 4)의 주소 체계를 사용하고 있습니다. 하지만 스마트폰의 등장 및 모든 사물이 인터넷으로 연결되는 사물 인터넷으로 인해 IP 주소를 사용하는 기기가 폭발적으로 증가하면서 IPv4보다 월등히 많은 수의 IP 주소를 할당할 수 있는 IPv6(Internet Protocol version 6)가 사용되기 시작했고, 향후 모든 IP 주소는 IPv6로 대체될 것이라 보고 있습니다. 보통 IP 주소라 하면 IPv4를 의미합니다. 

이번 포스팅에서는 현재 일반적으로 사용되고 있는 IPv4에 대해 살펴보도록 하겠습니다.




<br/><br/><br/>

## IPv4란?

IPv4의 IP 주소는 32비트(bit), 즉 0 또는 1로 만으로 표기하는 이진(Binary)수 32자리로 구성되어 있습니다.

*. 0 또는 1을 나타내는 정보의 최소 단위를 비트라고 합니다.

이진수로 표기된 IP 주소는 사람이 알아보기 어렵기 때문에  <그림 1>과 같이 전체 32비트를 8비트씩 4그룹으로 나누어, 각 그룹을 십진수로 변환하고, 그룹의 경계에 '. (닷, 점)'을 넣은 형식(Dotted-decimal notation)으로 표기하고 있습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNOThw%2FbtqNSzHds9i%2FFVtfql90mhCuOHNAc81NbK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 1> IPv4 주소 표기</b></sup>
</p><br/>

8비트를 십진수로 변환하면 0~255 사이의 값을 갖기 때문에 IPv4에서는 256 이상의 값을 갖는 IP 주소는 존재하지 않습니다.

IPv4로 할당할 수 있는 IP 주소의 개수는 2의 32승인 약 43억 개입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdJld9B%2FbtqNQxKcSkL%2FEw0d9UkC1M5zLpqwkSpap0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 2> IPv4 주소의 범위</b></sup>
</p><br/>

참고로 IPv6는 128비트로 구성되어 2의 128승, 약 340간(약 340조 X 1조 X 1조) 개의 IP 주소를 사용할 수 있습니다.




<br/><br/>

### IP 주소의 구성 - 네트워크 부와 호스트 부

IP 주소는 어느 네트워크의 어느 호스트라는 것을 식별하는 주소입니다. 따라서 IP 주소는 호스트가 속한 네트워크 주소인 네트워크 부(Network Part 또는 Network ID)와 호스트의 주소인 호스트 부 (Host Part 또는 Host ID)로 구성됩니다. 즉, 네트워크 부는 어떤 네트워크 인지를 나타내 다른 네트워크와 구분하는 역할을 하고, 호스트 부는 해당 네트워크의 어느 호스트인지를 나타내 다른 호스트와 구분하는 역할을 합니다. 여기서 호스트는 컴퓨터뿐만이 아니라 IP 주소가 할당되는 라우터를 포함합니다.

네트워크 부는 인터넷에 접속되어 있는 모든 네트워크 중에서, 호스트 부는 그 호스트가 속한 네트워크 내에서 유일한 번호를 할당하여 인터넷 전체에서 동일한 IP 주소를 갖는 호스트는 1대밖에 없도록 설정합니다.

따라서 같은 네트워크 안에 있는 컴퓨터, 즉 라우터 없이도 데이터 전송이 가능한 컴퓨터는 네트워크 부가 동일하고 호스트 부만 다릅니다. 달리 말하면 네트워크 부가 다르다는 것은 서로 다른 네트워크라는 의미이고, 라우터를 통하지 않고는 통신이 불가능하다는 뜻입니다. 서로 다른 네트워크가 라우터를 통해 통신이 가능한 것은 라우터가 IP 주소의 네트워크 부를 보고 라우팅을 하여 데이터를 전송하기 때문입니다.

인터넷에 접속 가능한 네트워크를 만들기 위해 IP 주소 할당 기관(NIC)에 IP 주소 할당을 신청하면 할당 기관에서는 네트워크 부까지만 할당합니다. 네트워크 부를 할당받으면 네트워크를 만드는 사람(네트워크 관리자)이 호스트 부를 결정하여 네트워크 부와 호스트 부를 합친 IP 주소를 개별 호스트에 설정하는 것입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB82mo%2FbtqNNi76sb9%2FiSw0UPN9LQloCd1lxeNR2k%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 3> 네트워크부와 호스트부</b></sup>
</p><br/>

IPv4의 주소에서는 어디까지가 네트워크 부이고, 어디까지가 호스트 부일까요? 다시 말해 <그림 1>의 IP 주소 203.179.33.13에서 어디까지가 네트워크 부이고, 어디까지가 호스트 부일까요? 네트워크 부와 호스트 부를 어떻게 식별할까요?

IPv4 도입 초기에는 클래스(class)를 기준으로 네트워크부와 호스트를 나누는 방식을 사용했지만, 클래스 방식의 비효율성으로 인해 현재는 클래스에 구애받지 않고 서브넷 마스크(subnet mask) 방식을 사용하고 있습니다.



<br/><br/>

### IP 주소의 클래스

클래스 기준은 IP 주소를 앞에서 8비트씩 나눈 그룹을 조합하여 네트워크 부와 호스트 부를 정한 것입니다. 즉, 클래스에 따라 어디까지가 네트워크 부이고, 어디까지가 호스트 부인지가 결정됩니다.


<br/>

#### ① 클래스 A

클래스 A는 IP 주소 32비트 중 앞 8비트를 네트워크 부로, 다음 24비트를 호스트 부로 나눈 것입니다. 네트워크 부의 첫 비트는 클래스 A 식별 비트인 '0'이 할당되기 때문에 00000000 ~ 01111111의 번호가 네트워크 부로 사용됩니다. 이를 십진수로 표기하면 클래스 A의 네트워크 부는 0 ~ 127의 번호가 할당됩니다.

다음 24비트는 호스트 부로 사용되고, 한 네트워크 안에서 할당할 수 있는 호스트 번호는 0.0.0 ~ 255.255.255까지 16,777,214개*입니다. 말하자면 IP 주소 관리기관이 IP 주소 신청자에게 클래스 A의 네트워크 부 1개를 할당하면, 신청자는 약 1,677만 개의 호스트 부를 마음대로 정할 수 있게 되는 것입니다. 1개의 네트워크에 약 1,677만 개의 호스트를 연결할 수 있기 때문에 클래스 A는 주로 대규모의 네트워크를 구축하는 기관에 할당됩니다.

*. 호스트 부의 모든 비트가 0과 1인 번호는 특수 목적(네트워크 주소와 브로드캐스트 주소)으로 사용하기 때문에 IP 주소의 호스트 부를 할당하는 경우에는 이 두 번호를 제외합니다. 따라서 클래스 A의 호스트 부에서는 2의 24승인 16,777,216에서 2를 뺀 16,777,214개의 번호를 호스트 부에 할당할 수 있습니다.

네트워크 부와 호스트 부를 조합해 클래스 A에서 할당 가능한 IP 주소의 범위는 0.0.0.0 ~ 127.255.255.255이고, 이는 2,147,483,648(2의 31승) 개로 전체 IP 주소의 개수 중 약 50%에 해당합니다.


<br/> 

#### ② 클래스 B

클래스 B는 IP 주소 32비트 중 앞 16비트를 네트워크 부로, 다음 16비트를 호스트 부로 나눈 것입니다. 네트워크 부의 맨 앞 2비트는 클래스 B의 식별 비트인 '10'으로 할당되기 때문에 10000000 ~ 10111111의 번호가 네트워크 부의 첫 8비트로 사용됩니다. 네트워크 부 16비트를 십진수로 표기하면 클래스 B의 네트워크 부는 128.0 ~ 191.255 번호가 할당됩니다.

다음 16비트는 호스트 부로 할당되고, 한 네트워크 안에서 할당할 수 있는 호스트 주소는 65,534(2의 16승 - 2) 개입니다.

네트워크 부와 호스트 부를 조합해 클래스 B에서 할당 가능한 IP 주소의 범위는 128.0.0.0 ~ 191.255.255.255이고, 이는 1,073,741,824(2의 30승) 개로 전체 IP 주소의 개수 중 약 25%에 해당합니다.


<br/> 

#### ③ 클래스 C

클래스 C는 IP 주소 32비트 중 앞 24비트를 네트워크 부로, 다음 8비트를 호스트 부로 나눈 것입니다. 네트워크 부의 맨 앞 3비트는 클래스 C의 식별 비트인 '110'으로 할당되기 때문에 11000000 ~ 11011111의 번호가 네트워크 부의 첫 8비트로 사용됩니다. 네트워크 부 24비트를 십진수로 표기하면 클래스 C의 네트워크 부는 192.0.0 ~ 223.255.255 번호가 할당됩니다.

다음 8비트는 호스트 부로 할당되고, 한 네트워크 안에서 할당할 수 있는 호스트 주소는 254(2의 8승 -2) 개입니다.

네트워크 부와 호스트 부를 조합해 클래스 C에서 할당 가능한 IP 주소는 192.0.0.0 ~ 223.255.255.255입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fy8x2n%2FbtqNQwYPRvr%2FDZcDOzjEiCd6hwRfJBkHFK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 4> IP 주소의 클래스</b></sup>
</p><br/>

클래스의 식별 비트로 인해 IP 주소의 첫 8비트를 십진수로 표기한 값의 범위가 클래스 A는 0~127, 클래스 B는 128~191, 클래스 C는 192~223로 구분됩니다. 따라서 첫 8비트의 값으로 클래스를 구분하고, 그에 따라 네트워크 부와 호스트 부를 식별할 수 있습니다.

클래스 기준에 따르면 IP 주소 203.179.33.13는 첫 8비트의 십진수 값이 203이므로 클래스 C에 속합니다. 따라서 203.179.33이 네트워크 부, 13이 호스트부가 됩니다.

아래 <그림 5>와 같이 동일한 네트워크 부 203.179.33을 갖고 있는 호스트들은 같은 네트워크 1에 속해 라우터를 통하지 않고 통신이 가능합니다. 반면, 다른 네트워크 2에 속한 호스트들은 네트워크 1과 다른 네트워크부를 갖고, 라우터를 통하지 않고서는 네트워크 1에 속한 호스트와 통신할 수 없는 것입니다.

네트워크 2에 속한 IP 주소가 192.168.24.4인 컴퓨터가 네트워크 1에 속한 IP 주소 203.179.33.13인 컴퓨터로 IP 패킷을 전송하면, 라우터 2가 수신지 IP 주소의 네트워크 부(203.179.33)를 보고 전송할 라우터를 찾아 IP 패킷을 전송합니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblHMO1%2FbtqNQ39YEXD%2FTrcSak3LXkhXyDIK4lRju1%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 5> 네트워크부와 호스트부의 의미</b></sup>
</p><br/>


<br/>

### 특수 목적을 위한 IP 주소 - 네트워크 주소와 브로드캐스트 주소

위 <그림 5>의 네트워크 1의 호스트나 라우터는 203.179.33.0이나 203.179.33.255의 IP 주소를 사용할 수 없습니다. 마찬가지로 네트워크 2의 호스트나 라우터도 192.168.24.0이나 192.168.24.255의 IP 주소를 사용할 수 없습니다. 다시 말해 클래스 C인 경우 호스트 부 8비트가 모두 0, 즉 십진수로 0인 번호와 호스트 부 8비트가 모두 1, 즉 10진수로 255인 번호는 컴퓨터나 라우터가 자신의 IP 주소로 사용할 수 없습니다.

클래스를 불문하고 IP 주소 중 호스트 부의 모든 비트가 0인 번호는 네트워크 주소로, 모든 비트가 1인 번호는 브로드캐스트 주소라는 특수 목적으로 사용하기 때문에 호스트와 라우터에는 할당하지 않습니다.

#### 네트워크 주소
네트워크 주소는 전체 네트워크에서 작은 네트워크를 식별할 때 사용되고, 호스트 부가 십진수로 0이면 그 네트워크를 대표하는 주소가 됩니다. 위 <그림 5>에서 IP 주소가 203.179.33.1 ~ 203.179.33.13 인 컴퓨터와 라우터는 203.179.33.0(네트워크 주소)의 네트워크(네트워크 1)에 있고, IP 주소가 192.168.24.1 ~ 192.168.24.3인 컴퓨터와 라우터는 192.168.24.0의 네트워크(네트워크 2)에 있는 것이라 할 수 있습니다.


#### 브로드캐스트 주소
브로드캐스트 주소는 하나의 네트워크에 있는 모든 호스트에 동시에 데이터를 보낼 때 사용되는 전용 IP 주소를 의미합니다. 즉, 전체 네트워크에 데이터를 전송할 때는 호스트 부에 255를 설정하면 됩니다. 만약 IP 주소 203.179.33.13인 호스트가 IP 주소 192.168.24.255로 데이터를 전송하면 192.168.24.0의 네트워크에 있는 모든 호스트가 데이터를 수신합니다.






<br/><br/><br/>

## 서브넷팅과 서브넷

클래스 기반 주소 지정 방식에서는 클래스가 정해지면 네트워크 부와 호스트 부의 길이 및 하나의 네트워크 당 사용 가능한 IP 주소가 정해집니다.

클래스 A를 사용할 경우 한 개의 네트워크 당 약 1,677만 대의 호스트를 연결할 수 있고 클래스 B를 사용할 경우 한 개의 네트워크 당 약 6만 5천대의 호스트를 연결할 수 있습니다. 하지만 실제로 이렇게 **많은 호스트를 하나의 네트워크에 연결하는 경우는 거의 없기 때문에 전체 IP 주소의 75%를 차지하는 클래스 A와 클래스 B에서 많은 수의 IP 주소가 사용되지 않고 낭비됩니다.**

IP 주소를 효율적으로 활용하기 위해서 클래스 A와 B 같은 **대규모 네트워크를 좀 더 작은 네트워크로 분할하는 것**을 **서브넷팅**(Subnetting)이라 하고, **분할된 네트워크**를 **서브넷**(Subnet)이라고 합니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLDjgW%2FbtqNU2Cuug8%2F02uFH1sdsBsygX5K8oWUT0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 6> 클래스 A 서브넷팅 전후</b></sup>
</p><br/>

위 <그림 6>는 네트워크 부가 0인 클래스 A의 네트워크 1개를 서브 넷팅 하여 256개의 작은 네트워크로 분할한 것입니다. 호스트 부의 비트를 서브넷 부로 변경하여 서브넷으로 만듭니다. 서브 넷팅을 하면 네트워크 부와 호스트 부로 구성되었던 클래스가 네트워크 부, 서브넷 부, 호스트 부로 변경됩니다.

<그림 6>에서는 호스트 부의 8비트를 서브넷 부로 변경하여 256(2의 8승) 개의 서브넷을 만들었습니다.

<그림 6>은 아래 <그림 7>으로 표현할 수 있습니다. 약 1,667만 대의 컴퓨터를 연결할 수 있던 하나의 네트워크를 256개의 서브넷으로 분할하여 하나의 서브넷에 약 6만 5천 대의 컴퓨터를 연결할 수 있게 만든 것입니다.

**서브넷팅**이라는 **논리적인 방법으로 분할된 네트워크**는 **라우터에 의해 물리적으로 구별됩니다.**

**서브넷팅 전에는 라우터 없이 약 1,667만 대의 컴퓨터 간에 통신이 가능했지만, 서브넷팅 후에는 서브넷이 서로 통신을 하기 위해선 라우터가 필요합니다.**

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FF4v9U%2FbtqNQ3B9RZe%2FwrekukTJGap7CaLED5Q8qK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 7> 클래스 A 서브넷팅</b></sup>
</p><br/>

이처럼 서브넷팅을 통해 호스트 부가 서브넷 부로 변경되면서 **네트워크 부가 확장됩니다.** 따라서 클래스 A의 IP 주소를 서브 넷팅하면 네트워크 부가 변경되는데 IP 주소만으로는 변경된 네트워크 부가 어디까지인지 알 수가 없습니다. 아래 <그림 8>과 같이 서브넷팅을 한다고 해서 IP 주소가 변경되지 않기 때문입니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNra50%2FbtqNVBdAkta%2Fvg6xAckyibp9o9MwnSxnGk%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 8> 클래스 A 서브넷팅 전후 IP 주소</b></sup>
</p><br/>

IP 주소만으로 네트워크 부와 호스트 부의 경계를 알 수 있도록 만든 클래스가 서브넷팅으로 인해 그 의미를 잃게 된 것입니다.

따라서 IP 주소를 서브넷팅하는 경우 IP 주소와 별도로 어디까지가 네트워크 부이고 어디까지가 호스트 부인지 구별할 수 있는 식별자가 필요한데, 이 식별자를 **서브넷 마스크**라고 합니다.

 
<br/><br/>

### 서브넷 마스크

서브넷 마스크는 **IP 주소의 네트워크 부와 호스트 부의 경계를 식별하기 위해 만든 숫자**입니다. 서브넷 마스크는 IP 주소의 32비트에 대응한 32비트로 구성되어 있습니다. 즉, 서브넷 마스크는 IP 주소처럼 32개의 0 또는 1로 구성된 값입니다.

IP 주소의 비트가 **네트워크 부**이면 이 비트에 대응하는 **서브넷 마스크의 비트는 1**이 되고, IP 주소의 비트가 **호스트 부**이면 **서브넷 마스크의 비트는 0**이 됩니다. 이러한 방법으로 클래스에 구애받지 않고 IP 주소의 네트워크부를 식별할 수 있습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhZD1c%2FbtqNQbm9E11%2Fi3A3mZj3px0rYm1DedeAj0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 9> IP 주소와 서브넷 마스크</b></sup>
</p><br/>



<br/>

#### 서브넷 마스크 표기법

<br/>

##### ① 십진수 표기법

32비트로 표현된 서브넷 마스크도 IP 주소와 마찬가지로 보기 쉽게 전체 32비트를 8비트씩 4그룹으로 나누어, 각 그룹을 십진수로 변환하고, 그룹의 경계에 '. (닷, 점)'을 넣은 방법으로 표기하고 있습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbh762H%2FbtqNRI5EK9R%2FKCrxAYpRDFkLphQmZtCRHK%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 10> 서브넷 마스크의 표기</b></sup>
</p><br/>


##### ② 프리픽스 표기법

서브넷 마스크를 슬래시(/)와 네트워크부 비트수로 나타내는 프리픽스(prefix) 표기법을 사용할 수 있습니다. <그림 10>에서 서브넷 마스크 255.255.255.0은 네트워크부의 비트수가 24비트이므로 프리픽스 표기법을 사용하면 /24가 됩니다. 프리픽스로 표기한 서브넷 마스크는 IP 주소와 함께 묶어 위 <그림 10>과 같이 표현합니다.

네트워크 부가 8비트인 클래스 A에서 8비트를 서브넷팅한 IP 주소를 서브넷 마스크로 정의하면 아래 <그림 11>과 같습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoPtep%2FbtqNVCcvMaJ%2FjurABfonKBufq9Zl37kmj0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 11> 클래스 A 서브넷팅 전후 서브넷 마스크</b></sup>
</p><br/>

서브넷팅 후 IP 주소는 동일하지만 달라진 서브넷 마스크로 서브넷팅 후에는 앞에서 16비트까지가 네트워크 부 인 것을 식별할 수 있게 됩니다.



<br/> 

#### 서브넷 마스크의 유용성

서브넷 마스크를 사용하면 8비트 단위가 아닌 **1비트 단위로 네트워크 부를 구성할 수 있기 때문에 더 세분화된 네트워크를 만들 수 있습니다.**

예를 들어, 약 60개의 호스트를 연결하는 네트워크를 구축하는 경우, 클래스 기준에서는 가장 적은 수의 호스트를 연결할 수 있는 클래스 C의 네트워크부를 사용할 수밖에 없습니다. 다시 말해 60개의 호스트를 연결하는 하나의 네트워크를 만들기 위해 IP 주소 관리 기관에 IP 주소 할당 신청을 하면 주소 관리 기관에서는 C클래스의 네트워크 부 주소 하나를 할당하게 되고 신청자는 254(2의 8승 - 2) 개의 IP 주소를 사용할 수 있게 됩니다. 60개가 필요한 데 254개가 할당되니 나머지 IP 주소는 누구도 사용하지 못하는 주소가 됩니다.

만약 호스트 부에서 2비트를 빌려 서브넷팅 하면 클래스 C의 1개의 네트워크를 4개로 분할하고 각 네트워크 당 62(2의 6승 -2)의 IP 주소를 사용할 수 있게 됩니다. 따라서 60개의 IP 주소가 필요한 사람에게 서브넷 마스크가 255.255.255.192인 IP 주소의 네트워크 부 주소 하나를 할당하고, 나머지 3개의 네트워크 부 주소를 다른 사람에게 할당하는 방법으로 IP 주소를 낭비하지 않을 수 있습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmJAAZ%2FbtqNQ2DlQah%2FooVuHtocZCwer0b26YwrA0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 12> 클래스 C의 서브넷팅</b></sup>
</p><br/>

현재는 클래스와 상관없이 한 네트워크에 연결하고 싶은 호스트들의 규모에 맞게 네트워크 부와 호스트 부의 길이를 비트 단위로 유연하게 변경할 수 있는 서브넷 마스크를 사용하여 IP 주소를 할당합니다.

클래스 방식에서 네트워크 부를 8비트 단위로 IP 주소 32비트의 맨 앞에서부터 선택한 것처럼 서브넷 마스크 방식에서도 네트워크 부를 1비트 단위로 IP 주소 32비트의 맨 앞에서부터 차례로 선택합니다. 따라서 서브넷 마스크는 반드시 연속한 '1'과 연속한'0'으로 구성됩니다. '1'과 '0'이 교대로 나타나는 서브넷 마스크는 없습니다. 이로 인해 서브넷 마스크의 십진수 표기법이 가질 수 있는 값은 <그림 13>과 같이 정해져 있습니다.

<br/><p align = "center">
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzZ6VD%2FbtqNQ4A6YTG%2FX7IxIS0USNALLSbwyu2XO0%2Fimg.png">
</p>
<p align = "center">
<sup><b><그림 13> 서브넷 마스크가 가질 수 있는 값</b></sup>
</p><br/>