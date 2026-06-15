# Humanizer 설치 및 사용법

이 프로젝트는 한국어 자기소개서 초안의 AI 문체를 줄이기 위해 `epoko77-ai/im-not-ai` 저장소의 Codex용 `humanize-korean` 스킬을 사용합니다.

- 원본 저장소: `https://github.com/epoko77-ai/im-not-ai`
- 사용 스킬: `humanize-korean`
- Codex 실행 명령: `$humanize-korean`
- 프로젝트 적용 대상: `result/기업명/직무명YYMM.md`
- 운영 원칙: 초안과 최종본을 분리하지 않고, humanizer 검수본을 같은 `.md` 파일에 덮어씁니다.

## 새 로컬 환경 설치

다른 PC나 새 Codex 환경에서 이 프로젝트를 이어서 작업할 때는 먼저 `humanize-korean` 스킬을 설치합니다.

### 1. 전제

- Git이 설치되어 있어야 합니다.
- Codex CLI 또는 Codex Desktop에서 스킬을 사용할 수 있어야 합니다.
- Windows PowerShell에서는 이 프로젝트의 `AGENTS.md`에 적힌 UTF-8 preamble을 적용한 뒤 명령을 실행합니다.

### 2. 저장소 클론

```bash
git clone https://github.com/epoko77-ai/im-not-ai.git
cd im-not-ai
```

### 3. Codex용 설치

원본 저장소는 Codex CLI Skills를 지원합니다. macOS, Linux, Git Bash, WSL처럼 shell script를 실행할 수 있는 환경에서는 Codex만 설치하도록 아래 명령을 사용합니다.

```bash
./install.sh --codex-only
```

Windows PowerShell에서 `install.sh` 실행이 어렵거나 심링크 권한 문제가 나면 수동 복사 방식으로 설치합니다.

```powershell
$src = "경로\to\im-not-ai\codex\skills\humanize-korean"
$dst = "$env:USERPROFILE\.codex\skills\humanize-korean"
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -Recurse -Force -Path $src -Destination $dst
```

수동 복사 후 아래 파일이 있어야 합니다.

```text
%USERPROFILE%\.codex\skills\humanize-korean\SKILL.md
%USERPROFILE%\.codex\skills\humanize-korean\references\quick-rules.md
%USERPROFILE%\.codex\skills\humanize-korean\references\ai-tell-taxonomy.md
%USERPROFILE%\.codex\skills\humanize-korean\references\rewriting-playbook.md
%USERPROFILE%\.codex\skills\humanize-korean\references\metrics.py
```

### 4. 설치 확인

새 Codex 세션을 열고 다음 중 하나로 확인합니다.

```text
$humanize-korean
```

또는 자연어로 요청합니다.

```text
이 문장 AI 티 없애고 자연스럽게 윤문해줘.
```

스킬 목록을 볼 수 있는 환경이라면 `humanize-korean`이 표시되는지도 확인합니다.

## 업데이트

원본 저장소가 업데이트되면 클론한 `im-not-ai` 폴더에서 아래 명령을 실행합니다.

```bash
git pull
./update.sh
```

Windows에서 스크립트 실행이 어렵다면 `codex/skills/humanize-korean` 폴더를 다시 `%USERPROFILE%\.codex\skills\humanize-korean`에 복사합니다.

## 프로젝트 사용 흐름

1. 기업 분석과 문항별 초안을 먼저 작성합니다.
2. 자기소개서 파일 전체 또는 특정 문항의 `### 답변` 본문을 대상으로 `$humanize-korean`을 적용합니다.
3. 윤문된 문장은 같은 `.md` 파일의 기존 초안 답변에 덮어씁니다.
4. 별도 초안 파일, 복사본, `_workspace` 결과 파일은 최종 산출물로 남기지 않습니다.
5. 실제 기업 자기소개서 최종본은 `result/기업명/직무명YYMM.md`에만 남깁니다.
6. 결과물의 의미, 수치, 고유명사, 기업명, 직무명이 원문과 달라지지 않았는지 확인합니다.
7. 문항별 글자 수 제한을 다시 확인합니다.
8. 이상이 없으면 `상태`를 `검토중` 또는 `제출본`으로 갱신합니다.

## 자소서 적용 원칙

- 사실, 수치, 프로젝트명, 기업명, 직무명, 기술명은 바꾸지 않습니다.
- JD 키워드, 기업 맞춤 문장, STAR 구조, 입사 후 기여 문장은 의미가 흐려지지 않게 보존합니다.
- `~를 통해`, `~에 대해`, `~에 있어서`, `결론적으로`, `이를 통해`, `따라서`처럼 반복되는 AI식 연결어를 줄입니다.
- 지나치게 균일한 문장 길이를 피하되, 자기소개서의 격식체는 유지합니다.
- 경험의 구조와 성과는 보존하고 문체만 자연스럽게 다듬습니다.
- 변경률이 커지면 원문 의도가 흐려질 수 있으므로 문항 단위로 검토합니다.

## 요청 예시

```text
$humanize-korean result/LG CNS/SoftwareEngineer2606.md
장르: 공적, 강도: 보수
```

```text
이 문항 답변 AI 티 없애고 자소서 문체로 자연스럽게 다듬어줘.
의미, 수치, 기술명은 바꾸지 말고 글자 수 제한도 유지해줘.
```

## 최종 확인

- 다른 기업명이 남아 있지 않은가
- 답변 제목과 본문이 분리되어 있는가
- 글자 수 제한을 넘지 않는가
- 기술명과 수치가 원문과 일치하는가
- 문장이 너무 과장되거나 문학적으로 바뀌지 않았는가
- humanizer 검수본이 `result/기업명/` 아래 같은 `.md` 파일에 반영되어 최종 파일 하나만 남아 있는가

## 참고

- `im-not-ai` 저장소는 Claude Code와 OpenAI Codex CLI를 모두 지원합니다.
- Codex에서는 Fast 단일 호출 모드로 동작합니다.
- 정밀 strict 파이프라인은 Claude Code 전용입니다.
