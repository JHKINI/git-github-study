# Git & GitHub 활용 가이드

**Git 기반 버전 관리 · 브랜치 관리 · 코드 통합 · 문제 해결**

Git과 GitHub를 활용한 소스 코드 버전 관리 및 협업 과정을 정리한 학습 저장소입니다. 기본적인 Git 명령어부터 원격 저장소 연동, 브랜치 병합, 충돌 관련 작업까지 학습하고 실제 프로젝트에서 경험한 내용을 기록합니다.

> 목적: 단순한 명령어 암기를 넘어 Git의 동작 원리를 이해하고, 프로젝트 개발 과정에서 버전 관리와 코드 통합을 수행할 수 있는 기본 역량을 갖추는 것

## 1. Overview

### Learning Objectives

- **Version Control:** Git을 활용한 소스 코드 변경 이력 관리
- **Remote Repository:** GitHub 원격 저장소 연결 및 코드 공유
- **Branch Management:** 브랜치를 활용한 작업 분리와 브랜치 전환
- **Code Integration:** 브랜치 병합을 통한 변경 사항 통합
- **Troubleshooting:** Push 거부 및 병합 충돌 등 개발 과정에서 발생하는 문제의 원인 파악과 해결 절차 학습

### Development Environment

| Category | Tools |
|---|---|
| Version Control | Git |
| Remote Repository | GitHub |
| Development Tool | Visual Studio Code |
| Documentation | Markdown |

### Practical Experience

실제 프로젝트에서 사용한 명령어와 작업 경험을 바탕으로 Git 활용 과정을 정리했습니다.

| Area | Experience |
|---|---|
| Repository | 로컬 저장소 초기화 및 원격 저장소 연결 |
| Commit | 변경 사항 스테이징 및 커밋 |
| Remote Sync | Push 및 Pull을 통한 저장소 동기화 |
| Branch | 브랜치 전환 및 브랜치 병합 |
| Troubleshooting | Push 거부 및 병합 충돌 관련 작업 경험 |

**Related Project:** [번호판 탐지 프로젝트 - GitHub](여기에-실제-프로젝트-URL-입력)

위 프로젝트는 브랜치 병합과 충돌 관련 작업을 경험한 실제 팀 프로젝트입니다.

---

## 2. Git Basic Workflow

Git의 기본적인 버전 관리 과정은 작업 상태 확인, 변경 사항 스테이징, 커밋, 원격 저장소 반영 순서로 진행됩니다.

```text
Working Directory
       ↓
   git status
       ↓
    git add
       ↓
   git commit
       ↓
    git push
       ↓
  GitHub Repository
```

### Basic Commands

```bash
# 1. 로컬 저장소 초기화
git init

# 2. 현재 작업 상태 확인
git status

# 3. 변경 파일 스테이징
git add .

# 4. 변경 사항 커밋
git commit -m "기능 구현"

# 5. 원격 저장소에 업로드
git push origin main
```

### 주요 명령어

| Command | Description |
|---|---|
| `git init` | 현재 디렉터리를 Git 저장소로 초기화 |
| `git status` | 파일 변경 및 스테이징 상태 확인 |
| `git add .` | 변경된 파일을 스테이징 영역에 등록 |
| `git commit -m "message"` | 스테이징된 변경 사항을 커밋으로 기록 |
| `git log --oneline` | 커밋 이력을 한 줄씩 확인 |
| `git diff` | 커밋되지 않은 변경 내용 비교 |
| `git diff --staged` | 스테이징된 변경 내용 확인 |

### Understanding the Workflow

- **Working Directory:** 파일을 실제로 수정하는 작업 공간
- **Staging Area:** 다음 커밋에 포함할 변경 사항을 준비하는 영역
- **Repository:** 커밋된 변경 이력을 저장하는 영역
- **Commit:** 특정 시점의 변경 사항을 기록한 버전

`git add`는 변경 사항을 커밋 대상으로 준비하는 명령어이며, 실제 버전 기록은 `git commit`을 실행해야 생성됩니다.

---

## 3. Remote Repository Management

로컬 저장소와 GitHub 원격 저장소를 연결하여 소스 코드를 공유하고 변경 사항을 동기화합니다.

### Remote Repository Connection

