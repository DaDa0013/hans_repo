September 26, 2024 - The [PostgreSQL Global Development Group](https://www.postgresql.org)
today announced the release of [PostgreSQL 17](https://www.postgresql.org/docs/17/release-17.html),
the latest version of the world's most advanced open source database.

PostgreSQL 17 builds on decades of open source development, improving its
performance and scalability while adapting to emergent data access and storage
patterns. This release of [PostgreSQL](https://www.postgresql.org) adds
significant overall performance gains, including an overhauled memory management
implementation for vacuum, optimizations to storage access and improvements for
high concurrency workloads, speedups in bulk loading and exports, and query
execution improvements for indexes. PostgreSQL 17 has features that benefit
brand new workloads and critical systems alike, such as additions to the
developer experience with the SQL/JSON `JSON_TABLE` command, and enhancements to
logical replication that simplify management of high availability workloads and
major version upgrades.

"PostgreSQL 17 highlights how the global open source community, which drives the
development of PostgreSQL, builds enhancements that help users at all stages of
their database journey," said Jonathan Katz, a member of the PostgreSQL core
team. "Whether it's improvements for operating databases at scale or
new features that build on a delightful developer experience, PostgreSQL 17
will enhance your data management experience." 

PostgreSQL, an innovative data management system known for its reliability,
robustness, and extensibility, benefits from over 25 years of open source
development from a global developer community and has become the preferred open
source relational database for organizations of all sizes.

### System-wide performance gains

The PostgreSQL [vacuum](https://www.postgresql.org/docs/17/routine-vacuuming.html)
process is critical for healthy operations, requiring server instance resources
to operate. PostgreSQL 17 introduces a new internal memory structure for vacuum
that consumes up to 20x less memory. This improves vacuum speed and
also reduces the use of shared resources, making more available for your
workload.

PostgreSQL 17 continues to improve performance of its I/O layer. High
concurrency workloads may see up to 2x better write throughput due to
improvements with [write-ahead log](https://www.postgresql.org/docs/17/wal-intro.html)
([WAL](https://www.postgresql.org/docs/17/wal-intro.html)) processing.
Additionally, the new streaming I/O interface speeds up sequential scans
(reading all the data from a table) and how quickly
[`ANALYZE`](https://www.postgresql.org/docs/17/sql-analyze.html) can update
planner statistics.

PostgreSQL 17 also extends its performance gains to query execution.
PostgreSQL 17 improves the performance of queries with `IN` clauses that use
[B-tree](https://www.postgresql.org/docs/17/indexes-types.html#INDEXES-TYPES-BTREE)
indexes, the default index method in PostgreSQL. Additionally,
[BRIN](https://www.postgresql.org/docs/17/brin.html) indexes now support
parallel builds. PostgreSQL 17 includes several improvements for query planning,
including optimizations for `NOT NULL` constraints, and improvements in
processing [common table expressions](https://www.postgresql.org/docs/17/queries-with.html)
([`WITH` queries](https://www.postgresql.org/docs/17/queries-with.html)). This
release adds more SIMD (Single Instruction/Multiple Data) support for
accelerating computations, including using AVX-512 for the
[`bit_count`](https://www.postgresql.org/docs/17/functions-bitstring.html)
function.

### 향상된 개발자 경험 확장

PostgreSQL는 [JSON support가 추가된 최초의 관계형 데이터베이스(2012)](https://www.postgresql.org/about/news/postgresql-92-released-1415/)였으며, PostgreSQL 17에서는 SQL/JSON 표준에 대한 구현을 더욱 강화했습니다. 이제 PostgreSQL 17에서는 [`JSON_TABLE`](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-TABLE) 기능이 추가되어, 개발자들이 JSON 데이터를 표준 PostgreSQL 테이블로 쉽게 변환할 수 있게 되었습니다. 또한 PostgreSQL 17은 [SQL/JSON 생성자](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-JSON-CREATION-TABLE)(`JSON`, `JSON_SCALAR`, `JSON_SERIALIZE`)와 [쿼리 함수](https://www.postgresql.org/docs/17/functions-json.html#SQLJSON-QUERY-FUNCTIONS)
(`JSON_EXISTS`, `JSON_QUERY`, `JSON_VALUE`)를 지원하여, 개발자들이 JSON 데이터와 보다 다양한 방식으로 상호작용할 수 있도록 기능을 강화했습니다. 이번 릴리즈에서는 JSON 데이터를 기본 PostgreSQL 데이터 유형으로 변환하는 데 중점을 두고, 숫자, 불리언(boolean), 문자열, 날짜/시간 유형을 포함한 더 많은 [`jsonpath` 표현식](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-PATH-OPERATORS)이 추가되었습니다.

또한 PostgreSQL 17은 조건부 업데이트에 사용되는 [`MERGE`](https://www.postgresql.org/docs/17/sql-merge.html) 기능을 더욱 강화하여, `RETURNING`절과 [뷰](https://www.postgresql.org/docs/17/sql-createview.html) 업데이트 기능을 추가했습니다. 이와 함께 PostgreSQL 17은 대량 데이터 로드 및 데이터 내보내기를 위한 새로운 기능도 도입했으며, 여기에는 [`COPY`](https://www.postgresql.org/docs/17/sql-copy.html) 명령어를 사용하여 큰 사이즈의 행을 내보낼 경우 성능이 최대 2배 향상되는 것도 포함됩니다. 또한 소스와 목적지 인코딩이 일치하는 경우 `COPY`의 성능이 개선되었고, 새롭게 추가된 옵션인 `ON_ERROR` 옵션을 통해 가져오기(import) 과정에서 삽입 오류가 발생하더라도 계속 진행할 수 있게 되었습니다.

이번 릴리즈는 파티션 내 데이터 관리와 원격 PostgreSQL 인스턴스에서 분산된 데이터 관리 기능이 확장되었습니다. PostgreSQL 17은 [partitioned tables](https://www.postgresql.org/docs/17/ddl-partitioning.html)에서 아이덴티티 열과 배제 제약 조건을 지원합니다. 원격 PostgreSQL 인스턴스에서 쿼리를 실행하는 데 사용되는 [PostgreSQL foreign data wrapper](https://www.postgresql.org/docs/17/postgres-fdw.html)([`postgres_fdw`](https://www.postgresql.org/docs/17/postgres-fdw.html))는 이제 EXISTS 및 IN 서브쿼리를 원격 서버로 푸시할 수 있어, 더 효율적인 처리 작업이 가능해졌습니다.

PostgreSQL 17에는 내장형(built-in)이며, 플랫폼에 독립적이고, 불변한, 정렬(collation) 프로바이더가 추가되었습니다. 이 프로바이더는 불변성을 보장하며, C 정렬 규칙과 유사한 정렬 의미론을 제공하지만, SQL_ASCII 대신 UTF-8 인코딩을 사용합니다. 이 새로운 정렬 프로바이더를 사용하면 PostgreSQL을 실행하는 환경에 관계없이 텍스트 기반 쿼리가 항상 동일한 정렬 결과를 반환하도록 보장됩니다.

### 고가용성과 주요 버전 업그레이드를 위한 논리적 복제의 향상된 기능들

[논리적 복제](https://www.postgresql.org/docs/17/logical-replication.html)는 다양한 사용 사례에서 데이터를 실시간으로 스트리밍하는 데 사용됩니다. 그러나 이번 릴리즈 이전에는, 주요 버전 업그레이드를 수행하려는 사용자들이 [logical replication slots](https://www.postgresql.org/docs/17/logical-replication-subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-SLOT)을 삭제해야 했고, 이로 인해 업그레이드 후 구독자들에게 데이터를 다시 동기화해야 하는 번거로움이 있었습니다. 하지만 PostgreSQL 17부터는 주요 버전 업그레이드 시 logical replication slots을 삭제할 필요가 없어졌습니다. 이로 인해 논리적 복제를 사용할 때 업그레이드 프로세스가 간소화되었습니다.

PostgreSQL 17은 논리적 복제를 위한 장애 조치(failover) 제어 기능을 포함하여, 고가용성 환경에서 배포될 때 더욱 탄력적으로 운영될 수 있도록 개선되었습니다. 또한, PostgreSQL 17에서는 물리적 복제본(physical replica)을 새로운 논리적 복제본(logical replica)으로 변환하는 [`pg_createsubscriber`](https://www.postgresql.org/docs/17/app-pgcreatesubscriber.html) 명령어 도구도 도입되었습니다.

### 보안 및 운영 관리를 위한 다양한 옵션

PostgreSQL 17은 사용자가 데이터베이스 시스템의 전체 라이프사이클을 관리할 수 있는 방법을 더욱 확장시켰습니다. PostgreSQL에는 새로운 TLS 옵션인 sslnegotiation이 있습니다. 이 옵션을 통해 [ALPN](https://en.wikipedia.org/wiki/Application-Layer_Protocol_Negotiation) (ALPN 디렉토리에 postgresql로 등록되어있음)을 사용할 때 사용자가 직접 TLS handshake를 수행할 수 있습니다.  PostgreSQL 17은 또한 사용자가 데이터베이스의 유지 관리 작업을 수행할 수 있는 권한을 가진 `pg_maintain`이라는 [predefined role](https://www.postgresql.org/docs/17/predefined-roles.html)을 새로 추가했습니다.

[`pg_basebackup`](https://www.postgresql.org/docs/17/app-pgbasebackup.html)은 PostgreSQL에 포함된 백업 유틸리티로, 현재 증분 백업을 지원하며, 전체 백업을 재구성할 수 있는 [`pg_combinebackup`](https://www.postgresql.org/docs/17/app-pgcombinebackup.html) 유틸리티가 추가되었습니다. 또한, [`pg_dump`](https://www.postgresql.org/docs/17/app-pgdump.html)을 생성할 때 포함할 객체를 선택할 수 있는 새로운 옵션인 `--filter`를 포함하고 있습니다.

PostgreSQL 17은 모니터링 및 분석 기능이 향상되었습니다. 이제 [`EXPLAIN`](https://www.postgresql.org/docs/17/sql-explain.html)은 로컬 I/O 블록 읽기 및 쓰기에 소요된 시간을 보여주며, 데이터 변환시 네트워크 전송에 소요된 시간과 사용된 메모리 양을 확인할 수 있는 두 가지 새로운 옵션인 `SERIALIZE`와 `MEMORY`를 추가했습니다.또한 PostgreSQL 17은 [인덱스 vacuum 진행상황](https://www.postgresql.org/docs/17/progress-reporting.html#VACUUM-PROGRESS-REPORTING)을 보고하며,
[`pg_wait_events`](https://www.postgresql.org/docs/17/view-pg-wait-events.html) 시스템 뷰를 추가했습니다. 해당 뷰는 
[`pg_stat_activity`](https://www.postgresql.org/docs/17/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)와 결합하여 액티브 세션이 대기하는 원인에 대한 더 많은 정보를 제공합니다.

### 추가 변경 사항

PostgreSQL 17에는 다음과 같이 여러 사용 사례에 도움될 수 있는 여러 새로운 기능과 개선 사항이 추가되었습니다.
새로운 기능 및 변경된 기능의 전체 목록은 [release notes](https://www.postgresql.org/docs/17/release-17.html)에서 확인할 수 있습니다.

### PostgreSQL 정보
[PostgreSQL](https://www.postgresql.org) 은 수천 명의 사용자, 기여자, 회사 및 조직의 세계적인 커뮤니티를 보유한 세계 최고 수준의오픈 소스 데이터베이스입니다. 캘리포니아, 버클리 대학교를 시작으로 35년 이상의 엔지니어링 기반으로 구축된 PostgreSQL은 타의 추종을 불허하는 속도로 계속 발전해왔습니다. PostgreSQL의 완성도 높은 기능들은 상용 데이터베이스 시스템과 거의 같으며, 확장성, 보안 및 안정성 측면에서도 뛰어납니다.

### 링크

* [Download](https://www.postgresql.org/download/)
* [Release Notes](https://www.postgresql.org/docs/17/release-17.html)
* [Press Kit](https://www.postgresql.org/about/press/)
* [Security Page](https://www.postgresql.org/support/security/)
* [Versioning Policy](https://www.postgresql.org/support/versioning/)
* [Follow @postgresql](https://twitter.com/postgresql)
* [Donate](https://www.postgresql.org/about/donate/)

## 기능에 대해 자세히 알아보기

기능 및 기타사항에 대한 설명은 다음을 참조하시기 바랍니다. 
리소스:

* [Release Notes](https://www.postgresql.org/docs/17/release-17.html)
* [Feature Matrix](https://www.postgresql.org/about/featurematrix/)

## 다운로드할 위치

PostgreSQL 17을 다운로드할 수 있는 방법은 다음과 같습니다:

* The [공식 다운로드](https://www.postgresql.org/download/) 페이지에는 [Windows](https://www.postgresql.org/download/windows/), [Linux](https://www.postgresql.org/download/linux/), [macOS](https://www.postgresql.org/download/macosx/)등의 설치 프로그램이 포함되어 있습니다.
* [소스코드](https://www.postgresql.org/ftp/source/v17.0)

기타 도구 및 확장 모듈은 [PostgreSQL Extension Network](http://pgxn.org/) 에서 확인하시면 됩니다.

## 문서

PostgreSQL 17 HTML 문서와 man 페이지가 함께 제공되며, 온라인 브라우저에서 [HTML](https://www.postgresql.org/docs/17/)양식과 [PDF](https://www.postgresql.org/files/documentation/pdf/17/postgresql-17-US.pdf) 양식도 제공합니다.

## 라이센스

PostgreSQL uses the [PostgreSQL License](https://www.postgresql.org/about/licence/),
a BSD-like "permissive" license. This
[OSI-certified license](http://www.opensource.org/licenses/postgresql/) is
widely appreciated as flexible and business-friendly, since it does not restrict
the use of PostgreSQL with commercial and proprietary applications. Together
with multi-company support and public ownership of the code, our license makes
PostgreSQL very popular with vendors wanting to embed a database in their own
products without fear of fees, vendor lock-in, or changes in licensing terms.

## Contacts

Website

* [https://www.postgresql.org/](https://www.postgresql.org/)

Email

* [press@postgresql.org](mailto:press@postgresql.org)

## Images and Logos

Postgres, PostgreSQL, and the Elephant Logo (Slonik) are all registered
trademarks of the [PostgreSQL Community Association](https://www.postgres.ca).
If you wish to use these marks, you must comply with the [trademark policy](https://www.postgresql.org/about/policies/trademarks/).

## Corporate Support and Donations

PostgreSQL enjoys the support of numerous companies, who sponsor developers,
provide hosting resources, and give us financial support. See our
[sponsors](https://www.postgresql.org/about/sponsors/) page for some of these
project supporters.

There is also a large community of
[companies offering PostgreSQL Support](https://www.postgresql.org/support/professional_support/),
from individual consultants to multinational companies.

If you wish to make a financial contribution to the PostgreSQL Global
Development Group or one of the recognized community non-profit organizations,
please visit our [donations](https://www.postgresql.org/about/donate/) page.





