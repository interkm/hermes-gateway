# Hermes Gateway — 에디슬라 AI 비서 설정

[Hermes Agent](https://github.com/NousResearch/hermes-agent) (NousResearch) 기반 개인 AI 비서 설정 파일 모음.

Telegram으로 대화하면 로컬 Ollama LLM(qwen3:14b)이 응답하고, `/wiki` `/learn` 명령으로 Obsidian vault에 자동 저장합니다.

## 구성 파일

| 파일 | 설명 |
|-----|------|
| `config.yaml` | 모델, 에이전트, 플랫폼 설정 |
| `SOUL.md` | 에이전트 페르소나 정의 |
| `skills/wiki/SKILL.md` | Obsidian 위키 커스텀 스킬 |
| `.env.example` | 환경변수 템플릿 |

## 설치

### 1. Hermes 프레임워크 설치

```bash
pip install hermes-agent
# 또는
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent && pip install -e .
```

### 2. 설정 파일 복사

```bash
cp config.yaml ~/.hermes/config.yaml
cp SOUL.md ~/.hermes/SOUL.md
mkdir -p ~/.hermes/skills/wiki
cp skills/wiki/SKILL.md ~/.hermes/skills/wiki/SKILL.md
```

### 3. 환경변수 설정

```bash
cp .env.example ~/.hermes/.env
# .env 파일에 토큰 입력
```

### 4. Gateway 실행

```bash
hermes gateway run
```

## 주요 설정 (config.yaml)

```yaml
model:
  provider: ollama-launch
  default: qwen3:14b

agent:
  max_turns: 60
  reasoning_effort: medium

compression:
  enabled: true
```

## 커스텀 Wiki 스킬 명령어

| 명령어 | 설명 |
|--------|------|
| `/wiki [내용]` | 텍스트 분석 후 Obsidian 저장 |
| `/learn [주제]` | 심층 학습 문서 생성 |
| `/summary` | 오늘 대화 요약 저장 |
| `/wstatus` | Vault 현황 조회 |

## 의존 프로젝트

- [JenyWikiBot](https://github.com/interkm/wiki-agent) — 별도 Telegram 봇 (wiki 전용)
- [Hermes Telegram Agent](https://github.com/interkm/telegram-agent) — 스킬 로더 봇
