# ⚡ Performance

대용량 데이터를 다루는 BI·SaaS 서비스에서 반복적으로 만났던 성능 문제와 해결 과정을 정리했습니다. 모든 항목은 **문제 → 원인 분석 → 해결 방법 → 결과** 순서로 정리했으며, 어떤 프로젝트에서 있었던 일인지 함께 표기했습니다.

기능을 먼저 완성한 뒤, React DevTools Profiler와 Chrome DevTools로 실제 병목 지점을 측정하고 그 지점에만 최적화를 적용하는 방식으로 작업합니다. "일단 memoization부터 걸고 본다" 대신, 측정 → 원인 특정 → 최소 범위 최적화 순서를 지키려 합니다.

> 🧭 메인 포트폴리오로 돌아가기: [portfolio.md](./portfolio.md) · 프로젝트 상세: [career.md](./career.md)

---

## 목차

1. [LCP 개선](#lcp)
2. [React Profiler 기반 렌더링 분석](#react-profiler)
3. [Chrome DevTools 기반 네트워크 분석](#chrome-devtools)
4. [Virtualized Rendering](#virtualized-rendering)
5. [Lazy Loading](#lazy-loading)
6. [Memoization](#memoization)
7. [Code Splitting](#code-splitting)
8. [Prefetch](#prefetch)
9. [API Cache](#api-cache)

---

<a id="lcp"></a>

## 1. LCP 개선

**관련 프로젝트**: [BI 플랫폼 레거시 현대화](./career.md#legacy-modernization) (2022.07 ~ 2023.12)

### 문제

초기 페이지 로드와 대용량 보고서 조회 속도가 느려 사용자 체감 성능이 낮았고, 이로 인한 운영 오류(타임아웃, 재시도 등)도 함께 발생하고 있었습니다.

### 원인 분석

- 데이터 가공 로직이 클라이언트에 집중되어 있어, 화면에 처음 콘텐츠가 그려지기 전까지 대기 시간이 길었습니다.
- 차트·피벗·그리드 등 시각화 컴포넌트가 초기 진입 시점에 한꺼번에 렌더링을 시도해 병목이 발생했습니다.
- 동일한 데이터를 캐싱 없이 매 화면 진입마다 새로 요청하고 있었습니다.

### 해결 방법

- 데이터 처리 구조를 최적화해 무거운 가공 로직을 클라이언트에서 서버 사이드로 이동
- [API 캐싱](#api-cache), 중복 호출 방지, [Prefetch](#prefetch) 전략을 적용해 네트워크 병목 완화
- 렌더링 병목 구간을 분석해 시각화 컴포넌트별 렌더링 최적화 전략 적용

### 결과

- LCP **2초 → 0.5초**로 개선
- 초기 로딩 지연으로 인한 운영 오류 약 **40% 감소**

---

<a id="react-profiler"></a>

## 2. React Profiler 기반 렌더링 분석

**관련 프로젝트**: [BI 솔루션 SaaS 전환](./career.md#saas-migration) (2025.01 ~ 2025.08)

### 문제

전역 상태(Zustand)가 변경될 때마다 화면 전체가 리렌더링되면서 사용자 인터랙션 응답성이 떨어졌습니다. 어떤 컴포넌트가 병목인지 감으로는 특정하기 어려웠습니다.

### 원인 분석

- React DevTools Profiler로 Commit 단위 렌더링 시간을 측정한 결과, 전역 상태를 구독하는 컴포넌트가 도메인 구분 없이 하나의 스토어를 참조하고 있었습니다.
- 상태 변경의 영향 범위가 실제 필요한 컴포넌트보다 훨씬 넓게 퍼져 있었습니다.

### 해결 방법

- 전역/로컬 상태를 도메인 단위(Zustand selector 기준)로 분리해 구독 범위를 최소화
- 계산 비용이 큰 지점에만 `useMemo`, `useCallback`을 선택적으로 적용 (모든 곳에 일괄 적용하지 않음)
- 입력 필터에 디바운싱을 적용해 타이핑 시마다 발생하던 불필요한 리렌더링·API 호출 제거

### 결과

- 초기 렌더링 속도 및 화면 전환 성능 개선
- 필터 입력 등 잦은 인터랙션 구간의 응답성 향상
- [레거시 현대화](./career.md#legacy-modernization) 프로젝트에서도 동일한 방식의 Profiler 분석으로 React DevTools 기준 Commit 시간 약 **30% 개선**을 확인했습니다.

---

<a id="chrome-devtools"></a>

## 3. Chrome DevTools 기반 네트워크 분석

**관련 프로젝트**: [BI 솔루션 SaaS 전환](./career.md#saas-migration) (2025.01 ~ 2025.08)

### 문제

동일한 데이터를 여러 컴포넌트가 각자 조회하면서 중복 네트워크 트래픽이 발생했습니다. 더 큰 문제는 권한 검증이 데이터 조회 API 응답 이후에 이루어져, 권한이 없는 데이터가 화면에 순간적으로 노출되는 Race Condition이었습니다.

### 원인 분석

- Chrome DevTools Network 탭으로 화면 진입부터 사용자 액션 종료까지 발생하는 모든 API 요청을 전수 추적했습니다.
- 하나의 화면에서 권한 확인, 메타 정보 조회, 실제 데이터 조회 API가 뒤섞여 호출되고 있었고, 호출 순서가 보장되지 않았습니다.

### 해결 방법

- API를 목적 단위(권한 확인 / 메타 정보 / 실제 데이터 조회)로 분류해 호출 책임을 명확히 분리
- `AbortController`를 활용해 이전 요청을 취소하고, 최신 요청·검증된 권한 응답만 화면에 반영되도록 구조 변경

### 결과

- 권한 검증 이전에 데이터가 노출되던 Race Condition 해결
- 불필요한 중복 호출 제거로 [API 호출 32% 감소](#api-cache)에 기여

---

<a id="virtualized-rendering"></a>

## 4. Virtualized Rendering

**관련 프로젝트**: [홈앤쇼핑 전사 관리 지표 프로젝트](./career.md#homeshopping) (2024.06 ~ 2025.05)

### 문제

SpreadJS 기반 대용량 보고서에서 스크롤이나 사용자 인터랙션 중 UI 프리징이 빈번하게 발생했습니다.

### 원인 분석

- 조회되는 데이터 전체를 한 번에 DOM으로 그리다 보니 DOM 노드 수가 과도하게 늘어났고, 메인 스레드 점유 시간이 길어져 인터랙션이 끊기는 현상으로 이어졌습니다.

### 해결 방법

- 화면에 실제로 노출되는 행/열만 렌더링하도록 렌더링 구조 변경
- 스크롤 위치를 기준으로 렌더링 범위를 동적으로 조절해, viewport 밖의 데이터는 렌더링하지 않도록 제한

### 결과

- DOM 생성량과 메인 스레드 점유 시간 감소로 UI 프리징 현상 제거
- 보고서 평균 조회 시간 단축([Lazy Loading](#lazy-loading), [Memoization](#memoization)과 함께 적용)에 기여

---

<a id="lazy-loading"></a>

## 5. Lazy Loading

**관련 프로젝트**: [홈앤쇼핑 전사 관리 지표 프로젝트](./career.md#homeshopping) · [BI 플랫폼 레거시 현대화](./career.md#legacy-modernization)

### 문제

화면에 진입하는 순간 핵심 지표와 상세 데이터를 한꺼번에 요청하면서 초기 응답 시간이 길어졌습니다.

### 원인 분석

- 사용자가 실제로 보는 것은 대부분 초기 화면의 핵심 지표뿐인데, 상세 데이터까지 미리 모두 로딩하는 구조라 불필요한 대기 시간이 발생하고 있었습니다.
- 컴포넌트 단위로도 화면 진입 즉시 모든 하위 컴포넌트를 동기적으로 로딩하고 있었습니다.

### 해결 방법

- 초기 화면 진입 시에는 핵심 지표만 우선 로딩하고, 상세 데이터는 사용자 인터랙션(펼치기, 탭 전환 등) 시점에 로딩
- React Suspense와 `lazy()`를 결합해 컴포넌트 단위 로딩 구조를 개선 ([Code Splitting](#code-splitting)과 함께 적용)

### 결과

- 초기 화면 진입 속도 향상
- 보고서 평균 조회 시간을 1분 30초~2분에서 **1분 이내**로 단축하는 데 기여

---

<a id="memoization"></a>

## 6. Memoization

**관련 프로젝트**: [홈앤쇼핑 전사 관리 지표 프로젝트](./career.md#homeshopping) · [BI 솔루션 SaaS 전환](./career.md#saas-migration)

### 문제

동일한 조건으로 보고서를 재조회할 때마다 클라이언트와 서버 양쪽에서 동일한 연산을 반복하고 있었고, 계산 비용이 큰 컴포넌트가 필요 이상으로 자주 재계산되고 있었습니다.

### 원인 분석

- 조회 결과나 가공 결과를 캐싱하지 않아, 같은 조건이어도 매번 처음부터 다시 계산하는 구조였습니다.
- React 컴포넌트 트리에서 상위 상태가 바뀔 때마다 하위의 무거운 계산 로직도 함께 재실행되고 있었습니다.

### 해결 방법

- 동일 조건 재조회 시 클라이언트/서버 재연산을 방지하도록 조회·가공 결과를 캐싱
- React DevTools Profiler로 확인한, 실제로 계산 비용이 큰 컴포넌트에만 선택적으로 `useMemo`/`useCallback` 적용 (전역 적용은 지양)

### 결과

- 반복 계산 제거로 보고서 재조회 속도 개선
- 불필요한 리렌더링 감소로 화면 전환 및 인터랙션 응답성 향상

---

<a id="code-splitting"></a>

## 7. Code Splitting

**관련 프로젝트**: [BI 플랫폼 레거시 현대화](./career.md#legacy-modernization) · [BI 솔루션 SaaS 전환](./career.md#saas-migration)

### 문제

하나의 번들에 여러 화면의 코드가 모두 포함되면서, 실제로 필요하지 않은 코드까지 초기 로딩 시점에 함께 다운로드되고 있었습니다.

### 원인 분석

- 라우트·기능 단위로 번들이 분리되어 있지 않아 초기 진입 시 다운로드해야 하는 JS 번들 크기가 컸습니다.

### 해결 방법

- React Suspense와 `lazy()` 기반으로 라우트·기능 단위 코드 스플리팅 적용
- Vite/Webpack 빌드 설정을 조정해 번들 단위를 재구성하고 불필요한 중복 포함을 제거

### 결과

- 초기 번들 크기 감소로 [LCP 개선](#lcp)에 기여
- 화면 진입 응답성 향상

---

<a id="prefetch"></a>

## 8. Prefetch

**관련 프로젝트**: [BI 플랫폼 레거시 현대화](./career.md#legacy-modernization)

### 문제

사용자가 다음 화면으로 이동할 때마다 그 시점부터 데이터를 요청해, 클릭 이후 로딩을 기다려야 하는 경험이 반복됐습니다.

### 원인 분석

- 필요한 시점에만 데이터를 요청하는 구조라, 이동 경로가 어느 정도 예측 가능한 화면에서도 매번 처음부터 요청·대기가 발생했습니다.

### 해결 방법

- 사용자가 다음에 이동할 가능성이 높은 화면의 데이터를 미리 요청해두는 Prefetch 전략 적용
- 중복 호출 방지 로직과 함께 적용해, 미리 가져온 데이터가 있으면 재요청하지 않도록 구성

### 결과

- 네트워크 병목 완화로 화면 전환 시 체감 대기 시간 감소
- [LCP 개선](#lcp) 및 전반적인 초기 로딩 성능 개선에 기여

---

<a id="api-cache"></a>

## 9. API Cache

**관련 프로젝트**: [BI 솔루션 SaaS 전환](./career.md#saas-migration) · [BI 플랫폼 레거시 현대화](./career.md#legacy-modernization)

### 문제

여러 컴포넌트가 동일한 데이터를 각자 조회하면서 중복 네트워크 트래픽이 반복적으로 발생하고 있었습니다.

### 원인 분석

- Chrome DevTools Network 탭으로 확인한 결과, 화면 하나에서 같은 엔드포인트가 여러 번 호출되는 경우가 다수 있었습니다. 컴포넌트 간에 조회 결과를 공유하는 캐시 계층이 없었기 때문입니다.

### 해결 방법

- API를 목적 단위로 분류하고, 캐싱이 가능한 조회(메타 정보 등)에는 캐시 계층을 적용
- 동일 요청이 진행 중이거나 이미 캐시된 경우 재요청하지 않도록 중복 호출 방지 로직 적용

### 결과

- 불필요한 API 호출 제거로 월 API 호출 횟수 **32% 감소**
- 네트워크 병목 완화로 화면 응답성 개선

---

## 요약

| 항목 | 핵심 결과 |
| --- | --- |
| [LCP 개선](#lcp) | 2초 → 0.5초 |
| [React Profiler](#react-profiler) | Commit 시간 약 30% 개선 |
| [Chrome DevTools](#chrome-devtools) | Race Condition 해결 |
| [Virtualized Rendering](#virtualized-rendering) | UI 프리징 제거 |
| [Lazy Loading](#lazy-loading) | 보고서 조회 1분 이내 |
| [Memoization](#memoization) | 반복 연산 제거 |
| [Code Splitting](#code-splitting) | 초기 번들 크기 감소 |
| [Prefetch](#prefetch) | 화면 전환 대기 시간 감소 |
| [API Cache](#api-cache) | API 호출 32% 감소 |

---

📖 함께 보기: [portfolio.md](./portfolio.md) · [career.md](./career.md) · [side-project.md](./side-project.md)
