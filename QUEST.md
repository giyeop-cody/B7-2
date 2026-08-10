# B7-2: 웹 기반 AI 챗봇 서비스 고도화 프로젝트

## 📋 과제 정보

| 항목 | 내용 |
|------|------|
| **과목** | Term Project |
| **난이도** | ★★★ (Lv.3) |
| **학습 시간** | 120분 |
| **과제 번호** | 185018 |

---

## 🛠️ 개발 환경

### 5\. 개발 환경

*   Python 3.10 이상

---

## ⚠️ 제약 사항

### 6\. 제약 사항

*   보안 및 비밀 관리
    *   API 키, 데이터베이스 비밀번호 등 민감 정보는 소스 코드에 직접 작성하지 않는다.
    *   모든 민감 정보는 `.env` 파일을 통해 환경 변수로 관리해야 한다.
*   협업 규칙
    *   모든 팀원은 최소 10회 이상의 유의미한 커밋을 생성해야 한다.
    *   기술 문서(README 또는 별도 문서)에 팀 구성원 역할과 개인별 작업 요약을 반드시 포함해야 한다.
    *   `main` 브랜치에는 직접 코드를 푸시할 수 없으며, 반드시 Pull Request를 통해서만 병합해야 한다.
*   배포
    *   비용 관리에 주의하며, 실습 종료 후 불필요한 리소스를 정리한다.

---

## 📝 결과 예시

### 7\. 결과 예시

아래는 정답이 아니라 참고 예시다. 실제 문구와 디자인은 달라도 된다.

*   서비스 흐름 예시
    
    ```css
    1. 회원가입 → 이메일, 비밀번호, 닉네임 입력
    2. 로그인 → 토큰 발급 → 인증 상태로 전환
    3. AI 챗봇 → 새 대화 시작 → 메시지 주고받기 → 대화 내역 저장
    4. 게시판 → 게시글 작성 → 목록에서 확인 → 수정/삭제
    5. 다른 기기/브라우저에서 배포 URL로 접속 → 동일 서비스 이용 가능
    ```
    
*   ERD 예시
    
    ```css
    [User] 1 ──── N [ChatSession] 1 ──── N [Message]
      │
      └── 1 ──── N [Post]
    
    User: id(PK), email, password_hash, username, created_at
    ChatSession: id(PK), user_id(FK), title, created_at
    Message: id(PK), session_id(FK), role, content, created_at
    Post: id(PK), user_id(FK), title, content, created_at, updated_at
    ```
    
*   API 명세서 예시
    
    | 메서드 | URL | 설명 | 인증 |
    | --- | --- | --- | --- |
    | POST | /auth/signup | 회원가입 | X |
    | POST | /auth/login | 로그인 | X |
    | GET | /chat/sessions | 대화 세션 목록 | O |
    | POST | /chat/sessions | 새 대화 세션 생성 | O |
    | POST | /chat/sessions/{id}/messages | 메시지 전송 | O |
    | GET | /chat/sessions/{id}/messages | 메시지 내역 조회 | O |
    | GET | /posts | 게시글 목록 | O |
    | POST | /posts | 게시글 작성 | O |
    | GET | /posts/{id} | 게시글 상세 | O |
    | PUT | /posts/{id} | 게시글 수정 | O (본인만) |
    | DELETE | /posts/{id} | 게시글 삭제 | O (본인만) |
    
*   시스템 아키텍처 예시
    
    ```css
    ┌──────────┐    HTTP     ┌──────────┐    SQL      ┌───────────┐
    │          │ ----------→ │          │ ----------→ │           │
    │ Frontend │   REST API  │ Backend  │             │     DB    │
    │ (React)  │ ←---------- │ (FastAPI)│ ←---------- │  (SQLite/ │
    │          │    JSON     │          │             │PostgreSQL)│
    └──────────┘             └────┬─────┘             └───────────┘
                                  │
                                  │ HTTPS
                                  ▼
                             ┌──────────┐
                             │  AI API  │
                             │(OpenAI / │
                             │Anthropic)│
                             └──────────┘
    ```

---

> *이 문서는 Codyssey AI/SW 기초 과정의 과제 내용을 기반으로 작성되었습니다.*
