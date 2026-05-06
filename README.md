# tutoring scheduler

과외 수업 일정, 학생 정보, 정산 내역을 한 곳에서 관리하는 웹 어플리케이션

## 주요 기능

- 월별 캘린더에서 수업 일정 확인
- 학생별 수업 등록 및 삭제
- 여러 날짜에 같은 수업을 한 번에 등록하는 일괄 등록
- 수업별 간단 메모 작성
- 날짜별 메모 작성 및 메모가 있는 날짜 표시
- 학생별 급여일 기준 정산 주기 확인
- 수업 횟수, 총 수업 시간, 예상 수입 계산
- GitHub 저장소의 `data.json`을 이용한 데이터 동기화
- 모바일 홈 화면에 설치 가능한 PWA 지원

## 사용 방법

1. 사이트에 접속합니다.
2. 처음 실행 시 GitHub Personal Access Token을 입력합니다.
3. 학생 관리 탭에서 학생 이름, 과목, 월 급여, 급여일을 등록합니다.
4. 캘린더에서 날짜를 선택한 뒤 수업을 추가합니다.
5. 필요한 경우 날짜 메모 또는 수업별 메모를 작성합니다.
6. 정산 탭에서 학생별 정산 주기와 예상 수입을 확인합니다.

## GitHub Token 안내

이 앱은 별도의 서버 없이 GitHub API를 사용해 `data.json` 파일에 데이터를 저장합니다.

토큰은 사용자의 브라우저 `localStorage`에만 저장됩니다. GitHub에 저장되는 데이터는 학생 정보, 수업 기록, 날짜 메모입니다.

토큰에는 이 저장소의 파일을 읽고 쓸 수 있는 권한이 필요합니다.

## 파일 구조

```text
.
├── index.html      # 앱 전체 UI와 로직
├── manifest.json   # PWA 설정
├── sw.js           # 오프라인 캐시용 service worker
├── data.json       # GitHub 동기화 데이터
├── icon-192.png    # PWA 아이콘
└── icon-512.png    # PWA 아이콘
```

## 로컬 실행

정적 HTML 앱이라 별도 빌드 과정은 없습니다.

```bash
open index.html
```

또는 간단한 로컬 서버로 실행할 수 있습니다.

```bash
python3 -m http.server 8000
```

이후 브라우저에서 아래 주소로 접속합니다.

```text
http://localhost:8000
```

## 배포

GitHub Pages로 배포할 수 있습니다.

일반적인 배포 흐름은 다음과 같습니다.

```bash
git add .
git commit -m "Update app"
git push
```

GitHub Pages가 활성화되어 있다면 `main` 브랜치의 최신 내용이 사이트에 반영됩니다.

## 데이터 형식

`data.json`은 다음 형태의 데이터를 저장합니다.

```json
{
  "students": [],
  "sessions": {},
  "dateNotes": {}
}
```

- `students`: 학생 정보
- `sessions`: 날짜별 수업 기록
- `dateNotes`: 날짜별 메모

## 기술 스택

- HTML
- CSS
- React UMD
- htm
- GitHub Contents API
- Service Worker
- Web App Manifest
