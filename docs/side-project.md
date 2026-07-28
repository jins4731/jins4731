# 🧩 Self-Service BI 데이터 모델링 플랫폼 (DataDesign Dashboard)

> Excel 데이터를 업로드하는 것만으로 데이터셋을 만들고, 차트와 대시보드까지 직접 구성할 수 있는 Self-Service BI 웹 서비스

🔗 [Repository](https://github.com/jins4731/datadesign-dashboard) · 🌐 [Demo](https://wemake.bar/)

> 🧭 메인 포트폴리오로 돌아가기: [portfolio.md](./portfolio.md) · 회사 프로젝트: [career.md](./career.md)

---

## 📌 프로젝트를 시작한 이유

회사에서 진행한 [BI 데이터 설계 플랫폼 개발](./career.md#data-design-platform) 프로젝트를 통해, SQL 지식이 없는 사용자에게 데이터 모델링이 얼마나 높은 진입장벽인지 직접 경험했습니다. 그 프로젝트는 조직 내부용 솔루션이라 데이터 소스와 배포 환경이 이미 정해져 있었지만, **"개인이 가진 엑셀 데이터만으로 아무 설치 없이 대시보드까지 만들 수 있다면 어떨까"** 라는 질문에서 이 프로젝트를 시작했습니다.

동시에 개인적으로는 React 19, React Router v7(Remix 스타일 데이터 로딩), Supabase 같은 최신 스택을 실제 서비스 규모로 다뤄보고 싶다는 목적도 있었습니다. 기획부터 배포까지 혼자 책임지는 프로젝트를 통해, 회사 업무에서는 이미 정해져 있던 아키텍처 의사결정을 스스로 내려보는 경험을 하고 싶었습니다.

---

## 🏗 Architecture

```
사용자 → Supabase 인증 → React 앱 → API 계층 → TypeORM → SQLite → Dataset 저장소 → ECharts 시각화
```

프론트엔드와 API 계층을 React Router v7의 loader/action 패턴으로 한 저장소 안에서 함께 관리하는 구조입니다. 별도의 백엔드 서버 없이도 데이터 조회·저장 로직을 라우트 단위로 배치할 수 있어, 개인 프로젝트 규모에 맞는 가벼운 풀스택 구조를 지향했습니다.

> TODO(Architecture): 전체 시스템 아키텍처 다이어그램 (Client / React Router / TypeORM / SQLite / Supabase)

---

## 🤔 기술 선택 이유

| 영역 | 기술 | 선택 이유 |
| --- | --- | --- |
| 프레임워크 | React 19, React Router v7, Vite | 파일 기반 라우팅과 loader/action 패턴으로 데이터 로딩·폼 처리를 라우트 단위로 응집시키기 위해 선택. Vite로 빠른 개발 서버와 빌드 속도 확보 |
| 데이터 저장 | TypeORM, better-sqlite3 | 회사 프로젝트에서 익숙했던 TypeORM의 엔티티 기반 모델링을 그대로 활용하면서도, 별도 DB 서버 없이 로컬/소규모 배포가 가능하도록 SQLite 채택 |
| 인증 | Supabase Auth | 인증 서버를 직접 구축하는 대신 세션 관리와 보호된 라우트 구현에만 집중하기 위해 BaaS(Backend as a Service)로 위임 |
| 시각화 | Apache ECharts | 실무(홈앤쇼핑 프로젝트 등)에서 대용량 데이터 렌더링 성능이 검증된 라이브러리로, 다양한 차트 타입과 커스터마이징 옵션이 필요했기 때문에 채택 |
| UI | shadcn/ui, Radix UI, Tailwind CSS | 헤드리스 컴포넌트로 접근성을 확보하면서도 디자인 시스템을 자유롭게 커스터마이징하기 위해 선택 |
| 폼 | React Hook Form, Zod | 데이터셋 생성, 차트 설정 등 필드가 많고 검증 규칙이 복잡한 폼을 스키마 기반으로 일관되게 관리하기 위해 채택 |
| 대시보드 레이아웃 | flexlayout-react | 위젯의 자유로운 배치·리사이즈·탭 구성을 직접 구현하는 대신, 검증된 레이아웃 엔진을 활용해 핵심 기능(차트/데이터 로직) 구현에 집중 |
| 엑셀 처리 | xlsx | 브라우저 환경에서 다중 시트 엑셀 파일을 파싱하기 위한 표준 라이브러리로 채택 |
| 배포 | Docker | 로컬 SQLite 파일과 애플리케이션을 함께 패키징해 배포 환경 간 일관성 확보 |

---

## 🔄 데이터 흐름

Excel 파일 하나가 대시보드 위젯이 되기까지의 흐름은 다음과 같습니다.

```
Excel 업로드
  → 시트 선택 및 첫 행을 컬럼 메타데이터로 해석
  → 데이터 타입 추론 (문자열 / 숫자 / 날짜 등)
  → Dataset 엔티티로 저장 (TypeORM)
  → Dimension / Measure 지정
  → Chart Builder에서 집계 함수(SUM, AVG, COUNT 등) 적용
  → ECharts로 시각화
  → Dashboard Builder에서 위젯으로 배치 (flexlayout-react, Drag & Drop)
```

핵심은 **"Excel → 메타데이터 모델 → Dataset → 시각화"** 로 이어지는 파이프라인에서, 원본 데이터를 한 번만 정규화해두면 이후 여러 차트가 같은 Dataset을 재사용할 수 있도록 만든 것입니다.

> TODO(Image): 엑셀 업로드부터 대시보드 완성까지의 화면 흐름 캡처

---

## ✨ 핵심 기능

### 1. Dataset Builder

- Excel 파일 업로드 및 시트(Sheet) 기반 데이터셋 생성
- 다중 시트 지원, 시트별 컬럼 선택을 통한 사용자 정의 데이터 집합 구성
- 컬럼 메타데이터 관리 및 데이터 타입 정의, Preview 기능

### 2. Chart Builder

- Dimension/Measure 기반 시각화, X축·Y축·색상·집계 함수(SUM/AVG/COUNT 등)를 사용자가 직접 설정
- 막대, 라인, 스캐터, 파이 등 기본 차트 타입 지원

### 3. Dashboard Builder

- flexlayout-react 기반 Drag & Drop 레이아웃으로 여러 차트를 하나의 화면에 자유롭게 배치
- 위젯 단위 대시보드 구성 관리

### 4. 사용자 인증

- Supabase 기반 로그인 및 세션 관리, 보호된 라우트 구현

> TODO(Image): Dataset Builder / Chart Builder / Dashboard Builder 각 화면 캡처

---

## 🛠 구현 과정

1. **데이터 모델 설계**: Dataset / Column / Row를 표현하는 TypeORM 엔티티를 먼저 설계해, 이후 어떤 기능을 추가하든 이 모델 위에서 확장할 수 있도록 했습니다.
2. **엑셀 파싱 및 타입 추론**: xlsx로 시트를 읽고, 컬럼별 값 샘플을 검사해 데이터 타입을 추론하는 로직을 구현했습니다.
3. **Chart Builder UI**: Dimension/Measure 선택과 집계 함수 설정을 React Hook Form + Zod로 관리해, 잘못된 조합(예: 문자열 컬럼에 SUM 적용)을 사전에 방지했습니다.
4. **Drag & Drop 대시보드**: flexlayout-react를 붙여 위젯 배치를 구현하고, 위젯 단위로 렌더링을 분리했습니다.
5. **인증 연동**: Supabase Auth로 로그인/세션 관리를 붙이고, 보호된 라우트를 React Router v7 loader에서 처리하도록 정리했습니다.

---

## 🚧 어려웠던 점

**다중 시트 엑셀의 컬럼 스키마 관리**
시트마다 컬럼 구성이 달라질 수 있어, 시트를 바꿀 때마다 이전 시트 기준으로 만들어둔 컬럼 선택 상태가 어긋나는 문제가 있었습니다. 시트 단위로 컬럼 메타데이터를 독립적으로 관리하고, 시트 전환 시 선택 상태를 초기화하는 방식으로 정리했습니다.

**Dataset 변경이 Chart 설정에 미치는 영향**
Dataset의 컬럼 구성이 바뀌면 이미 만들어둔 Chart의 Dimension/Measure 설정이 깨질 수 있었습니다. Dataset과 Chart 설정 사이의 의존 관계를 상태 구조로 명확히 분리해, 참조하는 컬럼이 사라졌을 때 이를 감지하고 처리할 수 있는 구조를 설계했습니다.

**차트 설정 변경 시 불필요한 전체 리렌더링**
대시보드에 여러 차트가 배치된 상태에서 하나의 차트 설정만 바꿔도 전체가 다시 그려지는 문제가 있었습니다. 렌더링 단위를 위젯(차트) 단위로 분리해, 설정을 변경한 위젯만 리렌더링되도록 구조를 개선했습니다.

**로컬 DB(better-sqlite3) 기준의 스키마 관리**
별도 DB 서버 없이 SQLite 파일 하나로 운영하다 보니, 엔티티 구조가 바뀔 때마다 마이그레이션을 직접 관리해야 했습니다. TypeORM 마이그레이션을 기능 단위로 쪼개어, 이후 변경 이력을 추적하기 쉽도록 관리했습니다.

---

## 🔭 앞으로 계획

- Dataset / 대시보드 Export 기능
- 대시보드 저장 및 불러오기
- 히트맵, 스택 차트 등 시각화 타입 추가
- AI 기반 차트 추천 기능 (회사 [AI 기반 BI 분석 지원 서비스](./career.md#ai-bi-analytics) 프로젝트 경험을 개인 프로젝트에도 적용해볼 예정)
- 대시보드 공유 및 RBAC 기반 권한 관리

---

📖 함께 보기: [portfolio.md](./portfolio.md) · [career.md](./career.md) · [performance.md](./performance.md)
