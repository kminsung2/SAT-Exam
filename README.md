# SAT Exam

과외 학생들을 위한 SAT 수학 온라인 시험 응시 사이트.

선생님이 시험지 파일과 답안을 업로드하면, 학생은 링크 하나로 바로 시험에 응시할 수 있습니다.

**[사이트 바로가기](https://kminsung2.github.io/SAT-Exam/exam.html)**

---

## 개발 배경

과외 수업에서 모의 시험을 진행할 때마다 문제를 직접 출력하거나 pdf파일로 푸는 것에 실제 시험 환경과 차이가 있었습니다. 문항 구성과 채점까지 한 곳에서 처리할 수 있는 도구가 필요했고, 직접 만들었습니다.

---

## 기능

- 관리자 모드에서 시험 및 링크 생성, 정답 설정
- 시험을 URL로 공유 — 학생은 별도 계정 없이 링크만으로 응시
- 자동 채점 및 오답 확인
- 응시 결과 로컬 저장

---

## 기술적 특이사항

시험 데이터를 URL 해시에 Base64로 인코딩하여 공유하는 방식을 사용합니다. 별도 서버나 데이터베이스 없이 단일 HTML 파일로 공유 기능을 구현했습니다.

한글 데이터를 `btoa()`로 인코딩하면 Latin-1 범위를 벗어나 에러가 발생합니다. `encodeURIComponent → unescape → btoa` 순으로 처리해 이 문제를 해결했습니다.

```js
const encoded = btoa(unescape(encodeURIComponent(JSON.stringify(exam))));
const url = location.href.split('#')[0] + '#exam=' + encoded;
```

---

## 기술 스택

HTML / CSS / JavaScript (프레임워크 없음, 단일 파일)

---

## 실행 방법

별도 설치 필요 없습니다. 브라우저에서 `exam.html`을 열거나 위 링크로 접속하면 됩니다.
