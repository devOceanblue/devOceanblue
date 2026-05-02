<!-- =========================
Kim Seungyoon (김승윤)
========================== -->

# 김승윤 | Seungyoon Kim
백엔드 개발자라는 타이틀보다는 유량(트래픽, 데이터)이 있는곳에서 복잡한 파이프라인을 고치고 운영하는   
배관공으로 스스로를 정의합니다.    
  
성능/안정성/데이터 신뢰도 · Observability 기반 문제 해결

📍 Seoul, KR  
📧 neptuner24@gmail.com · 📱 +82 010-9292-2495  
🌐 Portfolio: https://portfolio-mu-wheat-53.vercel.app/  
🧑‍💻 GitHub: https://github.com/devOceanblue

---

## Highlights
- **성능/병목 개선**: 실행계획 기반 튜닝, 분포/Heavy hitter 진단, p95/p99 기준으로 개선-검증
- **운영 안정성**: 장애 전파 차단, 롤백/Degrade-safe, 재현 가능한 원인 분석(RCA), Runbook 지향
- **데이터 신뢰도**: 멱등/체크포인트, 스키마 검증, 배치 안정성, 재처리/리플레이 통제
- **Search/Rec + LLM/Agent**: 데이터 파이프라인 + 검색/랭킹/리랭크 + Context Engineering에 집중

---

## Pinned / Featured
- 📚 **Book Search Labs** — production-grade search/retrieval pipeline  
  https://github.com/book-search-labs/bsl-backend
- 🧪 **distributed-systems-reliability-lab** — Kafka/Redis/MySQL 실패모드 실험 & 관측  
  https://github.com/devOceanblue/eventing-reliability-lab

---

## Side Projects

### 📚 Book Search Labs (2025 – Present)
**Java/Spring Boot · Python · MySQL · OpenSearch(Hybrid) · Redis · Kafka · OTel**  
- 10GB+ 도서 메타데이터(JSON-LD) **수집/정규화/적재 파이프라인**: 체크포인트, payload hash 중복방지, 스키마 검증
- MySQL **SSOT(정규 스키마 Canonical)** + Flyway migration 기반 재현 가능한 환경
- OpenSearch **index template + alias-swap(blue/green) 무중단 리인덱싱**, 즉시 롤백 절차
- QueryContext(qc.v1.x) 계약으로 **서비스 경계/contract 중심 설계**
- OTel 기반 trace_id 전파 + 단계별 latency/품질 지표(0-result 등) 메트릭화

---

### 🗂️ AutoDoc Tree — 문서 자동 정리 서비스 (2025 – Present)
**Kotlin/Spring Boot · React(TS) · MySQL · OpenSearch(BM25+Vector) · Redis · S3/MinIO · OTel**
- 업로드만 하면 **문서를 2-depth 트리(가상 폴더)**로 자동 분류/스냅샷 생성
- 멀티테넌시(Workspace=Tenant) 기반 **API/DB/Search/Cache/ObjectStorage 격리**
- Outbox + Worker 파이프라인: ingest → embedding → index → tree, **stage-level idempotency + DLQ/재처리**
- PDF/DOCX/TXT/MD 텍스트 추출 후 섹션/청크 임베딩 저장, 검색/클러스터링/라벨링에 활용
- 배치 근거를 제공하는 **Explainable placement(신뢰도 확보)** + 안정성(급변 방지/locked 노드)

---

### 🧪 distributed-systems-reliability-lab (2025 – Present)
**Kafka · Redis · MySQL · Spring Boot · Docker Compose · Prometheus/Grafana · OTel · k6**  
- Outbox/Relay/Processed-event 기반 **at-least-once** 환경에서 유실/중복/정합성 리스크를 **실험(E-001~)** 으로 재현
- DLQ/Retry/Replay 운영 흐름 실험 + runbook 정리
- Kafka 내구성(HW/LEO/LSO, read_committed, ISR/min.insync.replicas/acks) 해석 가이드
- Redis 실패/오남용(cache stampede, hot key/shard, cluster slot/CROSSSLOT) 재현 및 완화
- 대시보드(consumer lag, outbox age, DLQ rate, cache hit/miss, DB QPS)로 **성공/실패를 수치로 검증**

---

### 🏨 StayVista — 통합 여행 플랫폼(OTA) (2025 – Present)
**Kotlin/Spring Boot · React · MySQL · Redis · Kafka · OpenSearch · OTel · k6**
- 숙소/티켓/체험/패키지 예약을 **단일 Booking 도메인**으로 수렴(카탈로그 vs 예약 책임 분리)
- 숙소 재고는 날짜별 inventory 모델 + **조건부 원자 UPDATE(reserved+sold < total)** 로 과판매 방지
- **HOLD → CONFIRM** 모델 + Idempotency Key로 중복예약/중복결제 방지
- 패키지는 Saga(오케스트레이션) + 보상 트랜잭션, 외부효과는 Outbox로 비동기화
- 특가 폭주 대비: rate-limit/queue token/backpressure, p95/p99 latency budget 기반 timeout/degrade 정의
- OTel 기반 RED 메트릭 + 예약/재고 지표(HOLD age, sell-through, queue depth) 관측

---

### 🪙 Crypto Exchange Platform — 암호화폐 거래소(Spot) (2025 – Present)
**Rust · Go · Kotlin/Spring · PostgreSQL · Kafka/Redpanda · Flink · Redis · ClickHouse · OTel · K8s/GitOps**
- Matching/Risk hot-path를 **Rust 단일-writer 이벤트 루프**로 구성 + WAL(snapshots+replay)로 결정적 복구
- **Commit line**(WAL durable write 이후 publish)으로 체결 이벤트 유실/순서역전 리스크 제거
- PostgreSQL **복식부기(double-entry) 원장(append-only)** + 멱등 정산 컨슈머(DLQ/Replay)
- 체결 스트림 → Flink 집계로 candles/ticker 생성, Redis hot snapshot + ClickHouse history 분리
- WebSocket fan-out: snapshot+delta, seq gap recovery, backpressure, conflation 정책
- 운영/보안: settlement lag/불변식 위반/split-brain 감지, **CANCEL_ONLY/HALT** 안전장치 Runbook

---

## What I Care About (Engineering)
- **Performance**: 실행계획/쿼리·인덱스 설계, 분포 기반 병목 제거, p95/p99 latency budget
- **Reliability**: 장애 전파 차단, 멱등/재처리/리플레이, DLQ·Runbook, Degrade-safe
- **Data Trust**: 체크포인트, 스키마 검증, 샘플링 기반 정합성 검증, Backfill 통제
- **Architecture**: service boundary/contract, 이벤트/트랜잭션 경계 단순화, 관측성 내장(Logs·Metrics·Traces)

---

## Tech Stack
**Languages**: Java, Kotlin, Python, Go, Rust, SQL, JavaScript/TypeScript  
**Backend**: Spring Boot, FastAPI  
**Data/Infra**: MySQL, PostgreSQL, Redis, Kafka/Redpanda, OpenSearch/Elasticsearch, ClickHouse  
**Cloud/DevOps**: AWS, GCP, Docker, Kubernetes, GitOps

---

## Contact
- Email: neptuner24@gmail.com  
- Portfolio: https://portfolio-mu-wheat-53.vercel.app/  
- GitHub: https://github.com/devOceanblue
