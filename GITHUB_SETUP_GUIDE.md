# SpellDeck GitHub 연동 가이드

**설정 대상 계정**: combeewlgns  
**저장소명**: SpellDeck  
**브랜치**: main  

---

## 📋 Step 1: GitHub에서 저장소 생성

1. https://github.com/new 방문 (또는 GitHub → + → New repository)
2. **Repository name**: `SpellDeck`
3. **Description**: `2D Card Game - Unity 6.4`
4. **Public** 선택 (또는 Private 원하는 대로)
5. **.gitignore template**: `Unity` 선택 (이미 생성했지만 확인용)
6. **Add a README file**: 체크 해제 (우리가 만들 예정)
7. **Create repository** 클릭

생성되면 저장소 URL이 보입니다:  
`https://github.com/combeewlgns/SpellDeck.git`

---

## 📋 Step 2: 로컬 Git 설정

Windows PowerShell 또는 Git Bash를 열고 다음 명령을 실행합니다:

```powershell
# spelldeck 폴더로 이동
cd "C:\Users\음지훈\Documents\Claude\Projects\spelldeck"

# Git 초기화
git init --initial-branch=main

# 사용자 정보 설정
git config user.email "combeewlgns@gmail.com"
git config user.name "지훈"

# 글로벌 설정으로 저장 (선택사항)
git config --global user.email "combeewlgns@gmail.com"
git config --global user.name "지훈"
```

---

## 📋 Step 3: 초기 커밋

```powershell
# 모든 파일 스테이징
git add .

# 커밋
git commit -m "Initial commit: SpellDeck project setup with Unity 6.4"

# 상태 확인
git status
```

---

## 📋 Step 4: 원격 저장소 연결

```powershell
# GitHub 저장소를 원격으로 추가
git remote add origin https://github.com/combeewlgns/SpellDeck.git

# 현재 연결된 원격 저장소 확인
git remote -v
```

---

## 📋 Step 5: GitHub에 Push

```powershell
# main 브랜치를 GitHub에 푸시
git branch -M main
git push -u origin main
```

**첫 번째 푸시 시** GitHub 인증이 필요합니다:
- **GitHub 로그인** 창이 나타나면 combeewlgns 계정으로 로그인
- 또는 **Personal Access Token** 사용 (권장)

---

## 🔐 Personal Access Token 설정 (권장)

더 안전한 인증을 위해 Personal Access Token 사용:

### Token 생성하기
1. GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
2. **Generate new token** (classic) 클릭
3. **Token name**: `SpellDeck`
4. **Expiration**: 90 days 또는 No expiration
5. **Scopes** 선택:
   - ✅ `repo` (전체 제어)
   - ✅ `gist`
6. **Generate token** 클릭
7. **토큰 복사** (다시 볼 수 없으니 저장해두기)

### Windows에 Token 저장
```powershell
# Git이 Token을 기억하도록 설정
git config --global credential.helper wincred
```

첫 번째 push 시 사용자명/비밀번호 입력 창:
- 사용자명: `combeewlgns`
- 비밀번호: `생성한_Personal_Access_Token`

---

## 📋 Step 6: README.md 생성 (선택사항)

```powershell
# README.md 생성
echo "# SpellDeck

2D Card Game built with Unity 6.4

## Project Structure
- Assets/ - Game assets and scripts
- Documentation/ - Project documentation
- GDD/ - Game Design Documents

## Getting Started
1. Clone this repository
2. Open with Unity 6.4
3. Open the main scene

## Development
See UNITY_SETUP_GUIDE.md for development setup." > README.md

# 커밋 및 푸시
git add README.md
git commit -m "Add README.md"
git push origin main
```

---

## 🔄 이후 커밋 및 푸시 기본 명령

```powershell
# 변경사항 스테이징
git add .

# 커밋
git commit -m "작업 내용 설명"

# GitHub에 푸시
git push origin main

# 최신 변경사항 가져오기
git pull origin main
```

---

## ⚠️ Unity 프로젝트 구조 시 주의사항

### Library/ 폴더 제외 확인
`.gitignore`에 다음이 포함되어 있는지 확인:
```
Library/
Temp/
obj/
Obj/
Build/
Builds/
```

### 큰 파일 제외 (Git LFS 권장)
바이너리 파일이 크면 Git LFS 사용:
```powershell
# Git LFS 설치 후
git lfs install

# 추적할 파일 종류 지정
git lfs track "*.png"
git lfs track "*.psd"
git lfs track "Assets/Sprites/**"
```

---

## ✅ 체크리스트

- [ ] GitHub 저장소 생성 완료
- [ ] 로컬 Git 초기화 완료
- [ ] 사용자 정보 설정 완료
- [ ] 초기 커밋 완료
- [ ] 원격 저장소 연결 완료
- [ ] GitHub에 성공적으로 push 완료
- [ ] GitHub 저장소에서 파일 확인

---

## 📞 문제 해결

### "fatal: bad config line 1"
```powershell
# .git/config 파일 재설정
rm -Force -Recurse .git
git init --initial-branch=main
git config user.email "combeewlgns@gmail.com"
git config user.name "지훈"
```

### "Permission denied"
SSH 방식으로 변경:
```powershell
# SSH 키 생성 (처음 1회만)
ssh-keygen -t ed25519 -C "combeewlgns@gmail.com"

# GitHub Settings에 공개키 등록 후 사용
git remote set-url origin git@github.com:combeewlgns/SpellDeck.git
```

---

**다음 단계**: Unity 프로젝트를 생성하고 Assets 폴더를 추가한 후 커밋하기
