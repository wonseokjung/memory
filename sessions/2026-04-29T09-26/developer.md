# 💻 Developer — Next.js 기반 웹사이트 개발 시, Designer가 제공한 Deep Blue/Neon 디자인 시스템과 Tailwind CSS 커스텀 클래스를 100% 반영하여 MVP 구조를 재점검하고 시작하세요.

💻 Developer: 작업 시작합니다.

제공된 Designer의 최종 비주얼 시스템(Deep Blue/Neon)을 100% 반영하여, 수익화 흐름과 신뢰도를 극대화하는 Next.js 기반 MVP 웹사이트의 초기 구조와 핵심 스타일링 컴포넌트를 구현합니다. 모든 클래스는 Tailwind CSS 커스텀 설정을 기반으로 적용됩니다.

### 🚀 MVP 초기 파일 구조 및 스타일 정의

다음은 프로젝트 시작을 위한 초기 설정 파일과 메인 레이아웃 컴포넌트입니다.

**1. `tailwind.config.js` (커스텀 색상 정의)**
Designer가 제시한 컬러 시스템을 Tailwind CSS에 직접 적용하기 위해 커스텀 색상을 정의합니다.

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        'deep-blue': '#0A1931',         // Primary (신뢰) - 배경 및 주요 텍스트
        'dark-slate': '#1C2841',       // Secondary (보조) - 카드 배경
        'neon-cyan': '#00FFFF',        // Accent (행동/미래) - CTA 및 핵심 강조
        'electric-pink': '#FF00FF',    // Highlight (강조) - 특별한 시스템 단계 강조
      },
      fontFamily: {
        sans: ['Inter', 'Poppins'], // 가독성과 현대성을 위한 폰트 설정
      },
      boxShadow: {
        'neon-glow': '0 0 15px rgba(0, 255, 255, 0.7)', // Neon Cyan Glow 효과
      }
    },
  },
  plugins: [],
}
```

**2. `components/Layout.jsx` (최상위 레이아웃 컴포넌트)**
웹사이트 전체에 Deep Blue 배경과 타이포그래피 시스템을 적용하는 기본 구조를 정의합니다.

```jsx
import React from 'react';

// Tailwind CSS 커스텀 클래스를 사용하여 디자인 시스템 적용
const Layout = ({ children }) => {
  return (
    // Primary Color: Deep Blue (#0A1931) 배경 적용
    <div className="min-h-screen bg-deep-blue text-gray-200 font-sans">
      {/* 헤더/네비게이션 바 스타일링 */}
      <header className="bg-dark-slate shadow-lg border-b-4 border-neon-cyan">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex justify-between items-center">
          {/* 브랜드 로고/시스템 설계자 명시 */}
          <h1 className="text-3xl font-bold text-neon-cyan tracking-wider">
            SYSTEM DESIGN CORP
          </h1>
          {/* 네비게이션 링크 (예시) */}
          <nav className="space-x-6 text-sm font-medium">
            <a href="#dashboard" className="hover:text-neon-cyan transition duration-300 border-b border-transparent hover:border-neon-cyan">대시보드</a>
            <a href="#methodology" className="hover:text-neon-cyan transition duration-300 border-b border-transparent hover:border-neon-cyan">방법론</a>
            <a href="#pricing" className="hover:text-neon-cyan transition duration-300 border-b border-transparent hover:border-neon-cyan">가격책</a>
          </nav>
        </div>
      </header>

      {/* 메인 콘텐츠 영역 */}
      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
        {children}
      </main>

      {/* 푸터 (간단하게 적용) */}
      <footer className="mt-12 py-6 border-t border-dark-slate text-center text-xs text-gray-500">
        &copy; {new Date().getFullYear()} SYSTEM DESIGN CORP. All rights reserved. | Powered by System Design Methodology.
      </footer>
    </div>
  );
};

export default Layout;
```

**3. `pages/index.jsx` (초기 랜딩 페이지)**
위에서 정의한 레이아웃을 적용하여 첫 화면을 구성합니다.

```jsx
import Layout from '../components/Layout';

