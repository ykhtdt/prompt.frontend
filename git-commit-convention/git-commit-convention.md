Angular Commit Convention

> 최신 업데이트: 2025년 05월 13일 14:30

# Angular Commit Convention - 커밋 타입 정리

이 문서는 [Angular Commit Convention](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit)에 기반하여 커밋 타입을 정의하고, 자주 사용하는 예시를 제공합니다. 커밋 메시지를 일관성 있게 작성하여 협업 효율과 변경 이력을 명확히 유지할 수 있습니다.

---

커밋 타입 결정 기준

- **feat** - 기능이 새로 추가되었는가?
- **fix** - 버그를 수정했는가?
- **perf** - 성능을 개선했는가?(속도, 메모리, 렌더링 등)
- **refactor** - 코드 구조만 바꿨고, 동작이나 성능은 그대로인가?
- **test** - 테스트 코드를 추가/수정했는가?
- **style** - 스타일(공백, 포맷 등)만 바꿨는가?
- **docs** -  문서만 변경했는가? (README, 주석 등)
- **build** -  빌드 시스템이나 설정 파일 변경인가?
- **ci** -  CI/CD 설정을 수정했는가?
- **revert** - 기존 변경을 되돌리는 목적인가?
- **chore** - 위에 해당하지 않는 유지보수 작업인가?

---

## 커밋 타입 목록

| 타입       | 설명 | 자주 사용되는 예시 |
|------------|------|--------------------|
| **feat**   | 새로운 기능 추가 | 새로운 페이지, 컴포넌트, API 추가 |
| **fix**    | 버그 수정 | 로직 오류, 유효성 검사 수정 |
| **refactor** | 리팩토링 (동작 변화 없음) | 구조 개선, 네이밍 변경, 중복 제거 |
| **chore**  | 기타 변경 (릴리즈 영향 없음) | 파일명 변경, 설정 파일 정리, 의존성 정리 |
| **docs**   | 문서 관련 변경 | README 수정, 주석 보완 |
| **style**  | 코드 포맷팅 및 스타일 수정 | prettier 적용, 들여쓰기 수정 |
| **test**   | 테스트 코드 추가/수정 | 테스트 케이스 추가, 리팩토링 |
| **build**  | 빌드 설정/의존성 관련 변경 | tsconfig, vite, webpack 설정 변경 |
| **ci**     | CI 설정 변경 | GitHub Actions, Travis 등 설정 수정 |
| **perf**   | 성능 개선 | 렌더링 최적화, 연산 개선 |
| **revert** | 커밋 되돌리기 | `revert: feat(login): add login feature` |

---

## 커밋 메시지 예시

| 커밋 메시지 | 설명 |
|-------------|------|
| `feat: add user login feature` | 사용자 로그인 기능 추가 |
| `fix: correct typo in username validation` | 유효성 검사 오류 수정 |
| `refactor: extract feed logic into service` | 피드 로직을 서비스로 분리 |
| `chore: rename utils to shared-utils` | 파일명 또는 폴더명 변경 |
| `docs: update API usage in README` | 문서 내용 갱신 |
| `style: fix lint issues` | 코드 스타일 수정 |
| `build: update tsconfig include paths` | 빌드 설정 변경 |
| `ci: fix node version in GitHub Actions` | CI 환경 수정 |
| `perf: improve scroll rendering performance` | 스크롤 렌더링 성능 개선 |

---

## 팁

- `feat`와 `fix`는 릴리즈 노트 자동 생성에 핵심이 됩니다.
- `chore`, `style`, `refactor`는 릴리즈에 포함되지 않는 내부 변경입니다.

---

## 참고 링크

- [Angular Git Commit Guidelines](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit)
- [Conventional Commits 공식 사이트](https://www.conventionalcommits.org/)
