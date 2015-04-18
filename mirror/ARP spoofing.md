굉장히 단순하면서도 치명적이고 지독한 [해킹](%ED%95%B4%ED%82%B9.md) 방법.

주로 www.**.**/**/**.js 식의 [스크립트](%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8.md)를
쑤셔넣는 공격을 주로 한다.`[1]`  
그 외에도 만약 [VoIP](VoIP.md)`[2]` 사용자라면 통화내용도 도청이 된다.  
`[3]`  
[인터넷](%EC%9D%B8%ED%84%B0%EB%84%B7.md) 혹은
[네트워크](%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC.md)에 연결된
[컴퓨터](%EC%BB%B4%ED%93%A8%ED%84%B0.md)는 IP 주소 외에도 랜카드 고유의 인식 번호라 할 수 있는`[4]`
맥 어드레스(MAC address)라는 것을 부여 받는다. 그리고 같은 네트워크 혹은 **같은 회사의 회선**`[5]`을 이용하는 모든
이용자는 DHCP를 이용하여 IP 주소를 받기 때문에 기본적으로 인터넷 연결을 위해 Default Gateway에 대한 정보를 DHCP
옵션에 의해 받게 된다. 라우팅 테이블에서는 0.0.0.0 **게이트웨이 주소** 형태로 올라온 것을 볼 수 있는데, 이것은 밖으로 나가는
모든 패킷은 일단 게이트웨이로 보내겠다는 의미다. 즉, 로컬 네트워크에서 발생된 모든 트래픽은 게이트웨이로 나간다. 보통 인터넷 공유기가 이
역할을 해 주는데, 로컬 네트워크상에서는 IP 주소 이외에 다른 주소를 사용하여 통신하는데 이것이 바로 MAC 주소이다.

ARP Spoofing의 경우 대기하고 있다가 ARP 패킷에 답신을 하는 것이 아니라, ARP 패킷을 피해자 PC가 수신할 때 까지 무한대로
쏴댄다. 그러다 얻어 걸리면? [YOU JUST ACTIVATED MY TRAPCARD](YOU%20JUST%20ACTIVATED%20MY%20TRAP%20CARD.md). 공격자 PC는 [내가 바로 게이트웨이니까나한테 패킷을 보내라](%ED%8E%98%EC%9D%B4%ED%81%AC%EB%8B%A4%20%EC%9D%B4%20%EB%B3%91%EC%8B%A0%EB%93%A4%EC%95%84.md)라고 뻥을 친다. 하지만 컴퓨터는 생각만큼 똑똑하질 못해서 멍청하게 **정말로 그리로
패킷을 보낸다.**<del>야이새끼야!!</del> 공격자가 패킷 캡쳐하는 프로그램 사용하면 피해자가 주고받는 모든 패킷이 공격자 PC에
잡힌다.

하지만 중간 다리를 거쳐서 인터넷에 연결되므로 속도가 약간 느려진다. 뿐만 아니라 중간에서 데이터를 가로채므로 몇몇 기능이 제대로 동작하지
않는다. 그러나 이런 경우 대부분 컴퓨터가 이상하다고 생각하고 포맷을 권하는 지라, 이 공격에 노출된 것 자체를 알아채기가 쉽지 않은 것이
문제.

만약 아래와 같은 문제점이 있다면 ARP spoofing을 의심해보아야 한다.

  * 잘 되던 사이트가 갑자기 먹통이 될 때. 아예 안 뜨진 않지만 제대로 동작하지 않는다.
  * 특정 사이트에서 로그인이 안 된다. 이것도 될 때는 멀쩡히 된다.
  * 특정 페이지에서 페이지에 오류가 있습니다 라고 뜬다. 혹은 스크립트 오류 발견 등이 뜬다. 이것도 되다가 안되다가 할 때가 있다.
  * 액티브 X 를 사용하는 페이지`[6]`에서, 이유 없이 오류가 나거나 액티브 X를 재설치하라는 문구가 계속 뜬다. 이때 액티브 X를 삭제 후 재설치 해도 여전하다. 그러다가 될 때는 갑자기 된다.
  * 특정 사이트가 이유없이 깨져서 나타난다. 특히 인코딩이 깨진 것 처럼 외계어만 나타나는 경우가 많다. 이것도 될 때는 된다.
  * 윈도우 업데이트가 실패한다.
  * 이런 증상들이 나타나면서 바이러스나 악성코드 진단 시에는 이상이 없다.
  *   

![arp_spoofing.png](//rv.wkcdn.net/http://rigvedawiki.net/r1/pds/arp_spoofing.
png)