const HomePage = () => {
  return (
    <Layout>
      {/* Hero Section: 시스템 설계자 포지셔닝 강조 */}
      <section className="mb-16 p-8 bg-dark-slate rounded-xl shadow-2xl border-t-4 border-neon-cyan">
        <h2 className="text-5xl font-extrabold mb-4 text-white leading-tight">
          AI 기반 시스템 설계의 미래를 경험하세요.
        </h2>
        <p className="text-lg mb-6 max-w-3xl text-gray-300">
          복잡한 비즈니스 문제를 명확하고 검증된 **시스템 설계 방법론**을 통해 고가치 솔루션으로 전환하는 시스템 설계자(System Designer)의 길.
        </p>
        {/* CTA 버튼: Neon Cyan 강조 */}
        <a 
          href="#methodology" 
          className="inline-block px-10 py-4 text-lg font-bold rounded-full transition duration-300 
                     bg-neon-cyan text-deep-blue shadow-neon-glow hover:shadow-neon-cyan/80"
        >
          시스템 설계 방법론 보기
        </a>
      </section>

      {/* Feature Section: 신뢰도 구축 요소 */}
      <section className="space-y-10">
        {/* Feature 1: 신뢰성 강조 */}
        <div className="p-6 bg-dark-slate rounded-xl shadow-lg border-l-4 border-electric-pink">
          <h3 className="text-2xl font-semibold text-neon-cyan mb-2">신뢰 기반 설계 (Trust-Based Design)</h3>
          <p className="text-gray-300">모든 시스템은 Deep Blue의 신뢰감과 Neon의 혁신성이 결합되어, 잠재 고객에게 강력한 전문성과 미래지향적인 비전을 전달합니다.</p>
        </div>

        {/* Feature 2: 결과 중심 강조 */}
        <div className="p-6 bg-dark-slate rounded-xl shadow-lg border-l-4 border-neon-cyan">
          <h3 className="text-2xl font-semibold text-neon-cyan mb-2">결과 지향적 KPI (Result-Oriented KPIs)</h3>
          <p className="text-gray-300">단순한 자동화를 넘어, 시스템 적용 여부로 성과를 측정하는 명확한 KPI 프레임워크를 제공하여 고가치 판매를 보장합니다.</p>
        </div>

        {/* Feature 3: 포지셔닝 강조 */}
        <div className="p-6 bg-dark-slate rounded-xl shadow-lg border-l-4 border-electric-pink">
          <h3 className="text-2xl font-semibold text-neon-cyan mb-2">시스템 설계자 포지셔닝</h3>
          <p className="text-gray-300">단순한 코딩이 아닌, 시스템적 사고방식(Systemic Thinking)을 판매하여 사용자를 단순 개발자가 아닌 '시스템 설계자'로 포지셔닝합니다.</p>
        </div>
      </section>

    </Layout>
  );
};

export default HomePage;
```

### 📋 실행 방법 요약

1.  **Tailwind 설정 적용:** `tailwind.config.js` 파일에 위에서 정의한 커스텀 색상(`deep-blue`, `neon-cyan`, `electric-pink` 등)을 추가하여 빌드 환경을 준비합니다.
2.  **레이아웃 컴포넌트 구현:** `components/Layout.jsx`를 프로젝트 루트에 생성하고 위에 제공된 코드를 붙여넣습니다.
3.  **홈페이지 구축:** `pages/index.jsx` 파일을 생성하고 위에 제공된 코드를 붙여넣어 MVP의 첫 화면을 완성합니다.

이 초기 구조는 **Deep Blue/Neon 디자인 시스템**과 **시스템 설계자 포지셔닝**이라는 핵심 의사결정 사항을 즉시 시각적으로 반영하며 시작합니다.

📊 평가: 완료 — 요청된 비주얼 시스템을 완벽하게 반영한 Next.js MVP의 기초 코드를 제공했습니다.
📝 다음 단계: 다음으로, `sessions/2026-04-28T07-34/developer.md`에 정의된 **Next.js 스택 기반 MVP 아키텍처 및 데이터베이스 스키마 설계**를 실제 코드 구조로 변환하고 시작합니다.
