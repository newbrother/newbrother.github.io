---
layout: post
title: '블록체인 정리'
---

## 블록체인

정의 : 암호학기술을 사용한 분산되고, 추가만 가능한 데이터베이스(원장)

계층:
Data Layer (데이터 레이어)
* OSI로 따지면 물리적 계층으로써 가장 낮은 곳에 위치하고 있습니다. 제네시스 블록부터 이어지고 있는 블록체인 상의 데이터, 체인, 타임스탬프, 공개키 등이 포함됩니다.
Network Layer (네트워크 레이어)
* 아시다시피 블록체인은 기본적으로 P2P 네트워크를 기반으로 하고 있습니다. 네트워크 레이어는 P2P 네트워킹 매커니즘과 데이터전송 매커니즘이 포함되어 있죠. 각 노드는 자유롭게 연결되어 전체 체인을 유지하면서 데이터를 교환합니다.
Consensus Layer (컨센서스 레이어)
* 탈중앙화를 통해 각 노드가 분산화된 블록체인 상에서 데이터의 유효성에 대한 합의를 효율적으로 도출하기 위해서는 합의에 대한 협의가 가장 중요합니다. 합의 매커니즘은 블록체인의 핵심 기술이자 블록체인 커뮤니티의 통제 매커니즘이기도 하죠. 합의 매커니즘에는 작업증명을 포함하여 위임지분증명, 가치증명 등 다양한 매커니즘이 존재합니다.
Actuator Layer (액츄에이터 레이어)
* 액츄에이터 레이어는 블록체인 생태계를 더욱 효율적으로 동작시키기 위한 것으로 경제적인 보상제도로 볼 수 있는데요. 생태계 참여자를 위한 보상 발생과 배분이 포함되어 있습니다. 일정한 보상을 발생시켜 노드의 활발한 참여를 격려해 생태계를 유지시켜 발전을 유도하고 있죠.
Contract Layer (컨트렉트 레이어)
* 컨트렉트 레이어는 블록체인 상에서 프로그래밍 할 수 있는 다양한 기능들을 포함하고 있는 계층입니다. 프로그래밍이 가능한 코드나 알고리즘, 스마트컨트랙트 등이 포함되어 있습니다.
Application Layer (어플리케이션 레이어)
* 마지막으로 어플리케이션 레이어가 있는데요. OSI 7계층의 마지막 부분과 같이 블록체인 상에서 사용되는 Dapp 이라고 생각하시면 됩니다.

내부 구성
<Block 0>
block header : version , nonce_0
                        _
                    Timestamp_0   (유일성-복제불가능)
                    Merkle_Root_0
Body : Data_0
<Block 1>:작업증명을 통해 nonce값을 구할수 있는 사람이 생성
version, nonce_1
previous block hash_1 (block 0 의 헤더를 해싱해서 생성)
Timestamp_1
Merkle Root_1
Data_1
<Block ...> : 계속 연결
많이쓰이는 해쉬알고리즘: SHA-256(몇개는 sha-3) , 디지털 서명 (ECDSA : 타원곡선 디지털시그니처 알고리즘)
MD5는 2009년에 Chosen Prefix_collision 방식으로 뚫렸다.(위조가 가능하다)
SHA-1도 2017년에 구글에 의해서 뚫렸다.

SHA-3가 2015년에 AES, ECDSA 처럼 공모에 의해서 선정됨.(내부구조가 md5,sha1,sha2와 완전히 다름)

*solidity : 계약 지향 프로그래밍 언어. 블록체인 플랫폼 스마트계약 작성 및 구현에 사용.
*SHA : secure hash algorithm
*비트코인이 위험한것은 블록생성이 빠르게 되어? 문제가 생기는것보다(내생각) SHA-2 해시 충돌로 위조가 가능해질 위험이 크기 때문인것같다.


비밀키(대칭)암호 : DES,AES,SEED,ARIA

키를 교환해야한다.

일방향 함수 (ex해시함수):
y=Eg(x)로 x계산은 되지만
x=dg(y)로 y값으로 역연산은 불가능한 함수

비밀통로(trapdoor) 일방향함수(공개키 암호):
y=eg(x)로 x계산이 되고,
x=Dg(y)가 K(트랩도어정보)를 아는 사람은 y를 구할 수 있다.

공개키(비대칭)암호 : RSA, Rabin

전자서명: 메시지를 개인키로 서명을 하고, 누구든지 공개키로 검증
(RSA서명,DSA서명,ECDSA)


타원곡선


SHA 계열 해시함수
간단한 기본연산(논리회로 and, xor, rot, add, or)으로 연산하며 여러라운드를 반복 수행한다.

