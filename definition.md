## 1. 프로젝트 개요 (Vision & Background)
현재 조직 내 파편화된 파일 공유 방식(이메일, 메신저)은 **버전 충돌(Race Condition)**, **데이터 가시성 결여**, **보안 취약성** 문제를 야기하고 있습니다. 

본 프로젝트는 **Git의 Snapshot 메커니즘**과 **RBAC 보안 모델**을 결합하여, 대규모 트래픽에서도 데이터 무결성을 유지하는 중앙 집중형 파일 관리 플랫폼 구축을 목표로 합니다.

## 2. 시스템 아키텍처 (System Architecture)
대형 프로젝트의 확장성을 고려하여 **계층화 아키텍처(Layered Architecture)**를 채택합니다.

*   **Presentation Layer**: Web Dashboard (React/Next.js) & Mobile App (Kotlin/Jetpack Compose)
*   **Application Layer**: RESTful API Server (Python/FastAPI or Django)
*   **Infrastructure Layer**: 
    *   **Metadata Storage**: PostgreSQL (파일 경로, 권한, 버전 이력 인덱싱)
    *   **Object Storage**: AWS S3 또는 MinIO (실제 바이너리 데이터 저장)
    *   **Cache Layer**: Redis (공유 링크 세션 및 검색 결과 캐싱)

---

## 3. 핵심 기능 명세 (Core Technical Features)

### 3.1 Immutable Versioning (Git-like Snapshot)
*   **기술적 원리**: 파일 수정 시 원본을 덮어쓰지 않고, 새로운 해시(SHA-256) 기반의 블록을 생성합니다. 
*   **이점**: $O(1)$ 시간 복잡도로 특정 시점의 버전 복원이 가능하며, 데이터 오염 시 즉각적인 롤백을 보장합니다.

### 3.2 고성능 검색 엔진 (Multi-level Indexing)
*   **검색 최적화**: 파일명뿐만 아니라 확장자, 소유자, 업로드 기간에 대해 B-Tree 인덱스를 구축합니다.
*   **복잡도**: $O(\log N)$ 내에 200명 이상의 동시 사용자가 요청하는 검색 쿼리를 처리합니다.

### 3.3 보안 및 권한 제어 (RBAC & Signed URL)
*   **접근 제어**: 역할 기반 접근 제어(RBAC)를 통해 폴더별 상속 권한을 관리합니다.
*   **외부 공유**: 특정 시간 동안만 유효한 **Signed URL(HMAC 기반)**을 생성하여 외부 유출 리스크를 최소화합니다.

### 3.4 데이터 회복 탄력성 (Soft Delete & GC)
*   **메커니즘**: 삭제 요청 시 메타데이터의 `is_deleted` 플래그만 마킹(Soft Delete)하고, 30일 후 가비지 컬렉터(GC)가 물리적 데이터를 삭제합니다.

---

## 4. 기술 스택 (Technical Stack)

| Category | Technology | Reason |
| :--- | :--- | :--- |
| **Backend** | Python (FastAPI/PyTorch) | 비동기 처리 및 향후 AI 기반 자동 분류 확장성 고려 |
| **Frontend** | Kotlin (Jetpack Compose) | 네이티브 수준의 모바일 파일 탐색 UI 제공 |
| **Database** | PostgreSQL | 복잡한 계층 구조 쿼리(CTE) 및 트랜잭션 무결성 보장 |
| **Storage** | S3 Compatible Storage | 무제한 확장 가능한 스토리지 아키텍처 확보 |
| **DevOps** | Docker, Git Actions | CI/CD 자동화 및 환경 격리 |

---

## 5. 품질 목표 (Quality Attributes - ISO 25010)

1.  **신뢰성(Reliability)**: 데이터 유실률 0% 지향 (다중화 저장).
2.  **수행 효율성(Performance)**: 100MB 이하 파일 업로드 시 네트워크 대역폭의 90% 이상 활용.
3.  **유지보수성(Maintainability)**: SOLID 원칙 준수 및 모듈화된 인터페이스 설계를 통해 신규 스토리지 엔진 교체 용이성 확보.
4.  **보안성(Security)**: 모든 API 통신 TLS 1.3 암호화 및 2단계 인증(2FA) 지원.

---

## 6. 유사 시스템 분석 (Benchmarking)

| 분석 대상 | 장점 | 단점 | Mini Drive 개선 방향 |
| :--- | :--- | :--- | :--- |
| **Google Drive** | 강력한 협업 툴 연동 | 조직 내부 폐쇄망 적용 어려움 | 온프레미스/프라이빗 클라우드 최적화 |
| **Git/GitHub** | 완벽한 버전 관리 | 바이너리 대형 파일 처리 효율 저하 | LFS(Large File Storage) 최적화 아키텍처 적용 |
| **Dropbox** | 실시간 동기화 | 세밀한 커스텀 권한 설정 복잡성 | 조직 구조 기반의 직관적 RBAC UI 제공 |

---

## 7. 향후 확장 가능성 (Future Possibilities)
*   **AI 기반 자동 파일 분류**: PyTorch를 활용하여 이미지 내 텍스트(OCR) 추출 및 자동 태깅.
*   **분산 합의 알고리즘**: 데이터 일관성 강화를 위해 Raft 알고리즘 기반의 메타데이터 클러스터링 도입.
