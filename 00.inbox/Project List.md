

Tile Rush

기술스택 : SuiMove/ msytein dapp-kit & sui/ React/ vercel
https://github.com/nubro999/BB_sui_hackathon
실시간 경쟁과 즉각적 보상을 경험할 수 있는 Sui 블록체인 기반 온체인 전략 게임입니다.  두 명의 플레이어가 10x10 보드에서 SUI 토큰이 담긴 타일을 빠르게 수집하며, 속도와 전략을 겨루게 됩니다.  게임 내 모든 자산과 상태는 Sui의 Object 모델로 관리되며, 플레이어의 모든 행동은 블록체인에 기록됩니다.  빠른 턴 진행(3초 타임아웃), 즉각적 토큰 지급, 실시간 상태 반영 등 Sui의 기술적 장점을 극대화합니다. zk login을 지원하는 enoki Wallet을 사용하여 사용성을 도모합니다. 저는 이프로젝트에서 PM, Move Contract, Frontend 같은 전반적인 리딩을 맡았습니다.
## 기능적 구현

1. 실시간 2인 경쟁 및 즉각적 토큰 보상
2. 전략적 동선 선택 및 빠른 턴 진행
3. 간결한 인터페이스로 직관적 게임 플레이
4. 온체인 자산 관리 및 투명한 게임 기록

## 기술적 구현

1. Object-Centric Design 기반 온체인 데이터 구조
2. 병렬 트랜잭션 처리 및 빠른 finality(평균 400ms)
3. 이벤트 기반 실시간 상태 업데이트
4. Move 프로그래밍 언어 및 Sui Dynamic Field 활용

Recordii
기술스택 : Kotiln/ Ktor/ Koin/ coroutines/ Android API/ clean architecture
https://github.com/nubro999/kotlin_record
기록이라는 수단을 능동적으로 접근할 수 있도록 도와주는 안드로이드 어플리케이션입니다. 주요기능으로 STT기능, ai 질문 기능이 있고 사용자가 음성으로 마크다운 형식의 파일을 작성할 수 있습니다. 작성한 내용에 대해서 ai에게 보완적인 질문을 받아 답하는 방식으로 내용을 확장할 수 있습니다. 이 외에도 서식화, 문법 수정 등의 ai기능이 있습니다. ai와 stt는 api형식으로 소통하며 GoogleSpeech, Gemini, GPT를 사용합니다. 

기능적 구현
1. 편리한 음성 기록 - STT(speech to text) 
2. 창의적인 생각의 어려움을 해소하는 것(ai의 능동적인 질문) 
3. 번거로운 작업축소(ui 단순화) 
4. 데이터보안(기록내용 개인화)

기술적 구현
1. clean architecture
2. thread 최적화
3. MVVM 구조
4. 지연 최소화

Auto Trading
https://github.com/nubro999/AutoTrading
기술스택 : Python/ Upbit, Serp, Fear&Greed APIs/ gpt api/ FastAPI/ React/ 
Aws EC2, Nginx, Docker & Compose

AI와 데이터 분석을 활용한 암호화폐 자동 트레이딩 시스템입니다.  
시장 데이터, 뉴스, 투자심리 등 다양한 정보를 종합 분석하여 자동으로 매매 결정을 내리고, 웹 대시보드를 통해 실시간 현황을 모니터링할 수 있습니다. 현재는 업비트 거래소의 API를 사용하지만 추후 DEX에 연동할 계획입니다.

기능적 구현

1. AI 자동매매  
15개 주요 코인 분석 및 종목/매매타이밍 자동 선정  
시장 데이터, 뉴스, 심리지수(Fear & Greed) 등 다양한 정보 융합  
동적 포트폴리오 및 위험관리(비중, 손절/익절)

2. 싱글코인 집중 모드  
특정 코인에 대한 심층 분석  
AI 또는 수동 타겟 지정, 기술적 분석 백업

3. 실시간 데이터 수집 및 분석  
업비트 실시간 시세, 과거 OHLCV, 거래량  
구글 뉴스 기반 시황 분석 및 감성 점수화  
시장 심리지수(0~100) 통합

4. 웹 대시보드  
실시간 자산 현황, 거래내역, 수익률 시각화  
거래/분석 로그 및 통계 제공

API 기반 AI 연동  
OpenAI GPT-4, SerpAPI, PyUpbit 등 다양한 외부 API 연동  
REST API 및 WebSocket 실시간 업데이트



RecorD
기술스택 : Type script/ Next.js, nest.js/ gpt real-time web-rtc
https://github.com/nubro999/nest_record
위의 Recordii프로젝트 제작 전 typescript기반으로 제작한 웹어플리케이션입니다.
Model View Controller 구조로 기존의 웹어플리케이션 구조 문법을 사용했습니다.
WebRTC를 사용하여 실시간으로 ai와 대화하여 기록하고 이를 ai가 요약하고 능동적으로 필요한 부분을 찾아서 사용자에게 질문하는 기능을 구현했습니다. 다만 웹어플리케이션이 기록의 편리함이라는 목표를 달성하기에 물리적인 에로사항이 있어 위의 kotlin프로젝트로 변경했습니다.

기능적 구현
1. 음성 녹음: 앱에 직접 생각, 아이디어, 감상을 말로 기록합니다.
2. AI 처리: 고도화된 음성 인식 기술로 사용자의 음성을 텍스트로 변환합니다.
3. 요약 제공: AI가 주요 내용을 추출해 간단한 요약을 제공합니다.
4. 저장 및 리뷰: 일기 내용을 안전하게 저장하고 언제든지 다시 확인할 수 있습니다.


myhome
기술스택 : Typescript/ Dokcer/ React/ Nginx/ Aws EC2, S3
https://github.com/nubro999/myhome
EC2로 배포한 개인블로그입니다. typescript와 react를 사용했고 서버는 nginx를 사용했습니다. 

기능적 구현
1. 게시판
2. 갤러리
3. 포트폴리오
4. 최근 게시물

CS wiki
기술스택 : Obsidian/ git
https://github.com/nubro999/Obsidian
학습한고 리서치한 기술적인 내용을 Obsidian으로 정리한 Wiki형식의 파일입니다. 블록체인, 보안, 네트워크 등의 자료를 지속적으로 정리 및 업데이트합니다.


SE_2_2
기술스택 : Cpp
https://github.com/nubro999/SE_2_2
Requirement list > UseCase Diagram & description > communication diagram의 과정을 거쳐 소프트웨어 공학적으로 설계부터 구현까지의 과정을 거친 프로젝트입니다.
requirement capturing을 하여 도출된 결과물을 기반으로 requirement analysis 단계를 수행하고detailed design과 implementation을 수행했습니다.
기능적 구현
1. 회원가입
2. 로그인/로그아웃
3. 자전거 등록
4. 자전거 대여
5. 자전거 대여정보 조회

Silent-Auction
https://github.com/mmingyeomm/silent-auction
Silent auction is a private auction platform where auction participant and amount is concealed until the round results is published. Anyone can put up their digital item on the auction and the settlement happens for every round of the auction
저는 이프로젝트에서 프론트엔드(UI, UX)와 서버를 맡았고 nginx의 roadbalancing을 담당했습니다.

