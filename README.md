# Python Board App 📝

> 사용자 인증, 역할 기반 접근 제어, RESTful API 기능을 갖춘 견고하고 모듈화된 Flask 기반 게시판 애플리케이션입니다.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.0-green?logo=flask&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## 📖 개요 (Overview)

이 프로젝트는 **Flask**로 구축된 모놀리식 웹 애플리케이션입니다. 서버 사이드 렌더링 방식의 웹 UI와 모바일 클라이언트를 위한 JWT 보안 REST API를 모두 제공하여 커뮤니티 관리를 위한 완전한 솔루션을 제시합니다.
https://github.com/coreline-ai/flutter_simple_saas_app Flutter 앱울 확인하실 수 있습니다

주요 아키텍처 특징:
-   **애플리케이션 팩토리 패턴 (Application Factory Pattern)**: 확장성과 테스트 용이성을 고려한 초기화 구조.
-   **블루프린트 아키텍처 (Blueprint Architecture)**: 기능별 로직 분리 (인증, 게시판, 관리자, API).
-   **보안 설계 (Secure by Design)**: XSS 방지(Bleach), CSRF 토큰, 비밀번호 해싱 적용.

---

## ✨ 주요 기능 (Key Features)

### 🔐 인증 및 보안
-   **이원화된 인증 시스템**: 웹 UI는 세션 기반(Flask-Login), API는 JWT 기반(Flask-JWT-Extended) 인증을 사용합니다.
-   **역할 기반 접근 제어 (RBAC)**: 관리자와 일반 사용자에 대한 세밀한 권한 관리.
    -   `관리자 전용 (Admin Only)` 게시판.
    -   `로그인 필수 (Login Required)` 게시판.
-   **XSS 보호**: `Bleach`를 사용하여 게시글의 HTML 태그를 화이트리스트 방식으로 필터링합니다.

### 📋 게시판 시스템
-   **CRUD 작업**: 게시글 작성, 조회, 수정, 삭제 기능 완벽 지원.
-   **카테고리**: 게시판별 동적 카테고리 구성.
-   **파일 업로드**: 안전한 파일 첨부 기능.
-   **상호작용**: 댓글, 좋아요, 알림 시스템.
-   **관리자 대쉬보드**: 가입승인, 게시판생성, 카테고리생성, 사용자관리 기능.

### 🚀 REST API
-   **Swagger 문서화**: `flask-restx`를 통한 API 문서 자동 생성.
-   **최적화**: 즉시 로딩(`joinedload`) 전략을 사용하여 N+1 쿼리 문제 해결.

---

## 🛠️ 기술 스택 (Tech Stack)

| 구분 | 기술 | 설명 |
| :--- | :--- | :--- |
| **프레임워크** | **Flask** | 마이크로 웹 프레임워크 |
| **데이터베이스** | **SQLite** / **SQLAlchemy** | 기본 DB 및 ORM |
| **마이그레이션** | **Flask-Migrate** | Alembic 기반 스키마 관리 |
| **API** | **Flask-RESTx** | API 구축 및 문서화 |
| **인증** | **Flask-Login** / **JWT-Extended** | 사용자 인증 처리 |
| **서버** | **Gunicorn** | 프로덕션용 WSGI HTTP 서버 |

---

## 🚀 시작하기 (Getting Started)

### 필수 요구사항
-   Python 3.10 이상
-   Virtualenv (권장)

### 설치 방법

1.  **저장소 클론**
    ```bash
    git clone https://github.com/yourusername/python-board-app.git
    cd python-board-app
    ```

2.  **가상 환경 설정**
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate  # Windows: .venv\Scripts\activate
    ```

3.  **의존성 패키지 설치**
    ```bash
    pip install -r requirements.txt
    ```

4.  **데이터베이스 설정**
    SQLite 데이터베이스를 초기화하고 기존 마이그레이션을 적용합니다.
    ```bash
    flask db upgrade
    ```
    *(선택 사항) 샘플 데이터를 로드하려면:*
    ```bash
    cp board.sample.db board.db
    ```

### 애플리케이션 실행

**개발 모드:**
```bash
flask run --debug
```

**프로덕션 모드 (Gunicorn):**
```bash
# 포함된 run.sh 스크립트 사용
./run.sh
```
*참고: 기본적으로 `http://127.0.0.1:5000`에서 실행됩니다.*

---

## 📚 API 문서

서버가 실행 중일 때, 아래 주소에서 대화형 Swagger API 문서를 확인하실 수 있습니다:

-   **URL**: `http://localhost:5000/api/v1/docs`

API 주요 엔드포인트:
-   `/auth/login`: JWT 토큰 생성.
-   `/boards`: 게시판 및 카테고리 목록 조회.
-   `/boards/{slug}/posts`: 페이지네이션이 적용된 게시글 조회.

---

## 📂 프로젝트 구조

```
app/
├── __init__.py       # 앱 팩토리
├── models.py         # SQLAlchemy 모델
├── views/            # 블루프린트 (뷰)
│   ├── api_views.py  # REST API
│   ├── board_views.py# 웹 UI
│   └── auth_views.py # 인증 기능
├── templates/        # Jinja2 HTML 템플릿
├── static/           # CSS, JS, 이미지
└── utils/            # 유틸리티 함수
```

## 📜 라이선스

이 프로젝트는 [MIT License](LICENSE)에 따라 라이선스가 부여됩니다.
