# 새 컴퓨터 Claude Code 세팅 가이드

새 컴퓨터에서 이 프로젝트를 Claude Code로 작업하기 위한 전체 설치 순서입니다.
위에서부터 순서대로 따라 하면 됩니다. (Windows 기준, Mac은 각 단계에 병기)

---

## 1. Git 설치

- **Windows**: https://git-scm.com/download/win 에서 설치 (기본 옵션 그대로 Next)
- **Mac**: 터미널에서 `xcode-select --install`

설치 후 터미널(PowerShell 또는 Terminal)에서 본인 정보 등록:

```bash
git config --global user.name "jinha2007-dotcom"
git config --global user.email "jinha2007@gmail.com"
```

## 2. Node.js 설치 (선택이지만 권장)

로컬 서버 실행(`npx serve`)과 일부 도구에 필요합니다.

- https://nodejs.org 에서 **LTS 버전** 다운로드 후 설치

확인: `node -v` 입력 시 버전이 나오면 성공.

## 3. Claude Code 설치

**Windows (PowerShell에서):**

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Mac/Linux:**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

설치 후 새 터미널을 열고 확인:

```bash
claude --version
```

## 4. Claude Code 로그인

```bash
claude
```

처음 실행하면 브라우저가 열리며 로그인 안내가 나옵니다.
**Claude 구독 계정(claude.ai)** 으로 로그인하면 됩니다. 한 번만 하면 계속 유지됩니다.

## 5. 프로젝트 클론

작업 폴더로 이동 후 저장소를 내려받습니다:

```bash
git clone https://github.com/jinha2007-dotcom/us-stock-monitor.git
cd us-stock-monitor
```

> GitHub 로그인 창이 뜨면 브라우저 인증을 따라가면 됩니다.
> 인증이 번거로우면 GitHub CLI 설치 후 `gh auth login` 한 번으로 해결됩니다: https://cli.github.com

## 6. 프로젝트에서 Claude Code 시작

```bash
cd us-stock-monitor
claude
```

이 저장소에는 이미 다음이 세팅되어 있습니다:

- **`CLAUDE.md`** — Claude가 프로젝트 구조·전략 파라미터·주의사항을 자동으로 파악
- **`.claude/settings.json`** — git 조회/커밋, 로컬 서버 실행 등 자주 쓰는 명령이 사전 승인되어 매번 허용 버튼을 누를 필요 없음

즉, 클론만 하면 Claude Code 세팅은 끝입니다.

## 7. 모니터 실행 방법

```bash
# 프로젝트 폴더에서
python -m http.server 8000
# 또는
npx serve .
```

브라우저에서 `http://localhost:8000` 접속 → Massive API 키 입력(최초 1회, 브라우저에만 저장됨).

---

## 자주 쓰는 Claude Code 명령 / 팁

| 명령 | 설명 |
|------|------|
| `claude` | 대화형 세션 시작 |
| `claude -c` | 직전 대화 이어서 계속 |
| `claude --resume` | 과거 세션 목록에서 골라서 재개 |
| `/help` | 명령어 전체 보기 |
| `/config` | 테마·모델 등 환경설정 |
| `/clear` | 대화 초기화 (새 작업 시작할 때) |
| `Shift+Tab` | 모드 전환 (일반 → 자동수락 → 플랜 모드) |
| `Esc` | Claude 작업 중단 |

### 함께 쓰면 좋은 것

- **VS Code**: https://code.visualstudio.com 설치 후, 확장 마켓플레이스에서 **"Claude Code"** 확장을 설치하면 에디터 안에서 바로 Claude를 쓸 수 있습니다.
- **웹/모바일에서 작업**: https://claude.ai/code 에서 이 저장소를 연결하면 컴퓨터 없이도 작업을 시킬 수 있습니다 (지금 이 세팅도 그렇게 진행된 것).

## 문제 해결

- `claude` 명령을 못 찾음 → 터미널을 완전히 닫고 새로 열기
- git push 시 권한 오류 → `gh auth login` 으로 GitHub 재인증
- 차트가 안 뜸 → 인터넷 연결 확인 (차트 라이브러리를 CDN에서 불러옴)
