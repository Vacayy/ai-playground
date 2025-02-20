# RAG 기반 해외 주식의 재무 데이터 분석
## 주제: 주식 분석 에이전트/챗봇

주식 분석 에이전트의 기초 버전으로, 미국 주식의 재무 데이터를 불러와 분석하는 기능을 구현하였습니다.


----
### 1. 프로젝트 입/출력 정하기
**입력**
- 특정 주식의 Ticker (예: MSFT)
- 분석 요청 질문 (예: "최근 손익계산서에서 순이익 추이를 분석해줘.")

**출력**
- 해당 주식의 재무 데이터 분석 결과
- 시계열 비교 및 추세 해석
- 결과의 근거가 되는 재무 데이터의 구체적 수치
- (추후 목표) 주가 차트와 뉴스 데이터를 통합한 총체적 분석

----
### 2. 방법론
**데이터 준비**
- 분석하고자 하는 주식의 ticker를 입력합니다.
- yfinance를 기반으로 해당 주식의 재무 데이터를 불러옵니다.
- JSON이 아닌 Pandas DataFrame 타입의 데이터입니다.
- 재무 데이터를 전처리한 다음, context로 넣어줍니다.

(Pandas DataFrame 타입의 재무 데이터)
![image](https://github.com/user-attachments/assets/1c3d48d0-66f6-482d-8fd8-feb577d1d45b)

**Prompts**
- 역할 프롬프트: 재무와 투자에 능통한 시니어 애널리스트로서의 역할 부여
- 질문 프롬프트: 분석 요청 질문과 필요한 데이터를 제공

**Prompts 전략**
- 역할과 데이터를 분리하여 명확한 인스트럭션 제공
- 수치 분석 및 계산은 코딩을 통해 수행하도록 요청

----
### 3. 실제로 prompt를 줬을 때 LLM의 응답
**질문**
> Microsoft의 손익계산서에서 기간별 순이익(Net Income) 추이를 요약해줘.

**응답**
> Microsoft의 2024년 6월 30일 기준 순이익은 88,136,000,000달러이며, 이는 전년 동기인 2023년 6월 30일의 72,361,000,000달러에 비해 증가했습니다. 또한 2022년 6월 30일에는 72,738,000,000달러였으므로, 두 해를 비교했을 때 연속적인 성장세를 보였습니다. 이러한 성장 추세는 견고한 총 수익과 비용 관리의 결과로 해석될 수 있습니다.

**실제 순이익 데이터($)**
- 2024-06-30: 88136000000.0
- 2023-06-30: 72361000000.0
- 2022-06-30: 72738000000.0
- 2021-06-30: 61271000000.0


실제 데이터에 기반한 정확한 분석을 제시했으며, 기간별 순이익의 변화와 그 배경에 대한 해석을 포함했습니다. 특히, 수치 비교와 시계열 분석을 명확히 수행한 점에서 신뢰할 수 있는 결과를 도출했습니다.

----
### 결론 및 향후 방향
**테스트 결과**
- 재무 데이터 기반 분석에서 LLM이 정확성과 맥락을 잘 유지함.
- 역할 프롬프트를 통해 전문성과 신뢰도를 높이는 데 성공.

**향후 방향**
- 주가 차트 및 뉴스 데이터 통합하여 다각적 분석 에이전트/챗봇 완성
