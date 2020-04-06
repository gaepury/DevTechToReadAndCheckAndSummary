
# Chapter별 Check List
- [x] 1. GraphQL에 오신 것을 환영합니다.
- [x] 2. 그래프 이론
- [ ] 3. GraphQL 쿼리어
- [ ] 4. 스키마 설계하기
- [ ] 5. GraphQL API 만들기
- [ ] 6. GraphQL 클라이언트
- [ ] 7. 실제 제품을 위한 GraphQL


# Chapter별 Summary
## 1, 2. GraphQL에 오신 것을 환영합니다, 그래프 이론
- GraphQL 엔드포인트를 만들어 Rest 엔드포인트의 데이터를 가져오는 방식은 점진적으로 GraphQL을 도입할 수 있는 훌륭한 전략

## 3. GraphQL 쿼리어
- GraphQL 데이터는 저장환경을 가리지 않는다.(단일 데이터베이스, 여러 데이터베이스, 파일시스템, Rest API, 웹소켓, 또 다른 GraphQL API 등등)
- Query(조회), Mutation(수정), Sucscription(소켓 연결로 전달되는 데이터 변경사항 감지)
- 쿼리는 단순한 문자열로 GraphQL 엔드포인트로 Post 요청 본문에 담겨 전달
### GraphQL API 툴
- GraphiQL, GraphQL 플레이그라운드
   - GraphQL 플레이그라운드 웹버전: https://www.graphqlbin.com/v2/new
   - GraphQL 플레이그라운드 데스크톱앱 설치: https://github.com/prisma-labs/graphql-playground/releases
- 공용 GraphQL API
   - SWAPI, Github API, Yelp 등
   - https://github.com/APIs-guru/graphql-apis
### GraphQL 쿼리
- query lifts {}
   - query: GraphQL 타입(루트타입), 타입 하나가 곧 하나의 작업을 수행, 작업이 곧 쿼리문서의 루트를 의미
   - API 문서를 보면 Query 타입으로 선택할수 있는 필드가 나와있음.
- 셀렉션 세트
   - 중괄호로 묶인 블록
   - 서로 중첩 가능
   - 별칭 부여
      - ex: ```chairlifts: allLifts {}```
- 쿼리 인자
   - 키-값쌍
   - ex: ```allLifts(status: CLOSED) {}```
- 필드
   - 스칼라타입: 정수, 실수, 문자열, 불, 고유 식별자(ID)
      - 고유식별자: 반드시유일한문자열반환) 
   - 객체타입
   
 