MD5 : 라운드64, 해시값(bit) : 128. 하지만 루트(2^128)=2^64동안은 안뚫려야 생일 공격에 안전한데, 그 이전에 공격할 수 있는 방법이 알려져서 보안에 취약하다.

SHA-0, SHA-1 : 해시값(bit)를 160으로 늘렸다. 라운드도 80으로 늘렸다. 하지만 마찬가지로 뚫렸다.

SHA-2 : 해시값:224,256,384,512 (256:비트코인 해시함수) 기본연산에 Shift right연산 추가.
SHA-256 : 해시값:256bit, 64라운드, 보안강도:128bit

비트코인발표:2008년 따라서 가장 강한 SHA-256를 사용

SHA-3(2015년 발표) : 연산:And,Xor,Rot,Not 4가지. 내부상태 bit가 엄청 크다. SHA-3 보안강도:128bit


 해시함수 기반의 작업 증명
H(nonce||이전해시값||데이터) < d개의 0으로 시작하는 해시값(d:난이도)
(이전해시값,데이터는 고정되어있음)
위의 수식을 만족하는 nonce를 찾으면 작업이 증명된다.

작업을 증명한사람이 블록체인을 업데이트 할 수 있는 권한을 얻으면서 보상을 받게 됩니다.

nonce가 주어진다면 d개의 0으로 시작한다는 검증은 간단하도록 설계가 되어있다.

머클 트리: 대량의 데이터를 해시함수를 이용한 이진트리 형태의 링크드리스트로 만들면 log(n)번의 해시계산으로 데이터 인증이 가능하다.
h(A), h(B) -> h(ab) = h( h(A) || h(B) )
h(C), h(D) -> h(cd) = h( h(C) || h(D) )
머클루트 : h ( h(ab) || h(cd) )

