# SpellDeck Unity 프로젝트 초기설정 가이드

**작성일**: 2026-05-31  
**Unity 버전**: 6.4 (6000.4.9f1)  
**프로젝트 유형**: 2D 카드 게임

---

## 1. 환경 설정

### 필수 요구사항
- Unity 6.4 (6000.4.9f1) 이상
- Visual Studio Code 또는 Visual Studio (C# 개발)
- Git (버전 관리)

### Unity Hub를 통한 프로젝트 생성 절차
1. Unity Hub 실행
2. **New Project** → **2D (Built-in)** 선택 (또는 **2D URP** for 추가 그래픽 기능)
3. 프로젝트명: `SpellDeck`
4. 저장 위치: `C:\Users\음지훈\Documents\Claude\Projects\spelldeck`
5. **Create** 클릭

---

## 2. 폴더 구조

```
Assets/
├── Scenes/              # 게임 씬 (메인, 카드 선택, 배틀 등)
├── Scripts/             # C# 스크립트
│   ├── Manager/         # GameManager, UIManager, AudioManager
│   ├── Card/            # Card, CardDeck, CardEffect 클래스
│   ├── Game/            # 게임 로직 (턴 관리, 규칙 등)
│   ├── UI/              # UI 컨트롤러
│   └── Utilities/       # 유틸리티 (확장 메서드, 헬퍼 함수)
├── Sprites/             # 2D 그래픽 에셋
│   ├── Cards/           # 카드 이미지
│   ├── UI/              # 버튼, 배경, 아이콘
│   └── Effects/         # 파티클, 애니메이션 이미지
├── Prefabs/             # 재사용 가능한 프리팹
│   ├── Cards/           # 카드 프리팹
│   ├── UI/              # UI 요소 프리팹
│   └── Effects/         # 이펙트 프리팹
├── Audio/               # 사운드 파일
│   ├── Music/           # 배경음악
│   └── SFX/             # 효과음
├── Resources/           # 런타임 로드 가능한 데이터
│   ├── Cards/           # 카드 데이터 (JSON/CSV)
│   └── Config/          # 게임 설정 파일
├── Documentation/       # 기술 문서
│   ├── CODE_STYLE.md    # 코딩 스타일 가이드
│   └── ARCHITECTURE.md  # 아키텍처 설명
└── Editor/              # 에디터 스크립트 (빌드 불포함)
```

---

## 3. 초기 Scene 설정

### MainScene.unity 생성
1. **Assets → Scenes** 폴더 생성
2. **Create → Scene** → `MainScene` 저장
3. 기본 요소 추가:
   - Canvas (UI 루트)
   - Camera (메인 카메라)
   - GameManager (빈 GameObject)

### Canvas 설정 (UI 기반)
- Render Mode: **Screen Space - Camera**
- Canvas Scaler: 1920×1080 기준

---

## 4. 스크립트 기본 템플릿

### GameManager.cs 예시
```csharp
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public static GameManager Instance { get; private set; }

    private void Awake()
    {
        if (Instance != null && Instance != this)
        {
            Destroy(gameObject);
            return;
        }
        
        Instance = this;
        DontDestroyOnLoad(gameObject);
    }

    private void Start()
    {
        Debug.Log("SpellDeck Game Started");
    }
}
```

### Card.cs 기본 구조
```csharp
using UnityEngine;

public class Card : MonoBehaviour
{
    [SerializeField] private string cardName;
    [SerializeField] private string description;
    [SerializeField] private int cost;
    [SerializeField] private Sprite cardImage;

    public string CardName => cardName;
    public string Description => description;
    public int Cost => cost;

    public virtual void OnPlay()
    {
        Debug.Log($"{cardName} played!");
    }
}
```

---

## 5. 프로젝트 설정 (Project Settings)

### 필수 설정 항목

**Edit → Project Settings**

1. **Player Settings**
   - Company Name: Your Company
   - Product Name: SpellDeck
   - Default Icon 설정
   - Resolution: 1920×1080

2. **Graphics**
   - 2D 프로젝트이므로 기본 설정 유지

3. **Audio**
   - Default Speaker Mode: Stereo
   - Volume 레벨 조정

---

## 6. 권장 패키지

Unity 2022.3에서 추가 설치 권장:
- **2D Animation**: 2D 스프라이트 애니메이션
- **2D PSD Importer**: Photoshop 파일 임포트 (필요시)
- **TextMesh Pro**: 향상된 텍스트 렌더링

**Window → TextMesh Pro → Import TMP Essential Resources** 실행

---

## 7. Git 설정 (.gitignore)

프로젝트 루트에 `.gitignore` 파일 생성:

```
# Unity generated
[Ll]ibrary/
[Tt]emp/
[Oo]bj/
[Bb]uild/
[Bb]uilds/
[Cc]onverted/

# Visual Studio
.vs/
*.csproj
*.sln

# IDE
.idea/
*.swp

# OS
.DS_Store
Thumbs.db
```

---

## 8. 개발 첫 단계 체크리스트

- [ ] Unity 2022.3 LTS 설치 완료
- [ ] SpellDeck 프로젝트 생성
- [ ] 폴더 구조 생성
- [ ] MainScene.unity 생성
- [ ] GameManager 스크립트 작성
- [ ] Canvas 및 기본 UI 구성
- [ ] Git 초기화 (.gitignore 추가)
- [ ] GDD 참고하여 카드 시스템 설계

---

## 9. 참고 문서

- GDD: `SpellDeck_GDD_v08.docx` 참조
- Unity 공식 2D 튜토리얼: https://learn.unity.com/projects/2d-game-kit
- C# 스타일 가이드: https://microsoft.github.io/csharp-coding-conventions/

---

**다음 단계**: 카드 데이터 구조 설계 및 덱 시스템 구현
