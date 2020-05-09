# Chapter별 Check List
- [x] Setup and project outline
- [x] Setting up an Apollo Client
- [x] Setting up React Router
- [x] Getting data from the GraphQL API part One
- [x] Getting data from the GraphQL API part Two
- [x] Details Route with params
- [x] Creating a Query with variables
- [x] Conclusions

# Chapter별 Summary
## 1. Setup and project outline, Setting up an Apollo Client, Setting up React Router
* Movieql server, client 멀티 모듈 세팅
   * https://github.com/gaepury/movieql
   * npm-run-all 으로 client, server 동시 실행
   * package.json
``` javascript
{
  "name": "movieql",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "main": "index.js",
  "scripts": {
    "start": "npm-run-all --parallel dev:**",
    "dev:client": "react-scripts start",
    "dev:server": "nodemon --exec babel-node server/index.js",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.9.6",
    "@babel/node": "^7.8.7",
    "@babel/preset-env": "^7.9.6",
    "npm-run-all": "^4.1.5"
  },
  "dependencies": {
    "@apollo/react-hooks": "^3.1.5",
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "apollo-boost": "^0.4.8",
    "axios": "^0.19.2",
    "graphql": "^15.0.0",
    "graphql-yoga": "^1.18.3",
    "node-fetch": "^2.6.0",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-router-dom": "^5.1.2",
    "react-scripts": "3.4.1"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}

```

* Apollo client
   * https://www.apollographql.com/docs/react/get-started/
   * npm install apollo-boost @apollo/react-hooks graphql
      * v2.6기준 (강의와 조금 다름), 3.0 beta나옴
* APollo react dev tool 설치
   * client에서 api query docs를 볼수있고 playground처럼 실행해볼수 있음
* Setting up React Router
``` javascript
import React from 'react';
import { HashRouter as Router, Switch, Route } from "react-router-dom";
import { ApolloProvider } from '@apollo/react-hooks';
import client from "./apollo"

import Home from "./Home"
import Detail from "./Detail"

function App() {
  return (
      <ApolloProvider client={client}>
        <Router>
          <Switch>
            <Route exact={true} path={"/"} component={Home}/>
            <Route path={"/detail/:movieId"} component={Detail}/>
          </Switch>
        </Router>
      </ApolloProvider>
  );
}

export default App;
```

---

## 2. Getting data from the GraphQL API part 1, 2
### * Getting data from the GraphQL API part 1
* graphql-tag
``` javascript
import gql from 'graphql-tag'


export const HOME_PAGE = gql `
  {
    movies(limit: 10, rating: 8.0) {
      id
      title
      genres
    }
  }
```

### Getting data from the GraphQL API part 2
- Home
``` javascript 
import React from "react";
import {useQuery} from '@apollo/react-hooks'
import {HOME_PAGE} from "./query"

const Home = () => {
  const {loading, data, error} = useQuery(HOME_PAGE)
  if (loading) return <span>loading..</span>
  if (error) return <span>something happend..</span>

  return data.movies.map(movie => <h2 key={movie.props}>{movie.title} / {movie.rating}</h2>)
}

export default Home;
```

---

## 3. Details Route with params
- ![image](https://user-images.githubusercontent.com/20143765/81477972-7b7ebb80-9255-11ea-991a-129023a888fb.png)
   - match.params.movieId 를 깔끔하게 가져오는 방법

---

## 4. Creating a Query with variables
* param(movie id)를 받아오는 부분은 apollo 문법(graphql이랑은 별도)
    * 받아온 movie id를 가지고 movie, suggestion query 만듬 
    
``` javascript
export const MOVIE_DETAILS = gql`
  query getMovieDetails($movieId: Int!) {
    movie(id: $movieId) {
      medium_cover_image
      title
      rating
      description_intro
      language
      genres
    }
    suggestions(id: $movieId) {
      id
      title
      rating
      medium_cover_image
    }
  }
`;
```

---

## 5. Conclusion
* cache, fetch, state, loading, error등을 매직같이 처리해준다. 너무 아름답다.



## 참고 샘플 코드
클론: https://github.com/gaepury/movieql
원본: https://github.com/nomadcoders