데이터 A`가 추가되었을때 저장한 머클 루트값과 다시 계산한 머클 루트값을 비교해서 인증한다.


합의 프로토콜
-분산형 네트워크
-두가지 종류의 실패: 특정노드가 다른노드와 통신이 불가능한 경우, 특정 노드가 메세지를 보내지만 정상적인 동작을 하지 않을 경우. ->실패에도 잘 동작해야함
-합의의 필요성 : 분산화된 시스템에서 동일한 블록을 유지하기 위함, 블록체인은 데이터베이스이며 트리구조로 가장 잘 표현가능하다. 가장 긴 체인(링크드리스트)이 유용한 블록체인의 블록으로 인정받는다. 모든 사용자는 합의 프로토콜을 통해 새로운 블록의 생성을 결정한다.


-합의 프로토콜 : 추가되는 다음 블록이 유일하다는 것을보장. 공격자들이 합의 프로토콜을 공격하더라도 새로운 분기를 방지한다.
-합의프로토콜의 종류 : 작업증명(POW), 지분증명(POS), 위임지분 증명(DPOS), 소요시간 증명(PET), 소실증명, 공간증명, 중요도증명 등

-합의프로토콜 요구사항 : 합의(노드는 동일한 값을 제시), 종료(종료 후 최종적 합의에 도달), 검증, 고장내성, 무결성(한번의 합의포로토콜에 한번만 결정을 내린다)
51%이상의 정직한 노드가 있다면 정상적으로 동작가능

합의프로토콜 과정 : 노드가 합의 프로토콜에 직접 참여한다(채굴), 채굴은 특정 '어려움'을 만족시키는 nonce값을 찾는 과정. 채굴과정은 대량 병렬컴퓨터를 이용해 전력소모가 막대하다. 채굴 알고리즘은 안전성을 보장하여야 한다.

작업증명(비트코인,이더리움)에서는 nonce값 찾는과정에서 컴퓨팅파워가 많이 소모된다.

지분증명(peercoin): 소유한 지분에 따라서 합의를 이룬다.
따라서 컴퓨팅파워를 적게 소모하고 합의과정의 속도가 빠르다. 공개형,비공개형 블록체인 모두에서 사용가능.
단점:가장 지분이 많은 사용자에게 중앙화 될수있다. 지분이 없는 사용자들끼리 합의 프로토콜 공격 가능성.

위임지분증명(DPOS)(이오스) : 지분 증명 방식에서 대표자를 선출하는 과정이 추가. 선출된 대표자가 블록의 합의를 결정.
장점: PoS에 비해 속도가 빠르고 확장성 문제 해결가능.
단점: 대표자를 선출하기 때문에 완벽한 분산시스템이 아니게된다.

소요시간증명(PET) : CPU의 특정 소요시간을 통해 작업을 증명하는 방식. 각 노드는 무작위 선정된 대기시간을 소요해야함.
장점: 병렬하드웨어 불필요, 컴퓨팅파워 적게 필요.
단점: 보안 보장 하드웨어 필요

Practical Byzantine Fault Tolerance(PBFT) : 
악의적 노드가 적당히 있어도 합의 프로토콜 결과 보장.
-악의노드가 f일때 3f+1노드가 결과를 결정한다면 안전(33% 내성)

Fast Byzantine Fault Tolerance(FBFT) :
PBFT에 비해 속도를 높이는 방식, 블록 생성자가 전달하는 노드수를 제한한다. 확장성도 PBFT보다 높다.

공개형 합의프로토콜은 보상이 필요하다.


블록체인 종류
-공개형 블록체인: 누구나 코드를 다운로드하여 로컬서버, 네트워크 등에서 노드를 실행할 수 있으며 합의 프로토콜에 참여. 
암호프로토콜과 채굴보상을 통해 안전성 제공
장점: 중앙기관제거, 거래당사자간 바로 거래 가능, 거래 프로세스 및 비용감소, 참가의 자유성, 거래와 기록의 투명성 제공
단점: 확장성 보장어렵다(초당 거래속도) 분기(fork)가능성, 프라이버시 및 중요정보 노출에 위험, 익명성 보장 한계, 시스템 문제 발생시 책임자 없음
대표적화폐:비트코인,이더리움,라이트코인
*하드포크 : 해킹,시스템장애,큰업데이트로 인해 이전과 호환이 안되는 경우
*소프트포크 : 하드포크 이외의경우(블록의 생성시간 조정등)

-폐쇄형 블록체인: 액세스 권한이 한 기관에 집중
기업내 또는 정부기관 등에서는 분산형 구조가 비효율적임(합의과정 시간소요, 대외비 문서 노출위험성)
기관이 참여자에게 읽기,쓰기 권한을 부여한다.
검증은 내부적으로 수행한다.
다른합의알고리즘사용가능(PBFT,FBFT)
허가형 블록체인이라고도 한다.

장점: 51%공격(노드의 반이상 컴퓨팅파워를 가지고 분기시켜버림)에서 자유로움, 합의알고리즘시간단축, 데이터 처리속도증가, 블록체인내부규칙변경용이(자유성), 높은 프라이버시 및 중요데이터 보호 가능

단점: 중앙관리형구조(블록체인 분산형 이념과 충돌), 단일 장애점 문제, 단순히 분산 원장의 역할(많은 은행들이 국가간 지불용으로 이미 분산원장 기술을 테스트했음)

대표적화폐: 리플, quorum

-혼합형 블록체인: 공개형블록체인과 폐쇄형 블록체인을 서로 연결하거나 통합한 형태(장점만 상속하는것이 목표)
더블체인: 공개형과 폐쇄형을 연결 1:N의 사이드 체인방식으로 구성가능
인터체인: 서로 다른 블록체인 네트워크간 연결을 위한 기술
콘소시엄형 블록체인: 콘소시엄 기업들이 협업하여 운영(폐쇄형과 유사) ex:자동차 관련 컨서시엄형해서 폐차기록, 생산기록, 하청부품 기록들 체인화가능
참여를 위해 특별한 허가가 필요하지만, 여러기관이 단체로 운영하다보니 다자간 합의 알고리즘이 필요하다.
연합형 블록체인이라고도 한다.
ex: 하이퍼레저패브릭, 뱅크사인
장점:높은프라이버시,기관공동작업 이상적구조, 독점불가.
단점: 내부에서 공격이 일어날 가능성

대표적화폐: Hdac, icon




주요 암호화폐

-비트코인 : 사토시 나카모토가 2008년 제안, 공개형 블록체인, 작업증명(PoW) 합의 프로토콜, 스택 기반의 스크립트 언어를 사용(제한적 성능)

-이더리움 : 비탈릭 부테린이 2015년 제안, 공개형 블록체인, 스마트 계약이 가능하여 다양한 서비스 구현 가능(solidity 언어를 지원해서 성능 구현가능, 즉 조건이나 반복 연산 구현 가능), 합의프로토콜로 작업 증명 방식을 사용했으나 2019년말에 지분 증명 방식으로 전환예정(먼저 지분증명과 작업증명의 하이브리드 형식인 캐스퍼 도입중). 이더리움 엔터프라이즈라는 기업용 비공개형 블록체인 개발 예정.


-하이퍼레저 프로젝트: 리눅스 재단에서 2017년 제안. 콘소시엄형 블록체인 플랫폼, 블록체인 기술이 모듈화 되어있어 필요한 모듈만 사용해 구현 가능. GO,Java로 구현되어 있어 스마트 컨트랙트를 위한 언어가 따로 존재하지 않음.
블록체인의 응용서비스에 시선을 맞춤. 
하이퍼레저 패브릭: 블록체인 Framework구현. 합의 프로토콜 제공, 사용자 서비스 제공, 플러그앤플레이 방식.


블록체인의 발전방향
(블록체인이 컴퓨팅 비용을 높일 순 있지만 사회비용을 더 크게 낮출것이다)
(이더리움을 사물인터넷에 적용하면 기계간 금융거래도 가능해진다)

한국 정부의 비전과 전략 : 블록체인으로 혁신하고 성장하는 나라

대표 적용 분야 : 금융 분야(비상장 주식 거래, 실손 보험금 청구), 의료 분야(개인 의료정보 관리, 유전체 정보 공유), 콘텐츠 분야, 공공 분야(전자증명서 유통, 온라인 투표), 물류-유통 분야(개인 통관, 다이아몬드 유통), 에너지 분야(이웃간 전력거래, 전기자동차 충전)
즉, 거래 장부를 따로(분산) 관리한것을 중앙화(하나의 시스템으로)하자. 거래 장부를 여러사람이 공유함으로써 신뢰를 향상 시킬 수 있다.

예시: 온라인 투표(본인인증 후 블록체인 네트워크에 기록)->투표 결과 직접 검증 가능
국가간 전자문서 유통(실시간 처리가능, 단 모든 국가가 블록체인 인프라가 구축되어야 함)
축산물 이력관리(각 단계별 생성 정보 공유하고 추가해 나간다, 데이터조작불가능해지고 문제발생시 10분내 추적가능)
해운 물류관리(개인 통관, 12시간 이상 소요->실시간가능 / 환적의 경우 블록체인시스템으로 컨테이너 반출입증 전자문서화90%비율 달성)

정부의 블록체인 기술개발 로드맵
-블록체인 기반 기술 : 고성능 저비용 합의 기술, 스마트 컨트랙트 검증 기술, 양자저항성 갖는 암호 기술
-블록체인 확장 기술 :  대용량 데이터 처리 기술 및 외부 데이터 연동 기술(단순 거래내역저장->영상,사진등 댜용량 데이터 관리)
  대규모 노드 참여에도 성능 유지, 상호운용성확보기술(블록체인 간 데이터 거래 및 스마트 컨트랙트 상호 호환)
-블록체인 서비스 기술 : 거래 추적 및 분석 기술(불법 거래등 비정상 상황 모니터링) , 산업 분야별 기존 시스템 연동 기술, 전략 서비스 분야별 특화 블록체인(규모,보안,성능 관점에서 맞춤형 제공)
*양자내성암호화폐 : 2018년에 구글,IBM이 72bit양자컴퓨터 개발성공(2^72를 한번에 계산가능)
 -Quantum resistant ledger(QRL) : 해시함수(XMSS)를 이용 양자 내성 전자서명 개발 중. 

앞으로 해야할일: 
-유럽연합 일반개인정보보호법(GDPR)에서는 개인정보데이터를 삭제가 가능해야한다고 되어있으므로 블록체인의 가역불가능성과 충돌한다.
-사용하는 암호기술의 장기간 안전성을 보장해야 하고 보다 우수하고 안전한 합의 프로토콜 개발
-국내 환경에 적합한 킬러 어플리케이션 개발 및 보급
-블록체인과 타영역(IoT기술)과 결합

DTCC(미국중앙예탁청산기관) : 파생상품에 대한 정보가 기록된 거래정보저장고(TIW)에 있는 계정에 대한 기록을 액스코어라는 맞춤형 디지털 분산 원장으로 옮길 예정. -> 분산원장 기술 적용으로 업계표준화 주도, 파생상품 처리비용을 간소화하고 자동화한다.

* 익명정보와 비식별화정보의 차이는 개인정보수집자가 정보주체를 인지할 수 있는 식별자를 포함하여 수집한 정보인가 이다. 여기서 익명 정보와 비식별화 정보는 표면적으로는 개인을 식별할 수 없으나, 비식별화는 재식별화의 위험성이 내포되어 있고, 개인을 작은 단위로 그룹화하여 개인을 관리하는 것이 가능하다.


예탁결제원도 국가간 전자문서 유통에서 활용하듯이 해외수탁기관에서 예탁결제원 승인받고 증권사에 정보가가서 병합사실등이 공지가 될때 블록체인을 사용하면 예탁결제원 승인과 함께 증권사의 병합사실을 차단하도록 개선이 가능하겠다.
하지만 해외수탁기관이나 증권사에서 블록체인 인프라가 갖춰져야 시행이 가능하다.