```bash
# GitHub 저장소 연결
git remote add origin <REPOSITORY_URL>

# 등록된 원격 저장소 확인
git remote -v

# 현재 브랜치 이름을 main으로 변경
git branch -M main

# 원격 저장소에 최초 업로드
git push -u origin main
```

`origin`은 원격 저장소에 일반적으로 사용하는 별칭입니다. `git branch -M main`은 현재 브랜치의 이름을 `main`으로 변경합니다.

### Clone, Pull, Push

```bash
# 원격 저장소를 로컬에 복제
git clone <REPOSITORY_URL>

# 원격 저장소의 변경 사항 가져와 통합
git pull origin main

# 로컬 커밋을 원격 저장소에 업로드
git push origin main
```

| Command | Purpose |
|---|---|
| `git clone` | 저장소를 처음 로컬 환경에 복제 |
| `git pull` | 원격 변경 사항을 가져와 현재 브랜치에 통합 |
| `git push` | 로컬 커밋을 원격 저장소에 반영 |
| `git fetch` | 원격 변경 사항을 가져오되 현재 브랜치에 자동 통합하지 않음 |
| `git remote -v` | 원격 저장소 주소 확인 |

### Important Distinction

`git clone`은 저장소를 로컬에 복제하는 작업이며, `git pull`은 이미 연결된 저장소의 새로운 변경 사항을 가져와 통합하는 작업입니다. `git push`는 반대로 로컬에서 생성한 커밋을 원격 저장소에 전달합니다.

---

## 4. Branch Management

브랜치는 서로 다른 작업을 분리하고, 변경 사항을 독립적으로 개발한 후 통합할 수 있도록 지원합니다.

### Branch Commands

```bash
# 브랜치 목록 확인
git branch

# 새 브랜치 생성
git branch feature/search

# 새 브랜치를 생성하고 이동
git switch -c feature/search

# 기존 브랜치로 이동
git switch main

# 브랜치 병합
git merge feature/search
```

### Feature Branch Workflow

기능별 브랜치를 사용하는 일반적인 작업 흐름입니다.

```bash
# 1. 기능 브랜치 생성 및 이동
git switch -c feature/search

# 2. 코드 수정 후 변경 사항 기록
git add .
git commit -m "feat: implement search"

# 3. 원격 저장소에 브랜치 업로드
git push -u origin feature/search

# 4. 기준 브랜치로 이동
git switch main

# 5. 기능 브랜치 병합
git merge feature/search
```

실제 협업 환경에서는 팀의 브랜치 운영 정책에 따라 Pull Request를 통한 검토 후 병합할 수 있습니다.

### Merge Concept

브랜치 병합은 서로 다른 작업에서 발생한 변경 사항을 하나의 브랜치에 통합하는 과정입니다.

팀 프로젝트에서 `main` 브랜치와 `kiwook` 브랜치의 병합 과정을 경험했으며, 브랜치 통합 과정에서 발생하는 충돌과 변경 사항 확인의 중요성을 학습했습니다.

---

## 5. Git Conflict Resolution

### What Is a Merge Conflict?

두 브랜치에서 같은 파일의 동일한 부분을 서로 다르게 수정하면 Git이 어떤 변경 사항을 유지해야 할지 자동으로 판단하지 못해 병합 충돌이 발생할 수 있습니다.

### Conflict Resolution Workflow

1. `git status`로 충돌이 발생한 파일을 확인합니다.
2. 충돌 파일을 열어 각 브랜치의 변경 내용을 비교합니다.
3. 최종적으로 유지할 코드를 선택하고 충돌 표시를 제거합니다.
4. 수정된 파일을 스테이징합니다.
5. 병합 상태를 확인하고 병합을 완료합니다.

충돌 파일에는 다음과 같은 표시가 나타날 수 있습니다.

```text
<<<<<<< HEAD
현재 브랜치의 코드
=======
병합 대상 브랜치의 코드
>>>>>>> feature/search
```

충돌 해결 시 위 표시를 제거하고 의도한 최종 코드를 남겨야 합니다.

### Resolution Commands

```bash
# 충돌 상태 확인
git status

# 충돌 파일 수정 후 스테이징
git add <FILE_NAME>

# 일반적인 merge 충돌 해결 후 병합 완료
git commit

# 최종 상태 확인
git status
```

`git commit` 단계는 일반적인 merge 충돌을 해결하는 경우의 예시입니다. Rebase나 다른 진행 상태에서는 완료 절차가 달라질 수 있습니다.

