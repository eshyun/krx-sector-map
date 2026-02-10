# KRX Sector Map

KRX(한국거래소) 섹터별 시장 정보를 시각화한 인터랙티브 대시보드입니다. KOSPI와 KOSDAQ 시장의 섹터별 데이터를 트리맵 형태로 제공합니다.
이 Repository는 [KRX Sector Map](https://krx-sector-map.pages.dev/)에서 개인적으로 보기 위해 만든 페이지입니다.

## 주요 기능

- **시장 전환**: KOSPI와 KOSDAQ 시장 간 원활한 전환
- **섹터 시각화**: 각 섹터의 상대적 크기를 트리맵으로 표현
- **반응형 디자인**: 다양한 화면 크기에서 최적의 사용 경험 제공
- **모던 UI**: Material Design 아이콘과 깔끔한 인터페이스

## 파일 구조

```
krx-sector-map/
├── index.html              # 메인 페이지
├── KOSPI_treemap.html      # KOSPI 시장 트리맵
├── KOSDAQ_treemap.html     # KOSDAQ 시장 트리맵
└── README.md               # 프로젝트 문서
```

## 사용 방법

1. `index.html` 파일을 웹 브라우저에서 열기
2. 상단의 KOSPI/KOSDAQ 버튼으로 시장 전환
3. 트리맵에서 각 섹터의 크기와 구성 확인

## 기술 스택

- **HTML5**: 시맨틱 마크업
- **CSS3**: Flexbox 레이아웃, 모던 스타일링
- **JavaScript**: 인터랙티브 기능 구현
- **Material Icons**: Google Material Design 아이콘

## 디자인 특징

- **헤더**: 대시보드 아이콘과 시장 선택 버튼을 한 행에 배치
- **색상 테마**: 다크 블루(#2c3e50) 헤더와 밝은 배경
- **인터랙션**: 부드러운 전환 효과와 호버 상태
- **로딩**: 동적 콘텐츠 로딩 시 로딩 인디케이터 표시

## 브라우저 호환성

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

## 라이선스

MIT License