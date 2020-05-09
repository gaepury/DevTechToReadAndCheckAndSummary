# Chapter별 Check List
- [x] Introduction for Graph QL class
- [x] Problems solved by GraphQL
- [x] Creating a GraphQL Server with GraphQL Yoga
- [x] Creating the first Query and Resolver
- [x] Extending the Schema
- [x] Extending the Schema part Two
- [x] Creating Queries with Arguments
- [x] Defining Mutations
- [x] Creating first Mutation
- [x] Delete Mutation
- [x] Wrapping a REST API with GraphQL Part One
- [x] Wrapping a REST API with GraphQL Part Two
- [x] Overview to the final API


# Chapter별 Summary
## 1. Introduction for Graph QL class, Problems solved by GraphQL
* graphql-yoga 설치
* Over-fetching, Under-fetching
    * 하나의 쿼리로 위의 두문제를 모두 해결 가능

---

## 2. Creating a GraphQL Server with GraphQL Yoga
* GraphQL 서버 설정
``` javascript
import { GraphQLServer } from "graphql-yoga";
console.log('aa3')

const server = new GraphQLServer({

});

server.start(() => console.log("GraphQL Server Running"));
```

---

## 3. Creating the first Query and Resolver
* schema
    * 주거나 줄 데이터에 대한 서술
* query/
    * schema.graphql
    * resolvers.js
        * query를 resolve한다
        * resolver를 원하는대로 프로그래밍
            * 메모리, DB, API등 
    * Query를 설명하고(schema.graphql) resolver(resolvers.js)를 프로그래밍
* npm run start후 localhost:4000접속하면 graphql playground(graphql-yoga)가 나옴
    * test
        * query {name}
        
---

## 4. Extending the Schema 1, 2
### Extending the Schema 1
* Query 했을때 Flow 
    * Query 를 보내면 Query Schema를 찾고 맞는 Resolver를 찾는다
* Query Schema와 Resolver간에 키, 타입이 일치해야함
* GraphQL 요청은 항상 Post요청
* Person type 생성
    * name, age, gender
    * schema.graphql
       ``` graphql
        type Persion {
            name: String,
            age: Int,
            gender: String
        }
        type Query {
            person: Person
        }
       ```
    * resolver.js
        ``` javascript 
        const nohjunho = {
          name: "nohjunho",
          age: "30",
          gender: "mail"
        }
         
        const resolvers = {
          Query: {
            person: () => nohjunho
          }
        }
        
        export default resolvers
        ```

### Extending the Schema 2
* Query, Mutation, Subscription
* Array & 필수
    * [Person]!
* schema.graphql
    * people query 추가, Person Type id 추가
    ``` graphql
    type Person {
        id: Int!,
        name: String!,
        age: Int!,
        gender: String!
    }
    type Query {
        people: [Person]!
        person(id: Int!): Person
    }
    ```

---

## 5. Creating Queries with Arguments
*  !을 붙이면 값이 없을시 에러, 안붙이면 null 반환
    ``` graphql
    type Query {
      people: [Person]!
      person(id: Int!): Person!
    }
    ```
* 인자 전달하기
    * resolvers.js
       ``` javascript
       const resolvers = {
        Query: {
          people: () => people,
          person: (object, { id }) => getById(id)
        }
       }
    * playground
       ``` graphql
       {
         person(id: 2) {
           id
           name
         }
       }
     
---

## 6. Defininig Mutations, Creating first Mutation, Delete Mutation
### Defining Mutations
* movie관련 Query Schema, resolver, db 작성
    * People, person을 Movie 형태로 변경
### Creating fist Mutation, Delete Mutation
* db
``` javascript 
export const addMovie = (name, score) => {
  const newMovie = {
    id: movies.length + 1,
    name,
    score
  }
  movies.push(newMovie);
  return newMovie;
}

export const deleteMovie = id => {
  const cleanMovies = movies.filter(movie => movie.id !== id);

  if (movies.length > cleanMovies.length) {
    movies = cleanMovies;
    return true
  } else {
    return false;
  }
}

```
* resolvers
``` javascript
const resolvers = {
  Query: {
    movies: (_, { limit, rating }) => getMovies(limit, rating),
    movie: (_, { id }) => getMovie(id),
    suggestions: (_, { id }) => getSuggestions(id),
  },
}
```

* schema
``` graphql
type Query {
    movies(limit: Int, rating: Float): [Movie]!,
    movie(id: Int!): Movie!
    suggestions(id: Int!): [Movie]!
}
```

* playground
``` graphql
mutation {
  addMovie(name: "토르3", score: 8.2) {
    name
  }
}

mutation {
  deleteMovie(id: 0) 
}
```

---

## 7. Wrapping a REST API with GraphQL Part 1, 2, Overview to the final API
* db
``` javascript
import axios from "axios"

const BASE_URL = "https://yts.am/api/v2/";
const LIST_MOVIES_URL = `${BASE_URL}list_movies.json`
const MOVIE_DETAIL_URL = `${BASE_URL}movie_details.json`
const MOVIE_SUGGESTIONS_URL = `${BASE_URL}movie_suggestions.json`

export const getMovies = async (limit, rating) => {
  const {
    data: {
      data: { movies }
    }
  } = await axios(LIST_MOVIES_URL, {
    params: {
      limit,
      minimum_rating: rating
    }
  });

  return movies;
}


export const getMovie = async id => {
  const {
    data: {
      data: { movie }
    }
  } = await axios(MOVIE_DETAIL_URL, {
    params: {
      movie_id: id
    }
  });

  return movie;
};

export const getSuggestions = async id => {
  const {
    data: {
      data: { movies }
    }
  } = await axios(MOVIE_SUGGESTIONS_URL, {
    params: {
      movie_id: id
    }
  });

  return movies;
};
```

* resolver
``` javascript
const resolvers = {
  Query: {
    movies: (_, { limit, rating }) => getMovies(limit, rating),
    movie: (_, { id }) => getMovie(id),
    suggestions: (_, { id }) => getSuggestions(id),
  },
}
```

* schema
``` graphql 
type Movie {
    id: Int,
    title: String!,
    rating: Float,
    summary: String!,
    language: String!,
    medium_cover_image: String!
}

type Query {
    movies(limit: Int, rating: Float): [Movie]!,
    movie(id: Int!): Movie!
    suggestions(id: Int!): [Movie]!
}
```

* playground
``` graphql
query {
  movie(id:17392) {
    id
    title
    rating
  }
  suggestions(id:17392) {
    id,
    title
  }
}
```

## 참고 샘플 코드
클론: https://github.com/gaepury/movieql
원본: https://github.com/nomadcoders