[PNG image (55.04 KB)]

  
실제로 가상 머신 상에서 ARP Spoofing을 시도하여 성공한 모습이다. arp -a를 입력했을때 이런 식으로 MAC 주소가 중첩되어
나타난다면 100%.

  *   

![arp_spoofing_2.png](//rv.wkcdn.net/http://rigvedawiki.net/r1/pds/arp_spoofin
g_2.png)

[PNG image (121.62 KB)]

  
피해자 PC에서 패킷을 잡아본다면 이런 패킷들이 보인다.  

대부분의 증상이 될 때는 된다 라고 되어있는데, 이것이 ARP spoofing의 무서운 점이다. 디폴트 게이트웨이를 건드리기 때문에 내가
걸렸든지 말든지 같은 회선 상의 누군가가 걸려있다면 **무조건** 영향을 받는다. 즉, 내가 감염되지 않아도 피해는 얼마든지 볼 수 있는
것. 감염된 컴퓨터가 꺼지면 문제가 사라지기 때문에, 될 때는 되고 안 될 때는 안되는 것. ARP 자체가 브로드캐스트 패킷이기 때문에
벌어지는 현상이다.

이런 문제가 발생한다면 일단은 안철수 연구소에서 ARP spoofing 관련 방어 툴을 제공하고 있으니 다운 받아보자. 하지만 이것도
근본적인 해결책은 안된다. 인터넷에서 많이 이야기 하는 Xarp 진단 툴의 경우 진단만 되고 치료는 유료다.

개인 컴퓨터의 감염 예방 방법으로는  

  * 항상 백신을 최신 상태로 업데이트하고, 실시간감시로 두며
  * MS에서 제공하는 보안패치 [MS10-002](http://www.microsoft.com/korea/technet/security/Bulletin/ms10-002.mspx), [MS10-018](http://www.microsoft.com/technet/security/bulletin/ms10-018.mspx)를 적용하고
  * CMD에서 “arp -s 게이트웨이 IP 주소 게이트웨이 MAC 주소”를 입력하여 게이트웨이의 주소들을 Static으로 고정하여 ARP Spoofing 공격으로 인해 발생되는 인터넷 불가 현상을 예방할 수 있다. 예) arp -s 192.168.0.1 00-08-5B-84-C6-DE  
이 방법이 먹히지 않는 경우가 있는데, 이 경우엔 netsh를 사용하면 된다.  
명령 프롬프트를 열고, netsh -c "interface ipv4"로 netsh 메뉴에 진입하고 show interfaces를 입력하여
자신의 랜카드를 찾는다. 보통 MTU가 1500이고, 로컬 영역 연결 또는 이더넷 등의 이름을 달고 있다. 확인 했으면, set
neighbors "랜카드 이름" "IP 주소" "맥 주소"를 입력하면 ARP 테이블에 게이트웨이를 Static으로 올려서 이 공격을 예방할
수 있다.  
이런식으로 ARP 테이블에 게이트웨이를 등록하게 되면  

![arp_spoofing_3.png](//rv.wkcdn.net/http://rigvedawiki.net/r1/pds/arp_spoofin
g_3.png)

[PNG image (61.63 KB)]

  
이렇게 게이트웨이의 MAC 주소가 정적으로 영구적으로 등록된다. 당연히 우선순위는 정적 > 동적이기 때문에 저렇게 해 두면 아무리 ARP
Spoofing 공격을 날려도 무용지물.  

네트워크 관리자로서는 위에 언급한 Xarp 진단툴등을 이용하거나 arp -a 커맨드로 감염된 PC를 찾아내어 치료를 하면 되겠다. Xarp는
[여기](http://www.chrismc.de/development/xarp/index.html)서 다운로드 받을 수 있다.

`\----`

  * `[1]` 공개된 스크립트가 몇몇 있지만, 하도 여러가지인데다 변조도 쉬워 스크립트를 이용해 방어하는 것은 별 의미가 없다.
  * `[2]` 인터넷 전화
  * `[3]` Cain & Abel 등..
  * `[4]` 제조사 번호와 제품 번호가 나뉘어지며 제조사가 제품 번호를 다 쓰면 다시 돌려 쓰긴 하지만 그 텀이 길기 때문에 사실상 네트워크 장치 고유의 번호라고 할 수 있다. 그런데 이거 소프트웨어적으로 바꿀 순 있다. 즉 뻥치기가 가능.
  * `[5]` 대표적인 예가 아파트 광랜. **당신도 예외가 아니다**
  * `[6]` 주로 게임실행이나 본인 인증 등
