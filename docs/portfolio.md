# 👋 진승연 (Jin Seungyeon) — Full-Stack Developer

> Spring Boot와 React로 **BI(Business Intelligence) 데이터 분석 플랫폼**을 만드는 풀스택 개발자입니다.
> 기능 하나를 DB 쿼리부터 API, 화면까지 끝까지 맡고, 고객사마다 다른 인증·DB·보안 환경을 직접 연동해 왔습니다.

📫 jins4731@gmail.com · 🐙 [github.com/jins4731](https://github.com/jins4731)

---

## 📊 숫자로 보는 경력

| 경력 | 제품 세대 | 회사 저장소 | 본인 커밋 | 구축 고객사 |
| --- | --- | --- | --- | --- |
| **6년** (2020.07 ~) | **3세대** (JSP → React·Spring Boot → 공공기관 공통) | **8곳** | **약 1,225건** (+ JSP 버전 소스 변경 약 950곳) | **10곳 이상** |

---

## 🙋 About Me

구축형 BI 플랫폼 **WISEOLAP**과 데이터 설계 플랫폼을 6년간 개발했습니다.

- **JSP 버전**(jQuery·Spring MVC)에서 카카오 지도 위젯을 처음부터 만들고, 통계 분석을 Java와 R 두 방식으로 계산하는 서버 구조를 맡았습니다.
- **React·Spring Boot 전환 버전**을 새로 만들 때 초기부터 참여해 보고서 저장·Top/Bottom 서버 처리를 화면부터 API까지 개발했고, 홈앤쇼핑 구축에서는 프로젝트 리더를 맡았습니다.
- **고객사 구축**에서는 SSO·JWT 연동, 외부 데이터 플랫폼 연동, 보안 점검 조치, 쿼리 생성·커넥션 풀 문제처럼 서버에서 풀어야 하는 요구를 주로 해결했습니다.

고객사 문제를 따라가다 보면 원인이 화면이 아니라 **쿼리 생성 로직, 집계 위치, 커넥션 풀, 인증 연동**에 있는 경우가 많았습니다. 그래서 병목이 어디에 있든 직접 찾아 고치는 방식으로 일합니다.

**Domain** — 유통, 공공, 국방, 스포츠, 문화, 종교 등 (홈앤쇼핑, 한국자활복지개발원, 한국콘텐츠진흥원, 스포츠토토, SH공사, 천주교, 경찰청, 국방, 산림청, 문화정보원, 한국소방, 자산관리공사 등)

---

## 💡 핵심 역량

### 1. Backend API & 데이터 처리
- Spring Boot + MyBatis 계층형 REST API: 보고서 저장, 사용자/그룹/권한, 보고서·폴더 관리, 쿼리 실행 로그, 보고서 쿼리 검색, 데이터 설계(관계·차원·주제영역) 저장
- 쿼리 생성기(QueryGen)의 집계·`GROUP BY` 오류 수정, DBMS별 메타 조회 쿼리(Oracle·Tibero·PostgreSQL·MariaDB·DB2·Vertica)
- 서버 데이터 파이프라인의 Top/Bottom 단계, 3D 차트·시계열 분석용 `DataMaker`, dsExcel 서버 엑셀 처리
- 통계 분석 12종을 Java(Apache Commons Math)와 R(Rserve)로 계산하는 API와 사이트별 전환 설정

### 2. 인증 · 보안 · 외부 연동
- 고객사 SSO 토큰 → 내부 JWT 발급, SSO 장애 대비 비상 로그인 검증, 포털 iframe 인증
- 외부 데이터 플랫폼(티맥스 HyperData)의 암호화 사용자 ID 복호화 연동, 프로젝트별 데이터 원본 자동 등록
- 보안 점검 조치: 요청 본문 AES-256 암호화(axios 인터셉터 ↔ `RequestBodyAdvice`)로 SQL Injection 차단, 화이트리스트 + Canonical Path로 Path Traversal 차단
- HikariCP 풀 튜닝으로 커넥션 고갈 해결, DRM 복호화 API·세션 정책 연동

### 3. Frontend & 데이터 시각화
- 카카오 지도 위젯 신규 개발(클러스터러·폴리곤 코로플레스·마스터 필터), 행정구역 코드 기반 드릴다운
- ECharts GL 3D 차트·시계열 분석, 데이터 하이라이트·변동 측정값, SpreadJS PDF 내보내기
- 셀마다 하던 계산을 열당 1회로 줄이고, 그리드 분리로 리렌더링 제거, SpreadJS tableBinding·지연 로드
- Atomic Design 공통 컴포넌트, Custom Hook, Redux Toolkit selector

### 4. 협업 · 리딩
- 홈앤쇼핑 프로젝트 리더 — 일정 산정·리스크 관리
- 고객사 저장소 생성부터 구축·배포 담당 (천주교, SH공사, 스포츠토토, 한국자활, 한국콘텐츠진흥원)
- Jira 티켓(`WID-xxx`) 단위 작업, GitHub PR 기반 협업

> 📖 사례별 상세: [career.md](./career.md) · [performance.md](./performance.md)

---

## 🧰 Tech Stack

| 구분 | 회사 실무 | AI 프로젝트 · 개인 프로젝트 |
| --- | --- | --- |
| **Backend** | Java, Spring Boot, Spring MVC, MyBatis, HikariCP, JWT·SSO 연동, AES-256, dsExcel, R(Rserve), Apache Commons Math, JUnit | Drizzle ORM, Supabase(Auth·PostgreSQL) |
| **Database** | Oracle, Tibero, PostgreSQL, MariaDB, DB2, Vertica, MSSQL | PostgreSQL |
| **Frontend** | JavaScript, React, Redux Toolkit, React Router, styled-components, jQuery, JSP | TypeScript, Next.js, TanStack Query, React Router v7, Vite, Tailwind CSS, shadcn/ui |
| **Visualization** | DevExtreme, ECharts(GL), D3.js, SpreadJS, jsPDF, Kakao Maps API, GeoJSON | ECharts, flexlayout-react |
| **DevOps · 협업** | Maven, Tomcat, GitHub Actions, Git, Jira | Vercel, Docker |

---

## 📌 주요 프로젝트

| 프로젝트 | 기간 | 한 줄 요약 |
| --- | --- | --- |
| [WISEOLAP JSP 버전 고도화](./career.md) | 2020.07 ~ 2022.04 | 카카오 지도 위젯 신규 개발, 통계 분석 Java·R 이중 구현 |
| [BI 데이터 설계 플랫폼](./career.md) | 2022.10 ~ 2023.07 | 테이블 관계 설정 화면과 변경분 저장 API |
| [WISEOLAP React·Spring Boot 전환](./career.md) | 2023.08 ~ 2024.01 | React·Spring Boot 신규 구축, 보고서 저장·Top/Bottom 서버 처리 |
| [홈앤쇼핑 전사 관리 지표](./career.md) | 2024.01 ~ 2025.05 | PL, 사용자·권한·보고서 관리 API, 쿼리 로그, 엑셀 보고서 성능 |
| [고객사 BI 구축](./career.md) | 2022.09 ~ 현재 | SSO·JWT, 보안 조치, 3D·시계열 분석, 외부 플랫폼 연동 |
| [AI 기반 분석 자동화](./career.md) | 2025.08 ~ 현재 | AI 차트·대시보드 자동 생성 |
| [Self-Service BI (개인)](./side-project.md) | 2025.10 ~ 2026.07 | 엑셀 업로드부터 대시보드 저장까지 1인 풀스택 |

### 📊 전사 관리 지표 플랫폼 (홈앤쇼핑)
`2024.01 ~ 2025.05` · 프로젝트 리더 / Full-Stack

환경설정이 없던 React·Spring Boot 버전에 사용자·그룹·권한·보고서 관리와 쿼리 실행 로그를 API부터 화면까지 만들고, 엑셀 양식 보고서 성능을 개선했습니다.

- **Backend**: 사용자/그룹/기능 권한·데이터 원본·보고서/폴더 관리 API, 쿼리 실행 로그 개선·보고서 쿼리 검색, SpreadJS 파일 저장·dsExcel, 공용 보고서 목록 조회 개선, DRM 연동
- **Frontend**: 환경설정 화면, SpreadJS tableBinding·지연 로드, 보고서·폴더 Drag & Drop, 즐겨찾기·틀 고정

📖 [자세히 보기](./career.md)

### 🏛 고객사 BI 구축 및 커스터마이징
`2022.09 ~ 현재` · Full-Stack

- **스포츠토토**: SSO + JWT 연동, 비상 로그인 검증 API, 요청 본문 AES-256 암호화, Path Traversal 조치
- **천주교**: 티맥스 HyperData 연동 — 암호화 사용자 ID 복호화, 프로젝트별 데이터 원본 자동 등록
- **공공기관 공통 버전**: 3D 차트·시계열 분석(서버 `DataMaker` + ECharts GL), 포털 iframe·기관 SSO 연동, 이중 집계 오류 수정
- **한국자활·경찰청**: NOFUNC 측정값 `GROUP BY` 오류 수정, 커넥션 풀 고갈 해결, 드릴다운·변동 측정값·하이라이트, 행정구역 개편 반영
- **한국콘텐츠진흥원 / SH공사**: SpreadJS PDF 내보내기·세계 지도 / Vertica 메타 조회 지원

📖 [자세히 보기](./career.md)

### 🗺 WISEOLAP JSP 버전 고도화 — 카카오 지도 · 통계 분석
`2020.07 ~ 2022.04` · Full-Stack

- **Frontend**: 카카오 지도 위젯(마커 클러스터러·폴리곤 코로플레스·마스터 필터·편집 팝업), 코로플레스 드릴다운 개선(산림청)
- **Backend**: 통계 분석 12종의 R(Rserve) 구현과 Java/R 사이트별 전환, Z·카이제곱·F 검정·기술통계 추가

📖 [자세히 보기](./career.md)

### 🗂 BI 데이터 설계 플랫폼
`2022.10 ~ 2023.07` · Full-Stack

- **Frontend**: 데이터 원본 뷰 관계 설정(자동 매핑·1:N/N:1·복합키), 차원·주제영역 편집
- **Backend**: 변경 상태(`modifyTag`) 기반 저장 API, DBMS별 메타 조회, Oracle 쿼리 튜닝

📖 [자세히 보기](./career.md)

### 🏗 WISEOLAP React·Spring Boot 전환
`2023.08 ~ 2024.01` · Full-Stack

- 보고서 저장 흐름을 모달·훅·Redux부터 API·Mapper까지 신규 설계
- 서버 `DataSanitizer`에 Top/Bottom 단계 추가, 아이템 생성·데이터 준비 로직 모듈화

📖 [자세히 보기](./career.md)

### 🤖 AI 기반 분석 자동화
`2025.08 ~ 현재` · Full-Stack

- BI 결과 메타데이터 기반 AI 차트·대시보드 자동 생성, 유사 보고서 추천, 목적별 Prompt Template
- **Tech**: Next.js, TypeScript, TanStack Query, ECharts, PostgreSQL

📖 [자세히 보기](./career.md)

### 🧩 Self-Service BI 데이터 모델링 플랫폼 (개인 프로젝트)
`2025.10 ~ 2026.07` · 1인 개발

엑셀 업로드부터 차트·대시보드 구성과 저장까지 되는 셀프서비스 BI 웹 서비스입니다.

- **구현**: UI와 분리한 차트 엔진(binding → groupBy → aggregate → ECharts 옵션), `loader`·`action` 기반 인증 확인과 대시보드 저장(JSONB)
- **해결한 문제**: Supabase 풀러의 prepared statement 미지원 대응, 라우트별 인증 요청 제거와 서울 리전 배포로 응답 시간 단축
- **Tech**: React 19, TypeScript, React Router v7, Drizzle ORM, Supabase, ECharts, Vercel, Docker

🔗 [Repository](https://github.com/jins4731/datadesign-dashboard) · 🌐 [Demo](https://wemake.bar/) · 📖 [자세히 보기](./side-project.md)

---

## ⚡ 성능 · 안정성 하이라이트

| 영역 | 개선 내용 | 상세 |
| --- | --- | --- |
| 엑셀 양식 보고서 | tableBinding·지연 로드·서버 엑셀 처리로 저장·불러오기·다운로드 개선 | [SpreadJS](./performance.md) |
| 그리드 렌더링 | 셀마다 하던 열 최댓값 계산 N² → 열당 1회 | [반복 계산 제거](./performance.md) |
| 지도 | 마커 클러스터러, 다시 그릴 때 이전 오버레이 해제 | [지도 마커·오버레이](./performance.md) |
| 목록 조회 API | 보고서×폴더 이중 반복 → `Set` 조회 + 사용자명 캐시 | [공용 보고서 목록](./performance.md) |
| DB 커넥션 | 커넥션 고갈·타임아웃 해소, 설정 외부화 | [커넥션 풀](./performance.md) |
| 집계 정합성 | NOFUNC·이중 집계로 틀어지던 결과 수정 | [GROUP BY 오류](./performance.md) |
| 보안 점검 | SQL Injection·Path Traversal 조치 | [요청 본문 암호화](./performance.md) · [Path Traversal](./performance.md) |

---

## 🏢 Career

**㈜위세아이텍 · AX Development Team · Full-Stack Engineer** (2020.07 ~ 현재)
BI 플랫폼 WISEOLAP과 데이터 설계 플랫폼의 백엔드 API·쿼리·인증 연동과 프론트엔드 시각화를 함께 개발하며, 고객사 구축과 AI 기반 분석 자동화를 담당하고 있습니다.

## 🎓 Education

**광운대학교 스마트융합대학원 · 정보시스템학과 석사** (2016.08 ~ 2018.08) — 졸업논문: 노드의 전송 효율을 개선한 WSN 라우팅 기법 · GPA 4.27/4.3
**광운대학교 정보과학교육원 · 컴퓨터공학과 학사** (2013.03 ~ 2015.08)

---

## 📚 Documentation

| 문서 | 내용 |
| --- | --- |
| 📄 [portfolio.md](./portfolio.md) | 지금 보고 계신 요약 문서 |
| 🏢 [career.md](./career.md) | 프로젝트별 상세 (요약 · 핵심 기여 · 해결한 문제 · 설계 포인트 · 성과) |
| ⚡ [performance.md](./performance.md) | 성능·안정성 사례 10개 (문제 · 원인 · 해결 · 결과) |
| 🧩 [side-project.md](./side-project.md) | 개인 프로젝트 (아키텍처 · 기술 선택 이유 · 어려웠던 점) |

📫 **Contact** — jins4731@gmail.com
