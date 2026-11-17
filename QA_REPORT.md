# v0.7.20 기술 변경·회귀검수보고서

## 1. 기준본 및 범위
- 제3차시: 사용자가 제공한 `kafv-fishing-village-consultant-main 3차시.zip`의 index.html (v0.7.19 계열, 전체화면 클릭 복귀 포함).
- UI MASTER: 사용자 승인 제4차시 `KAFV_Lesson4_v0.4.9_Standalone_Deploy.zip`의 index.html.
- 제3차시의 이론 화면 좌측 설명부와 부캉이만 변경. 제3차시 고유 교육과정(8/7/5/14 페이지), 미션 탐색, 실습 데이터, 원본 이미지·효과음·QR 루틴 유지.
- 기존 나레이션은 원문 유지. 그림 해설/용어 정의 및 페이지별 질문 34개는 원 강의 내용에 맞춰 새로 편집한 학습보조자료. 기존 퀴즈 20개는 원문 기반. 외부 법령·안전 기준의 최신성 별도 검증 대상.

## 2. 구현
- 기존 제4차시의 부캉이 SVG·팝업 HTML·CSS 및 이동·크기조절 로직을 이식하고 스타일 범위를 제한.
- 제3차시 이론 페이지 키 기반으로 주요 용어를 생성하고, 질문·답변·관련 강의 이동과 연결.
- 단일 HTML 내 지식 DB; 원본 강의·실습·음향의 바이너리 자산 및 기존 스크립트 보존.
- 기존 강사용 토의 질문을 접이 영역에 보존. 사용자 승인 전 신규 버전은 후보본.

## 3. 자동 및 시각 검수
- 실행본 내용을 Chromium에 직접 로딩. 파일 URL은 현재 환경의 브라우저 정책에 의해 차단되어 메모리 로딩으로 검수.
- JavaScript 전체 구문 검사: 통과.
- 원본 스크립트 9개 중 이론 화면을 포함하는 1개만 수정, 나머지 8개 바이트 동일. 원본 CSS 3개 블록 동일.
- 34개 페이지의 원본 나레이션·이미지 디코딩·해설·용어·추천질문·페이지 키 일치.
- 76개 주요 용어, 54개 예상질문 정답 매칭 확인.
- PC 기본 화면·상담창·실습 화면·모바일 상담창 시각 확인.

### 검수 로그 (21개 그룹)
1. PASS — exact HTML startup by browser memory loading
2. PASS — 34/34 lecture pages: original narration, guide, terms, images, suggestions
3. PASS — 76/76 term question lookup
4. PASS — 54/54 exact Q&A
5. PASS — unknown query fallback
6. PASS — term button opens popup and asks
7. PASS — typed question
8. PASS — cross-PART reference opens slide and closes chat
9. PASS — FAB and help
10. PASS — chat drag
11. PASS — chat resize
12. PASS — FAB drag does not open chat
13. PASS — PART 1–4 fullscreen, thumb navigation, image-click restoration
14. PASS — example fullscreen image-click restore
15. PASS — PIP maximize
16. PASS — PIP fullscreen click returns to original panel
17. PASS — theory to original practice world
18. PASS — practice return
19. PASS — mobile popup fits viewport
20. PASS — no Javascript errors
21. PASS — no external asset requests

## 4. 무결성
- 원본 HTML SHA-256: `080f7b31f837ae660c0dd634d3e9371862f2ce4ed110b21874af1e90808a6cf2`
- 배포 HTML SHA-256: `5aa428149819616581232a7c383000a3d5b466b85ec090d1be82f4f12e79e3ba`
- 원본 크기: 16,816,187 bytes
- 배포 크기: 16,882,744 bytes

## 5. 검수 한계
- 메모리 로딩 방식으로 검사했으며 Windows file:// 직접 실행, 실제 GitHub 배포 및 실기기 모바일, 실제 음향 청취, 전체 실습 미션의 전수 수행, 최신 법령·위생기준에 대한 별도 재검증은 미실시.
- 자연어 질문은 내장 사전과 예상질문에 기반한 검색·매칭 방식이며 생성형 AI가 아님. 등록 외 질문은 안내 또는 관련 용어 설명으로 제한.
- 승인 후 기존 GitHub 주소에서 사용자 검수 필요.
