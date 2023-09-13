### Elasticsearch

Apache Lucene(아파치 루씬) 기반의 java 오픈소스 분산 검색 엔진입니다.

"데이터 저장소"가 아니라 MySQL같은 데이터베이스를 대체할 수 없습니다.

방대한 양의 데이터를 신속하고 거의 실시간으로 저장,검색,분석할 수 있습니다.

Elasticsearch는 검색을 위해 단독으로 사용되기도 하며, ELK( Elasticsearch / Logstatsh / Kibana )스택으로 사용되기도 합니다.

---

### ELK( Elasticsearch / Logstatsh / Kibana ) 스택

ELK는 위 그림과 같이, 분석 및 저장 기능을 담당하는 ElasticSearch, 수집 기능을 하는 Logstash, 이를 시각화하는 도구인 Kibana의 앞글자만 딴 단어입니다.

ELK는 접근성과 용이성이 좋아 최근 가장 핫한 Log 및 데이터 분석 도구입니다.

ⓐ Logstatsh
: 다양한 소스(DB, csv파일 등)의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elasticsearch 로 전달

ⓑ Elasticsearch
: Logstatsh로 부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득

ⓒ Kibana
: Elasticsearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링


### Elasticsearch 핵심 개념

1. 클러스터
: 클러스터는 하나 이상의 노드(서버)가 모인 것이며, 이를 통해 전체 데이터를 저장하고 모든 노드를 포관하는 통합 색인화 및 검색 기능을 제공합니다. 클러스터는 고유한 이름으로 식별 되는데, 기본 이름은 "elasticsearch"입니다.

2. 노드
: 노드는 클러스터에 포함된 단일 서버로서 데이터를 저장하고 클러스터의 색인화 및 검색 기능에 참여한다. 노드는 클러스터처럼 이름으로 식별되는데, 기본이름은 시작 시 노드에 지정되는 임의 UUID(Universally Unique Identifier)이다. 기본이름 대신 특정 이름으로 정의 가능하다. 네트워크의 어떤 서버가 Elasticsearch 클러스터의 어떤 노드에 해당하는지 식별해야 하기 때문에 노드의 이름은 관리의 목적에서 중요하다.

3. 인덱스
: 색인은 다소 비슷한 특성을 가진 문서의 모음이다. 이를테면 고객 데이터에 대한 색인, 제품 카탈로그에 대한 색인, 주문 데이터에 대한 색인을 각각 둘 수 있다. 색인은 이름(모두 소문자여야함)으로 식별되며, 이 이름은 색인에 포함된 문서에 대한 색인화, 검색, 업데이트, 삭제 작업에서 해당 색인을 가르키는데 쓰인다.

4. 타입
: 하나의 색인에서 하나 이상의 유형을 정의할 수 있다. 유형이란 색인을 논리적으로 분류/구분한 것이며 그 의미 체계는 전적으로 사용자가 결정한다. 일반적으로 여러 공통된 필드를 갖는 문서에 대해 유형이 정의 된다. 예를 들어 블로그 플랫폼을 운영하고 있는데 모든 데이터를 하나의 색인에 저장한다고 가정하면 이 색인에서 사용자 데이터, 블로그 데이터, 댓글 데이터에 대한 유형을 각각 정의할 수 있다.

5. 도큐먼트
: 도큐먼트는 색인화 할 수 있는 기본 정보 단위이다. 예를 들어 어떤 단일 고객, 단일 제품, 단일 주문에 대한 도큐먼트가 각각 존재할 수 있다. 이 문서는 JSON(JavaScript Object Notation)형식인데, 이는 널리 사용되는 인터넷 데이터 교환 형식이다.

6. 샤드 & 리플리카
: 색인은 방대한 양의 데이터를 저장할 수 있는데, 이 데이터가 단일 노드의 하드웨어 한도를 초과할 수도 있다. 예를 들어 10억 개의 문서로 구성된 하나의 색인데 1TB의 디스크 공간이 필요할 경우, 단일 노드의 디스크에서 수용하지 못하거나 단일 노드에서 검색 요청 처리 시 속도가 너무 느려질 수 있다.