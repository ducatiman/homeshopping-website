# 드로어 메뉴 상세 설계 문서

## 📋 목차
1. [개요](#개요)
2. [메뉴 구조](#메뉴-구조)
3. [디자인 스펙](#디자인-스펙)
4. [레이아웃 구조](#레이아웃-구조)
5. [인터랙션 및 애니메이션](#인터랙션-및-애니메이션)
6. [반응형 디자인](#반응형-디자인)
7. [접근성](#접근성)
8. [구현 상세](#구현-상세)

---

## 1. 개요

### 1.1 목적
- 왼쪽에서 슬라이드되는 드로어 메뉴 구현
- 현재 홈페이지 디자인과 조화로운 통합
- 모바일 우선 반응형 디자인

### 1.2 참고 사이트 분석
- **참고 URL**: https://m.xn--539an7vgta625d.com/#none
- **특징**: 
  - 왼쪽 슬라이드 드로어
  - 카테고리 기반 메뉴 구조
  - 오버레이 배경
  - 부드러운 애니메이션

---

## 2. 메뉴 구조

### 2.1 메뉴 계층 구조

```
📱 메뉴
│
├─ 🏠 홈
│  └─ index.html
│
├─ 📦 카테고리
│  ├─ 이달의 추천상품
│  │  └─ index.html (스크롤 이동)
│  │
│  ├─ 프리미엄 밀키트
│  │  ├─ 청양식 닭갈비 밀키트 → product1.html
│  │  ├─ 청양식 한우육개장 밀키트 → product2.html
│  │  ├─ 표고와사비장 → product3.html
│  │  ├─ 청양식 한우불고기 밀키트 → product4.html
│  │  ├─ 청양식 된장찌개 밀키트 → product5.html
│  │  └─ 청양식 두부전골 밀키트 → product6.html
│  │
│  └─ 전체 상품 보기
│     └─ index.html (스크롤 이동)
│
├─ 📞 고객센터
│  ├─ 공지사항 (준비중)
│  ├─ 상품문의 (준비중)
│  └─ 1:1 문의 (준비중)
│
└─ ℹ️ 회사소개
   └─ 브랜드 스토리 (준비중)
```

### 2.2 메뉴 항목 상세

#### 2.2.1 주요 메뉴
| 메뉴명 | 링크 | 아이콘 | 설명 |
|--------|------|--------|------|
| 홈 | `index.html` | 🏠 | 메인 페이지로 이동 |
| 카테고리 | `#` | 📦 | 카테고리 메뉴 확장 |
| 고객센터 | `#` | 📞 | 고객센터 메뉴 확장 |
| 회사소개 | `#` | ℹ️ | 회사소개 메뉴 확장 |

#### 2.2.2 서브 메뉴
- **카테고리 하위**
  - 이달의 추천상품
  - 프리미엄 밀키트 (6개 상품)
  - 전체 상품 보기

- **고객센터 하위**
  - 공지사항
  - 상품문의
  - 1:1 문의

---

## 3. 디자인 스펙

### 3.1 색상 팔레트

#### 3.1.1 기본 색상
```css
/* 배경색 */
--drawer-bg: #ffffff;              /* 드로어 배경 */
--drawer-header-bg: #fcfbf9;      /* 드로어 헤더 배경 */
--overlay-bg: rgba(0, 0, 0, 0.5);  /* 오버레이 배경 */

/* 텍스트 색상 */
--text-primary: #000000;           /* 주요 텍스트 */
--text-secondary: #666666;          /* 보조 텍스트 */
--text-tertiary: #999999;          /* 3차 텍스트 */

/* 강조 색상 */
--accent-color: #4caf50;           /* 브랜드 녹색 */
--accent-hover: #45a049;           /* 호버 시 녹색 */
--border-color: #e5e5e5;           /* 테두리 색상 */
--border-light: #e0ede1;          /* 연한 테두리 */

/* 인터랙션 색상 */
--menu-hover-bg: #f8f8f8;          /* 메뉴 호버 배경 */
--menu-active-bg: #f0f7f0;         /* 메뉴 활성 배경 */
```

#### 3.1.2 그라데이션
```css
/* 버튼 그라데이션 */
--gradient-primary: linear-gradient(135deg, #4caf50 0%, #66bb6a 100%);
--gradient-hover: linear-gradient(135deg, #45a049 0%, #5cb85c 100%);
```

### 3.2 타이포그래피

```css
/* 폰트 패밀리 */
font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

/* 폰트 크기 */
--font-size-xs: 12px;      /* 작은 텍스트 */
--font-size-sm: 14px;      /* 기본 텍스트 */
--font-size-md: 16px;      /* 중간 텍스트 */
--font-size-lg: 18px;      /* 큰 텍스트 */
--font-size-xl: 20px;      /* 매우 큰 텍스트 */
--font-size-2xl: 24px;     /* 헤더 텍스트 */

/* 폰트 굵기 */
--font-weight-normal: 400;
--font-weight-medium: 500;
--font-weight-semibold: 600;
--font-weight-bold: 700;

/* 줄 간격 */
--line-height-tight: 1.2;
--line-height-normal: 1.5;
--line-height-relaxed: 1.8;
```

### 3.3 간격 시스템

```css
/* 패딩 */
--spacing-xs: 8px;
--spacing-sm: 12px;
--spacing-md: 16px;
--spacing-lg: 24px;
--spacing-xl: 32px;
--spacing-2xl: 40px;

/* 마진 */
--margin-xs: 8px;
--margin-sm: 12px;
--margin-md: 16px;
--margin-lg: 24px;
--margin-xl: 32px;
```

### 3.4 그림자

```css
/* 드로어 그림자 */
--shadow-drawer: 2px 0 8px rgba(0, 0, 0, 0.1);

/* 메뉴 항목 호버 그림자 */
--shadow-menu-hover: 0 2px 4px rgba(76, 175, 80, 0.1);
```

### 3.5 테두리

```css
/* 테두리 반경 */
--radius-sm: 4px;
--radius-md: 8px;
--radius-lg: 12px;

/* 테두리 두께 */
--border-width-thin: 1px;
--border-width-medium: 2px;
```

---

## 4. 레이아웃 구조

### 4.1 HTML 구조

```html
<!-- 햄버거 메뉴 버튼 (헤더에 추가) -->
<button class="menu-toggle" aria-label="메뉴 열기">
  <span class="menu-icon"></span>
</button>

<!-- 드로어 메뉴 -->
<nav class="drawer" id="drawerMenu" aria-label="주요 메뉴">
  <!-- 드로어 헤더 -->
  <div class="drawer-header">
    <div class="drawer-logo">
      <img src="./images/ic_farm.gif" alt="정산농협">
      <h2>청양식 밀키트 전문몰</h2>
    </div>
    <button class="drawer-close" aria-label="메뉴 닫기">
      <span class="close-icon">×</span>
    </button>
  </div>

  <!-- 드로어 메뉴 본문 -->
  <div class="drawer-body">
    <ul class="drawer-menu">
      <!-- 홈 -->
      <li class="menu-item">
        <a href="index.html" class="menu-link">
          <span class="menu-icon">🏠</span>
          <span class="menu-text">홈</span>
        </a>
      </li>

      <!-- 카테고리 (확장 가능) -->
      <li class="menu-item menu-item-expandable">
        <button class="menu-link menu-toggle-sub" aria-expanded="false">
          <span class="menu-icon">📦</span>
          <span class="menu-text">카테고리</span>
          <span class="menu-arrow">›</span>
        </button>
        <ul class="submenu">
          <li><a href="#recommended">이달의 추천상품</a></li>
          <li class="submenu-item-group">
            <span class="submenu-group-title">프리미엄 밀키트</span>
            <ul class="submenu-nested">
              <li><a href="product1.html">청양식 닭갈비 밀키트</a></li>
              <li><a href="product2.html">청양식 한우육개장 밀키트</a></li>
              <li><a href="product3.html">표고와사비장</a></li>
              <li><a href="product4.html">청양식 한우불고기 밀키트</a></li>
              <li><a href="product5.html">청양식 된장찌개 밀키트</a></li>
              <li><a href="product6.html">청양식 두부전골 밀키트</a></li>
            </ul>
          </li>
          <li><a href="#products">전체 상품 보기</a></li>
        </ul>
      </li>

      <!-- 고객센터 (확장 가능) -->
      <li class="menu-item menu-item-expandable">
        <button class="menu-link menu-toggle-sub" aria-expanded="false">
          <span class="menu-icon">📞</span>
          <span class="menu-text">고객센터</span>
          <span class="menu-arrow">›</span>
        </button>
        <ul class="submenu">
          <li><a href="#notice">공지사항</a></li>
          <li><a href="#inquiry">상품문의</a></li>
          <li><a href="#contact">1:1 문의</a></li>
        </ul>
      </li>

      <!-- 회사소개 -->
      <li class="menu-item">
        <a href="#about" class="menu-link">
          <span class="menu-icon">ℹ️</span>
          <span class="menu-text">회사소개</span>
        </a>
      </li>
    </ul>
  </div>

  <!-- 드로어 푸터 (선택사항) -->
  <div class="drawer-footer">
    <p class="drawer-footer-text">청양식 밀키트 전문몰</p>
    <p class="drawer-footer-text">국산 재료로 만든 프리미엄 밀키트</p>
  </div>
</nav>

<!-- 오버레이 -->
<div class="drawer-overlay" id="drawerOverlay" aria-hidden="true"></div>
```

### 4.2 드로어 크기

#### 모바일 (< 768px)
- **너비**: 280px ~ 320px (화면의 80%)
- **최대 너비**: 320px
- **높이**: 100vh (전체 화면)

#### 태블릿 (768px ~ 1024px)
- **너비**: 320px ~ 360px
- **높이**: 100vh

#### 데스크톱 (> 1024px)
- **너비**: 360px ~ 400px
- **높이**: 100vh

### 4.3 헤더 통합

현재 헤더 구조에 햄버거 버튼 추가:

```html
<div class="header">
  <div class="container">
    <!-- 햄버거 버튼 추가 -->
    <button class="menu-toggle" aria-label="메뉴 열기">
      <span class="menu-icon">☰</span>
    </button>
    
    <div class="header-logo-container">
      <img src="./images/ic_farm.gif" alt="정산농협" class="header-logo-img">
      <h1>청양식 밀키트 전문몰</h1>
    </div>
    <p>국산 재료로 만든 프리미엄 밀키트를 만나보세요</p>
  </div>
</div>
```

---

## 5. 인터랙션 및 애니메이션

### 5.1 드로어 열기/닫기

#### 5.1.1 열기 애니메이션
```css
/* 초기 상태 (닫힘) */
.drawer {
  transform: translateX(-100%);
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* 열린 상태 */
.drawer.drawer-open {
  transform: translateX(0);
}

/* 오버레이 */
.drawer-overlay {
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.drawer-overlay.active {
  opacity: 1;
  visibility: visible;
}
```

#### 5.1.2 닫기 애니메이션
- 동일한 애니메이션 역방향
- `transform: translateX(-100%)`로 복귀
- 오버레이 페이드 아웃

### 5.2 서브메뉴 확장/축소

```css
/* 서브메뉴 초기 상태 */
.submenu {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease;
}

/* 확장된 상태 */
.menu-item-expandable.expanded .submenu {
  max-height: 1000px; /* 충분히 큰 값 */
}

/* 화살표 회전 */
.menu-arrow {
  transition: transform 0.3s ease;
}

.menu-item-expandable.expanded .menu-arrow {
  transform: rotate(90deg);
}
```

### 5.3 메뉴 항목 호버 효과

```css
.menu-link {
  transition: background-color 0.2s ease, color 0.2s ease;
}

.menu-link:hover {
  background-color: var(--menu-hover-bg);
  color: var(--accent-color);
}

.menu-link:active {
  background-color: var(--menu-active-bg);
}
```

### 5.4 터치 제스처 (모바일)

- **스와이프 오른쪽**: 드로어 열기
- **스와이프 왼쪽**: 드로어 닫기
- **오버레이 탭**: 드로어 닫기

---

## 6. 반응형 디자인

### 6.1 브레이크포인트

```css
/* 모바일 */
@media (max-width: 767px) {
  /* 드로어 너비: 280px */
}

/* 태블릿 */
@media (min-width: 768px) and (max-width: 1023px) {
  /* 드로어 너비: 320px */
}

/* 데스크톱 */
@media (min-width: 1024px) {
  /* 드로어 너비: 360px */
}
```

### 6.2 헤더 버튼 위치

#### 모바일
- 왼쪽 상단
- 고정 위치 (`position: fixed`)
- z-index: 1000

#### 데스크톱
- 왼쪽 상단 또는 헤더 내부
- 선택 가능

### 6.3 폰트 크기 조정

```css
/* 모바일 */
.drawer-header h2 {
  font-size: 20px;
}

.menu-text {
  font-size: 16px;
}

/* 데스크톱 */
@media (min-width: 1024px) {
  .drawer-header h2 {
    font-size: 24px;
  }
  
  .menu-text {
    font-size: 18px;
  }
}
```

---

## 7. 접근성

### 7.1 ARIA 속성

```html
<!-- 드로어 메뉴 -->
<nav class="drawer" 
     id="drawerMenu" 
     aria-label="주요 메뉴"
     aria-hidden="true">

<!-- 메뉴 토글 버튼 -->
<button class="menu-toggle" 
        aria-label="메뉴 열기"
        aria-expanded="false"
        aria-controls="drawerMenu">

<!-- 서브메뉴 토글 -->
<button class="menu-toggle-sub" 
        aria-expanded="false"
        aria-controls="submenu-category">
```

### 7.2 키보드 네비게이션

- **Tab**: 메뉴 항목 간 이동
- **Enter/Space**: 메뉴 항목 선택 또는 확장
- **Escape**: 드로어 닫기
- **Arrow Down/Up**: 서브메뉴 내 이동

### 7.3 포커스 관리

```javascript
// 드로어 열릴 때
- 첫 번째 메뉴 항목에 포커스
- body 스크롤 잠금

// 드로어 닫힐 때
- 메뉴 토글 버튼에 포커스 복귀
- body 스크롤 해제
```

### 7.4 스크린 리더 지원

- 의미 있는 링크 텍스트
- 아이콘에 `aria-hidden="true"`
- 상태 변경 시 `aria-live` 영역 업데이트

---

## 8. 구현 상세

### 8.1 CSS 클래스 구조

```css
/* 드로어 컨테이너 */
.drawer { }
.drawer.drawer-open { }

/* 드로어 헤더 */
.drawer-header { }
.drawer-logo { }
.drawer-close { }

/* 드로어 본문 */
.drawer-body { }
.drawer-menu { }

/* 메뉴 항목 */
.menu-item { }
.menu-item-expandable { }
.menu-item-expandable.expanded { }
.menu-link { }
.menu-icon { }
.menu-text { }
.menu-arrow { }

/* 서브메뉴 */
.submenu { }
.submenu-item-group { }
.submenu-group-title { }
.submenu-nested { }

/* 오버레이 */
.drawer-overlay { }
.drawer-overlay.active { }

/* 헤더 버튼 */
.menu-toggle { }
.menu-toggle.active { }
```

### 8.2 JavaScript 기능

#### 8.2.1 핵심 함수

```javascript
// 드로어 열기
function openDrawer() {
  // 드로어 열기
  // 오버레이 표시
  // body 스크롤 잠금
  // 포커스 관리
  // ARIA 속성 업데이트
}

// 드로어 닫기
function closeDrawer() {
  // 드로어 닫기
  // 오버레이 숨김
  // body 스크롤 해제
  // 포커스 복귀
  // ARIA 속성 업데이트
}

// 서브메뉴 토글
function toggleSubmenu(button) {
  // 확장/축소
  // 화살표 회전
  // ARIA 속성 업데이트
}
```

#### 8.2.2 이벤트 리스너

```javascript
// 햄버거 버튼 클릭
menuToggle.addEventListener('click', openDrawer);

// 닫기 버튼 클릭
closeButton.addEventListener('click', closeDrawer);

// 오버레이 클릭
overlay.addEventListener('click', closeDrawer);

// ESC 키
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape' && drawer.classList.contains('drawer-open')) {
    closeDrawer();
  }
});

// 서브메뉴 토글
submenuToggles.forEach(toggle => {
  toggle.addEventListener('click', () => toggleSubmenu(toggle));
});
```

### 8.3 성능 최적화

#### 8.3.1 CSS 최적화
```css
/* GPU 가속 활용 */
.drawer {
  will-change: transform;
  transform: translateX(-100%);
}

/* 리플로우 최소화 */
.drawer-body {
  contain: layout style paint;
}
```

#### 8.3.2 JavaScript 최적화
- 이벤트 위임 사용
- 디바운싱/쓰로틀링 (필요시)
- 메모리 누수 방지 (이벤트 리스너 정리)

### 8.4 브라우저 호환성

#### 지원 브라우저
- Chrome (최신 2개 버전)
- Safari (최신 2개 버전)
- Firefox (최신 2개 버전)
- Edge (최신 2개 버전)
- 모바일 브라우저 (iOS Safari, Chrome Mobile)

#### 폴백
- CSS Grid → Flexbox
- `will-change` → 일반 transform
- Custom Properties → 하드코딩 값

---

## 9. 구현 체크리스트

### 9.1 HTML
- [ ] 햄버거 버튼 추가
- [ ] 드로어 메뉴 구조 생성
- [ ] ARIA 속성 추가
- [ ] 시맨틱 HTML 사용

### 9.2 CSS
- [ ] 드로어 기본 스타일
- [ ] 애니메이션 정의
- [ ] 반응형 미디어 쿼리
- [ ] 호버 효과
- [ ] 접근성 스타일

### 9.3 JavaScript
- [ ] 드로어 열기/닫기 로직
- [ ] 서브메뉴 토글 기능
- [ ] 키보드 이벤트 처리
- [ ] 포커스 관리
- [ ] 터치 제스처 (선택사항)

### 9.4 테스트
- [ ] 모바일 디바이스 테스트
- [ ] 태블릿 디바이스 테스트
- [ ] 데스크톱 브라우저 테스트
- [ ] 키보드 네비게이션 테스트
- [ ] 스크린 리더 테스트
- [ ] 성능 테스트

---

## 10. 향후 확장 가능성

### 10.1 추가 기능
- 검색 기능 통합
- 사용자 계정 메뉴
- 장바구니 링크
- 최근 본 상품

### 10.2 개선 사항
- 애니메이션 커스터마이징 옵션
- 다크 모드 지원
- 다국어 지원
- 메뉴 즐겨찾기

---

## 📝 참고사항

- 이 설계는 현재 프로젝트의 디자인 시스템과 일관성을 유지합니다
- 모든 색상과 간격은 기존 스타일 가이드를 따릅니다
- 구현 시 접근성과 성능을 최우선으로 고려합니다
- 모바일 우선 접근 방식을 채택합니다

---

**작성일**: 2025-01-27  
**버전**: 1.0  
**상태**: 설계 완료

