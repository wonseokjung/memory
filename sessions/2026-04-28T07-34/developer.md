# 💻 Developer — Business에서 정의된 요구사항과 Designer의 비주얼 가이드라인을 기반으로 Next.js 스택을 사용한 초기 MVP 아키텍처 및 데이터베이스 스키마 설계를 즉시 시작해줘.

💻 Developer: 작업 시작합니다.

요청하신 대로, **시스템 설계자로서의 명료함과 수익화 흐름을 극대화**하는 것을 목표로 Next.js 기반의 초기 MVP 아키텍처 및 데이터베이스 스키마 설계를 즉시 시작합니다. 비주얼 가이드라인(Deep Blue/Neon)과 비즈니스 요구사항(System Blueprint, Deep Dive Hub)을 반영하여 설계합니다.

---

## 1. MVP 기술 스택 및 아키텍처 설계 (Next.js Stack & Architecture)

시스템의 확장성과 수익화 흐름(Step 2: 신뢰 구축, Step 3: 전환)에 중점을 두어 Next.js 기반의 풀스택 구조를 제안합니다.

### A. 스택 선택 (Tech Stack Selection)
*   **프레임워크:** Next.js (App Router 사용 권장)
    *   *이유:* 서버 컴포넌트와 라우팅을 통해 강력한 성능과 SEO 최적화(Step 1: 인지 및 유입)를 확보하며, 수익화에 필수적인 빠른 배포 속도를 제공합니다.
*   **스타일링:** Tailwind CSS + Custom CSS Modules
    *   *이유:* Designer가 확정한 네온/딥 블루의 시각적 가이드라인을 빠르고 일관성 있게 구현하기 위함입니다.
*   **데이터베이스 (DB):** PostgreSQL 또는 Supabase (PostgreSQL 기반)
    *   *이유:* 구조화된 시스템 설계와 데이터 무결성이 중요하므로 관계형 데이터베이스가 가장 적합합니다. 초기 MVP는 Supabase를 통해 백엔드 및 인증 기능을 빠르게 구축하여 개발 속도를 높입니다.

### B. 아키텍처 다이어그램 (Conceptual Flow)
시스템은 크게 세 부분으로 나뉘며, 모든 흐름은 **데이터 파이프라인**을 통해 연결됩니다.

1.  **Presentation Layer (Frontend - Next.js):** 사용자와 상호작용하고 디자인을 시각화합니다.
2.  **Application Layer (API/Logic - Next.js Server Actions / Server Components):** 데이터 처리, 권한 확인, 렌더링 로직을 담당합니다.
3.  **Data Layer (Database - PostgreSQL/Supabase):** 모든 시스템 설계와 콘텐츠를 영구적으로 저장합니다.

### C. 초기 파일 구조 (Initial File Structure)
다음과 같이 폴더 및 파일 구조를 설정하여 체계적인 개발 환경을 구축합니다.

```
/nextjs-ai-system-platform
├── /app/                     # Next.js App Router 핵심 경로
│   ├── (main)/              # Layouts and main navigation groups
│   │   ├── layout.tsx
│   │   └── page.tsx         # Home Page (Hero Section)
│   ├── api/                 # Backend API Routes (Server Actions 대체 가능)
│   ├── dashboard/          # User-specific content area (Future)
│   └── globals.css         # Global styles (Tailwind setup + Custom Neon)
├── /components/             # 재사용 가능한 UI 컴포넌트 (Designer Style)
│   ├── Header.tsx
│   ├── BlueprintCard.tsx    # System Blueprint 카드 컴포넌트
│   └── NeonButton.tsx       # 네온 색상 버튼 컴포넌트
├── /lib/                     # 데이터베이스 및 API 연결 로직
│   └── supabaseClient.ts    # Supabase 클라이언트 초기화
├── /public/                  # 정적 에셋 (Images, Fonts)
├── /prisma/                  # (선택 사항: ORM 사용 시) 스키마 관리
├── package.json
└── next.config.js
```

---

## 2. 데이터베이스 스키마 설계 (PostgreSQL / Supabase Schema)

핵심 요구사항인 **'System Blueprint Index'**와 **'Deep Dive Article Hub'**를 중심으로 최소한의 테이블을 설계합니다.

### A. `blueprints` 테이블 (시스템 설계 인덱스)
이 테이블은 웹사이트의 핵심 권위 자산이며, Step 2(신뢰 구축)의 기반이 됩니다.

| 필드명 | 데이터 타입 | 제약 조건 | 설명 | 비고 |
| :--- | :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | 고유 식별자 | |
| `title` | VARCHAR(255) | NOT NULL | 시스템/워크플로우 제목 (H1 기준) | |
| `slug` | VARCHAR(255) | UNIQUE, NOT NULL | URL에 사용될 고유 슬러그 | SEO 최적화 |
| `description` | TEXT | NOT NULL | 시스템의 핵심 설계 논리 요약 | |
| `status` | VARCHAR(50) | DEFAULT 'draft' | 콘텐츠 상태 (Draft, Published, Archived) | 관리 용이성 |
| `category` | VARCHAR(100) | NULL | 분류 (예: AI Automation, Data Pipeline) | 필터링용 |
| `published_at` | TIMESTAMP | NULL | 게시 일시 | |
| `featured_image_url`| TEXT | NULL | 대표 이미지 경로 | Designer 가이드 준수 |

### B. `articles` 테이블 (심층 분석 허브)
이 테이블은 각 Blueprint에 대한 구체적인 구현 과정(Step 3: 전환)을 담습니다.

| 필드명 | 데이터 타입 | 제약 조건 | 설명 | 비고 |
| :--- | :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | 고유 식별자 | |
| `blueprint_id` | INTEGER | NOT NULL, REFERENCES blueprints(id) | 연결된 시스템 설계 ID | 관계 설정 |
| `title` | VARCHAR(255) | NOT NULL | 심층 분석 기사 제목 | |
| `content` | TEXT | NOT NULL | 본문 내용 (마크다운 또는 Rich Text) | |
| `author_id` | INTEGER | REFERENCES users(id) | 작성자 ID (향후 사용자 시스템 도입 시) | |
| `reading_time` | INTEGER | NULL | 예상 독서 시간 (분) | |
| `published_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | 게시 일시 | |

### C. `users` 테이블 (사용자 및 수익화 기반)
향후 멤버십 또는 유료 상품 판매를 위한 최소한의 사용자 데이터 구조입니다.

| 필드명 | 데이터 타입 | 제약 조건 | 설명 | 비고 |
| :--- | :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | 고유 식별자 | |
| `email` | VARCHAR(255) | UNIQUE, NOT NULL | 사용자 이메일 | 로그인/구독 |
| `name` | VARCHAR(100) | NOT NULL | 사용자 이름 | |
| `role` | VARCHAR(50) | DEFAULT 'subscriber' | 사용자 역할 (예: Free User, Premium Member) | 수익화 연동 |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | 가입 일시 | |

---

📝 다음 단계 제안:
Next.js 프로젝트 환경 설정 및 Supabase 초기 연결을 위한 필수 파일(`package.json`, `.env.local`, `lib/supabaseClient.ts`)을 생성하고, Designer가 제시한 컬러 팔레트와 타이포그래피를 적용하는 글로벌 CSS 설정을 완료합니다.