### Practical Experience

팀 프로젝트의 브랜치 병합 과정에서 충돌 관련 작업을 경험했습니다. 이를 통해 브랜치 통합은 단순히 명령어를 실행하는 것뿐 아니라, 변경 내용과 코드의 의도를 확인하는 과정이 중요하다는 점을 학습했습니다.

**Related Project:** [번호판 탐지 프로젝트 - GitHub](여기에-실제-프로젝트-URL-입력)

---

## 6. Troubleshooting

### Case 1. Push Rejected

**Problem**

원격 저장소에 로컬에 없는 커밋이 존재하면 Push가 거부될 수 있습니다.

**Diagnosis**

```bash
git status
git fetch origin
git log --oneline --graph --all
```

원격 저장소와 로컬 저장소의 커밋 이력을 확인하여 차이를 파악합니다.

**Possible Resolution**

```bash
git pull --rebase origin main
git push origin main
```

Rebase 과정에서 충돌이 발생하면 파일을 수정하고 스테이징한 후 `git rebase --continue`로 진행합니다. 작업을 취소해야 하는 경우에는 `git rebase --abort`를 사용할 수 있습니다.

단, 원격 저장소의 변경 사항과 현재 작업 상태에 따라 해결 방법이 달라질 수 있으므로 원인을 먼저 확인해야 합니다.

### Case 2. Merge Conflict

**Problem**

서로 다른 브랜치에서 동일한 코드 영역을 수정하여 자동 병합에 실패하는 상황입니다.

**Resolution**

- `git status`로 충돌 파일을 확인합니다.
- 변경 사항을 비교하여 최종 코드를 결정합니다.
- 충돌 표시를 제거하고 파일을 수정합니다.
- 스테이징 및 병합 완료 절차를 진행합니다.
- 최종 변경 사항을 확인합니다.

### Troubleshooting Principles

- 오류 메시지를 확인한 뒤 원인을 파악합니다.
- 원격 및 로컬 커밋 이력을 확인합니다.
- 작업 내용을 백업하거나 커밋하여 불필요한 코드 손실을 방지합니다.
- 무조건 강제 Push하기보다 저장소 상태를 먼저 확인합니다.

---

## 7. Collaboration Practices

협업 시에는 명령어 사용뿐 아니라 변경 이력을 명확하게 관리하고, 팀원 간 코드 통합 과정에서 발생할 수 있는 문제를 예방하는 것이 중요합니다.

### Commit Convention

커밋 메시지는 변경 목적을 명확하게 표현하도록 작성합니다.

```bash
git commit -m "feat: add search functionality"
git commit -m "fix: handle empty response"
git commit -m "docs: update README"
```

| Prefix | Purpose |
|---|---|
| `feat` | 기능 추가 |
| `fix` | 오류 수정 |
| `docs` | 문서 수정 |
| `refactor` | 기능 변경 없이 코드 구조 개선 |
| `test` | 테스트 추가 및 수정 |

### Repository Safety

- `.env`, API 키, 비밀번호 등 민감한 정보를 저장소에 업로드하지 않습니다.
- 작업 전 원격 저장소의 변경 사항을 확인합니다.
- 기능별 브랜치로 작업 범위를 분리합니다.
- 병합 전 변경 사항과 충돌 여부를 검토합니다.
- Pull Request 및 코드 리뷰는 팀의 협업 절차에 따라 적용합니다.

---

## 8. What I Learned

Git과 GitHub는 단순히 코드를 업로드하는 도구가 아니라, 변경 이력을 추적하고 여러 작업의 결과를 통합하기 위한 개발 도구입니다.

이번 학습 내용을 통해 다음과 같은 개념을 정리했습니다.

- 로컬 저장소와 원격 저장소의 역할 및 차이
- 스테이징, 커밋, Push를 통한 버전 관리 과정
- 브랜치 전환과 병합을 통한 작업 통합
- Push 거부 및 병합 충돌의 원인과 해결 절차
- 협업 과정에서 변경 이력과 코드 검토가 중요한 이유

앞으로는 기능별 브랜치 생성부터 원격 Push, Pull Request, 코드 리뷰, 병합까지의 흐름을 직접 반복 실습하여 Git 활용 역량을 강화할 계획입니다.

---

## 9. References

- [Git 공식 문서](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [GitHub Skills](https://skills.github.com/)

