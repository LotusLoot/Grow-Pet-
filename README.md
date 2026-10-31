# 펫 부화장 — 올리는 방법

GitHub Pages에 게임을 올리고, Firebase로 저장·랭킹·아레나를 연결하는 순서예요. 둘 다 무료 요금제로 충분해요.

## 폴더 안 파일

| 파일 | 하는 일 |
| --- | --- |
| `index.html` | 게임 본체 |
| `img/` | 몬스터 그림 96장 |
| `firebase-config.js` | Firebase 연결값 (직접 채워야 함) |
| `firestore.rules` | 데이터 보안 규칙 (Firebase에 붙여 넣기) |

## 1단계: Firebase 프로젝트 만들기

1. https://console.firebase.google.com 에 Google 계정으로 들어가요.
2. **프로젝트 만들기** → 이름(예: `pet-hatchery`) → Google 애널리틱스는 꺼도 돼요.

## 2단계: 익명 로그인 켜기

친구들이 가입 없이 각자 기록을 저장하게 해줘요.

1. 왼쪽 메뉴 **빌드 → Authentication → 시작하기**
2. **로그인 방법** 탭 → **익명** → 사용 설정 → 저장

## 3단계: Firestore 데이터베이스 만들기

1. 왼쪽 메뉴 **빌드 → Firestore Database → 데이터베이스 만들기**
2. 위치는 **asia-northeast3 (서울)** 추천
3. **프로덕션 모드**로 시작
4. 다 만들어지면 **규칙** 탭을 열고, 안의 내용을 전부 지운 뒤 `firestore.rules` 파일 내용을 붙여 넣고 **게시**

## 4단계: 연결값 넣기

1. 왼쪽 위 톱니바퀴 → **프로젝트 설정**
2. 아래쪽 **내 앱**에서 웹 아이콘 `</>` 클릭 → 앱 이름 입력 → 등록 (Firebase 호스팅은 체크 안 해도 돼요)
3. 화면에 나오는 `firebaseConfig = { ... }` 안의 값 6개를 `firebase-config.js`의 같은 이름 칸에 복사해 넣어요.

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "pet-hatchery-xxxx.firebaseapp.com",
  projectId: "pet-hatchery-xxxx",
  storageBucket: "pet-hatchery-xxxx.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
```

이 값은 비밀번호가 아니라서 공개돼도 괜찮아요. 데이터는 3단계의 보안 규칙이 지켜줘요.

## 5단계: GitHub에 올리기

1. https://github.com 에서 **New repository** → 이름(예: `pet-hatchery`) → **Public** → Create
2. 저장소 화면에서 **Add file → Upload files**
3. 이 폴더 안의 파일을 전부 끌어다 놓아요. `img` 폴더도 폴더째 끌어 놓으면 돼요.
4. 아래 **Commit changes** 클릭

## 6단계: GitHub Pages 켜기

1. 저장소 **Settings → Pages**
2. **Build and deployment → Source: Deploy from a branch**
3. Branch는 **main**, 폴더는 **/(root)** → Save
4. 1~2분 기다리면 위쪽에 주소가 떠요: `https://아이디.github.io/pet-hatchery/`

이 주소를 친구들에게 보내면 돼요.

## 잘 되는지 확인

- 게임을 열고 **기록(트로피) → 닉네임**을 정해요.
- 1분쯤 뒤 **기록 → 랭킹**에 내 이름이 보이면 연결 성공이에요.
- Firebase 콘솔 → Firestore Database → **데이터** 탭에 `ranks`, `arena`, `data`가 생겨요.

## 안 될 때

- **랭킹이 "서버에 연결되지 않아"라고 나와요**: `firebase-config.js` 값이 맞는지, 2단계 익명 로그인을 켰는지 확인해요.
- **수정했는데 그대로예요**: GitHub에 파일을 다시 올린 뒤 1~2분 기다리고, 브라우저를 새로고침해요.
- **로그인 오류가 나요**: Authentication → 설정 → **승인된 도메인**에 `아이디.github.io`를 추가해요.

## 알아둘 점

- 웹 게임은 코드가 공개돼서, 마음먹으면 자기 기록을 조작할 수 있어요. 보안 규칙이 남의 기록은 못 고치게 막고, 아레나 점수가 10,000점을 넘지 못하게 해 두었어요.
- 기기마다 따로 저장돼요. 폰과 컴퓨터는 다른 사람으로 인식돼요.
- 무료 요금제는 하루 읽기 5만 번, 쓰기 2만 번까지예요. 친구들끼리 하기엔 충분해요.
