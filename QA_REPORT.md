# KAFV 제3차시 전체화면 복귀 기능 정밀 수정 QA 보고

기준일: 2026-11-16
입력 원본: `index(3).html` / 파일 내부 버전 `v0.7.19 DEV`
결과물: `index.html`

## 원인
- 전체화면은 브라우저의 Fullscreen API (`requestFullscreen` / `exitFullscreen`)를 사용
- Esc로 복귀 가능(사용자의 실제 브라우저 조작 확인)
- 전체화면 상태에서 이론 이미지를 다시 클릭하면 `expandImage` 이벤트가 `openFloating`을 실행하도록 되어 있어 클릭 복귀가 구현되지 않았음
- PART 4의 HTML 실무예제(`.example-visual`)는 애초에 일반 이미지 버튼이 아니므로 클릭 복귀 이벤트가 없었음

## 변경 사항
- 원본 코드·이미지·강의자료는 수정하지 않음
- HTML 맨 끝에 독립된 클릭 복귀 이벤트 리스너 1개만 추가
- 전체화면 이론 이미지 및 HTML 실무예제 화면 클릭 → `exitFullscreen()`
- PIP 전체화면 이미지 클릭 → 전체화면 종료 후 원래 교재 패널로 복귀
- 썸네일·버튼·입력·링크는 클릭 복귀 대상에서 제외
- 브라우저의 기존 Esc 동작은 변경하지 않음

## 브라우저 자동 검수 결과 (Chromium Headless)
| 검수 항목 | 결과 |
|---|---|
| PART 1 전체화면 진입 → 강의 이미지 클릭 복귀 | PASS |
| PART 2 전체화면 진입 → 강의 이미지 클릭 복귀 | PASS |
| PART 3 전체화면 진입 → 강의 이미지 클릭 복귀 | PASS |
| PART 4 전체화면 진입 → 강의 이미지 클릭 복귀 | PASS |
| PART 4 HTML 실무예제 전체화면 → 예제 클릭 복귀 | PASS |
| PIP 전체화면 → 강의 이미지 클릭 → 원래 패널 복귀 | PASS |
| 전체화면 썸네일 클릭 시 화면 유지 | PASS |
| Esc 키를 이용한 복귀 | 사용자가 실제 브라우저에서 확인, 자동화에서는 미검증(Headless 제한) |

## 원본 보존·무결성
원본 SHA-256: `fd4989dff9dcaf3cecab5587dab5d0b445d8fefdbec62223d6c8ffb43bbc00cf`
수정본 SHA-256: `080f7b31f837ae660c0dd634d3e9371862f2ce4ed110b21874af1e90808a6cf2`
변경 범위: HTML 종료 태그 직전에 독립 스크립트 삽입; 기존 본문과 자료는 원본과 완전 일치.

## 배포
1. 기존 GitHub 저장소 `kafv-fishing-village-consultant`에서 기존 `index.html`을 백업한다.
2. 이 ZIP의 `index.html`을 저장소 루트에 업로드하여 덮어쓴다.
3. GitHub Pages 배포 후 `?step=theory`로 접속해 PART 1~4 전체화면, 이미지 클릭·Esc, 썸네일, PIP, 실습 연결을 실제 기기에서 최종 검수한다.
4. 원본의 다른 기능을 변경하지 않았지만 전체 실기기 회귀검수 완료 전에는 온라인 최종 PASS를 선언하지 않는다.
