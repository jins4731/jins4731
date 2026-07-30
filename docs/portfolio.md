# 👋 진승연 (Jin Seungyeon) — Frontend Developer

> React / TypeScript 기반으로 **BI(Business Intelligence)·SaaS 데이터 시각화 서비스**를 만드는 프론트엔드 개발자입니다.
> 대용량 데이터를 다루는 화면에서 "왜 느린가"를 측정하고 구조로 풀어내는 일을 좋아합니다.

📫 jins4731@gmail.com · 🐙 [github.com/jins4731](https://github.com/jins4731)

---

## 🙋 About Me

5년 이상 React 기반 BI·SaaS 플랫폼을 개발해 온 프론트엔드 개발자입니다. 데이터 모델링부터 시각화, 대시보드 구성까지 BI 서비스의 전체 흐름을 이해하고 있으며, 대용량 데이터를 다루는 화면에서 반복적으로 발생하는 **렌더링 병목·조회 지연 문제**를 구조적으로 해결하는 데 강점이 있습니다.

기능을 먼저 완성한 뒤 병목 구간을 측정하고, 필요한 지점에만 최적화를 적용하는 방식으로 작업합니다. 최근에는 JSP 기반 레거시 시스템을 React SPA로 전환하고, 이를 다시 SaaS 아키텍처로 확장하는 과정에 참여하면서 **"기능이 늘어나도 무너지지 않는 구조"** 를 설계하는 경험을 쌓았습니다.

- 5년 이상의 Frontend 개발 경험 (BI·SaaS 플랫폼 중심)
- React / Next.js / TypeScript 기반 서비스 개발 및 아키텍처 설계
- 대용량 데이터 시각화 환경에서의 렌더링 최적화 (DevExtreme, ECharts, SpreadJS)
- JSP 레거시 시스템 → React SPA → SaaS 아키텍처로 이어지는 전환 경험
- 자체 AI 모델 기반 분석·대시보드 자동 생성 기능 개발 경험

### Domain Experience

유통, 공공, 스포츠, 행정 등 다양한 산업군의 데이터 분석 요구사항을 이해하고 BI 플랫폼 기능으로 구현해 왔습니다. (홈앤쇼핑, 한국자활복지개발원, 스포츠토토, 한국국립과학원, 경찰청 등)

---

## 💡 핵심 역량

### 1. 프론트엔드 아키텍처 & 성능 최적화

대용량 데이터를 다루는 SaaS·BI 서비스에서 API 호출 구조와 렌더링 비용을 함께 고려한 구조 설계를 지향합니다.

- React DevTools Profiler / Chrome DevTools 기반 성능 저하 원인 분석
- Virtualized Rendering, Memoization, Code Splitting을 통한 렌더링 최적화
- API 캐싱·Prefetch 전략과 Zustand selector 기반 상태 분리로 불필요한 리렌더링 제거

> 📖 자세한 사례는 [performance.md](./performance.md) 참고

### 2. SaaS 플랫폼 & 데이터 시각화 개발

사용자·그룹·요금제가 얽힌 SaaS 권한 구조와 대용량 데이터 시각화 기능을 함께 설계·구현한 경험이 있습니다.

- 사용자 활동 로그 수집, 요금제·결제 상태 기반 접근 제어 등 SaaS 핵심 기능 설계
- NestJS Guard 기반 권한 검증 구조 설계 및 표준화
- DevExtreme, ECharts, SpreadJS 기반 대시보드·보고서 시각화 개발

### 3. 레거시 현대화 & 협업 리딩

레거시 시스템의 구조적 한계를 진단하고, 점진적 전환 전략과 협업 프로세스 개선을 함께 이끈 경험이 있습니다.

- JSP → React SPA 전환 전략 수립 및 컴포넌트 책임 분리
- 프로젝트 리더로서 일정·리스크 관리 체계 수립 (개발 일정 약 20% 단축)
- SVN → Git Flow 전환, Jest/RTL/Playwright 기반 테스트 문화 정착

> 📖 프로젝트별 상세 내용은 [career.md](./career.md) 참고

---

## 🧰 Tech Stack

**Frontend**

`React` `Next.js` `TypeScript` `React Router (Remix)` `TanStack Query` `Redux Toolkit` `Zustand` `Vite` `Tailwind CSS` `Shadcn UI`

**Data Visualization**

`DevExtreme` `ECharts` `D3.js` `SpreadJS` `Virtualized Rendering` `Large Dataset Optimization`

**Backend**

`NestJS` `Spring` `PostgreSQL` `TypeORM`

**AI**

`Prompt Engineering`

**Testing**

`Jest` `React Testing Library` `Playwright`

**DevOps & Collaboration**

`GitHub Actions` `Jenkins` `Git Flow` `Jira` `AWS`

---

## 📌 주요 프로젝트

### 🤖 AI 기반 BI 분석 지원 서비스
`2025.08 ~ 현재`

자체 AI 모델을 활용해 BI 조회 결과 분석과 대시보드 생성을 자동화하는 서비스입니다. 반복적인 보고서 작성 과정을 자동화하여 사용자의 BI 활용성을 높이는 데 초점을 맞췄습니다.

- **Tech**: Next.js, React, TypeScript, TanStack Query, PostgreSQL
- **핵심**: BI 결과 메타데이터 기반 AI 차트·대시보드 자동 생성, 유사 보고서 추천, Prompt Template 설계

📖 [career.md에서 자세히 보기](./career.md#ai-bi-analytics)

---

### 🎯 스포츠토토 BI 서비스 SSO 연동 및 안정화
`2025.06 ~ 2026.02`

스포츠토토 BI 서비스에 SSO 인증을 연동하고, 피벗그리드·데이터그리드·SpreadJS 기반 보고서 기능의 안정성을 높인 프로젝트입니다.

- **Tech**: React, DevExtreme(PivotGrid/DataGrid), SpreadJS, Spring
- **핵심**: SSO 연동 및 비상 로그인 기능 개발, SpreadJS 18 업그레이드, 그리드 페이징·필터 오류 개선

📖 [career.md에서 자세히 보기](./career.md#sportstoto)

---

### 🏢 BI 솔루션 SaaS 전환
`2025.01 ~ 2025.08`

기존 사용자·그룹 권한 체계에 요금제 기반 권한이 추가되며 급증한 복잡도를 해결하기 위해 SaaS 아키텍처로 전환한 프로젝트입니다.

- **Tech**: TypeScript, NestJS, TypeORM, React, Vite, Shadcn UI, DevExtreme, PostgreSQL
- **핵심**: NestJS Guard 기반 권한 검증 구조 설계, 사용자 활동 로그·운영 대시보드 구축, API 호출 32% 감소

📖 [career.md에서 자세히 보기](./career.md#saas-migration)

---

### 📊 홈앤쇼핑 전사 관리 지표 프로젝트
`2024.06 ~ 2025.05`

OLAP 기반 대용량 보고서의 조회 지연과 UI 프리징 문제를 해결하고, 프로젝트 리더로서 일정과 리스크를 관리한 프로젝트입니다.

- **Tech**: JavaScript, DevExtreme, React, ECharts, D3.js, SpreadJS, Oracle
- **핵심**: Virtualized Rendering·Lazy Loading·Memoization 적용, 보고서 평균 조회 시간 1분 이내로 단축

📖 [career.md에서 자세히 보기](./career.md#homeshopping)

---

### 🏗 BI 플랫폼 레거시 현대화
`2022.07 ~ 2023.12`

JSP 기반 레거시 시스템을 React SPA 아키텍처로 전환하며 컴포넌트 책임 분리와 상태 관리 구조를 재설계한 프로젝트입니다.

- **Tech**: React, NestJS, Spring, Redux Toolkit, Jenkins, GitHub Actions, Jest
- **핵심**: 전체 코드량 62% 감소, LCP 2초 → 0.5초 개선, Storybook 기반 컴포넌트 문서화

📖 [career.md에서 자세히 보기](./career.md#legacy-modernization)

---

### 🧩 Self-Service BI 데이터 모델링 플랫폼 (개인 프로젝트)

SQL 지식이 없는 사용자도 엑셀 데이터를 업로드해 데이터셋을 만들고, 차트와 대시보드를 직접 구성할 수 있는 셀프서비스 BI 웹 서비스입니다.

- **Tech**: React 19, TypeScript, React Router v7, ECharts, Supabase, PostgreSQL, TypeORM, Shadcn UI, Tailwind CSS
- **핵심**: Excel 기반 데이터셋 생성, Dimension/Measure 기반 Chart Builder, Drag & Drop 대시보드

🔗 [Repository](https://github.com/jins4731/datadesign-dashboard) · 🌐 [Demo](https://wemake.bar/) · 📖 [side-project.md에서 자세히 보기](./side-project.md)

---

## ⚡ 성능 개선 하이라이트

| 영역 | 개선 결과 | 상세 |
| --- | --- | --- |
| 초기 화면 로딩 (LCP) | 2초 → 0.5초 | [LCP 개선](./performance.md#lcp) |
| 대용량 보고서 조회 | 1분 30초~2분 → 1분 이내 | [Virtualized Rendering](./performance.md#virtualized-rendering) |
| API 호출 효율 | 월 API 호출 횟수 32% 감소 | [API Cache](./performance.md#api-cache) |
| 렌더링 커밋 시간 | React DevTools 기준 약 30% 개선 | [React Profiler](./performance.md#react-profiler) |
| 코드 구조 | 코드량 약 62% 감소 | [career.md](./career.md#legacy-modernization) |

> 📖 문제 정의부터 원인 분석, 해결 방법까지 전체 과정은 [performance.md](./performance.md) 에서 확인하실 수 있습니다.

---

## 🏢 Career

**㈜위세아이텍 · WI Development Team · Software Engineer** (2020.07 ~ 현재)

BI Platform 개발, SaaS 아키텍처 전환, 데이터 시각화, AI 기반 분석, 성능 최적화를 주요 업무로 담당하고 있습니다.

| 기간 | 프로젝트 |
| --- | --- |
| 2025.08 ~ 현재 | AI 기반 BI 분석 지원 서비스 |
| 2025.06 ~ 2026.02 | 스포츠토토 BI 서비스 SSO 연동 및 안정화 |
| 2025.01 ~ 2025.08 | BI 솔루션 SaaS 전환 |
| 2024.06 ~ 2025.05 | 홈앤쇼핑 전사 관리 지표 프로젝트 |
| 2022.07 ~ 2023.12 | BI 플랫폼 레거시 현대화 |
| 2020.07 ~ 2022.06 | BI 데이터 설계 플랫폼 개발 |

> 📖 프로젝트별 배경·문제·해결 과정은 [career.md](./career.md) 에서 확인하실 수 있습니다.

---

## 🎓 Education

**광운대학교 스마트융합대학원 · 정보시스템학과 석사** (2016.08 ~ 2018.08)
졸업논문: 노드의 전송 효율을 개선한 WSN 라우팅 기법 · GPA 4.27/4.3

**광운대학교 정보과학교육원 · 컴퓨터공학과 학사** (2013.03 ~ 2015.08)

---

## 📚 Documentation

이 저장소는 아래 문서들로 구성되어 있습니다.

| 문서 | 설명 |
| --- | --- |
| 📄 [portfolio.md](./portfolio.md) | 지금 보고 계신 메인 포트폴리오 문서 |
| 🏢 [career.md](./career.md) | 회사 프로젝트별 상세 설명 (배경 · 역할 · 구현 · 성과) |
| 🧩 [side-project.md](./side-project.md) | 개인 프로젝트 상세 설명 (아키텍처 · 기술 선택 이유 · 회고) |
| ⚡ [performance.md](./performance.md) | 성능 개선 사례 모음 (문제 · 원인 분석 · 해결 · 결과) |

---

## 📫 Contact

이메일로 편하게 연락 주시면 빠르게 답변드리겠습니다.

**Email**: jins4731@gmail.com
