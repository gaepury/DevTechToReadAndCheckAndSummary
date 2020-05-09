# Chapter별 Check List
- [x] Setup and project outline
- [x] Setting up an Apollo Client
- [ ] Setting up React Router
- [ ] Getting data from the GraphQL API part One
- [ ] Getting data from the GraphQL API part Two
- [ ] Details Route with params
- [ ] Creating a Query with variables
- [ ] Conclusions

# Chapter별 Summary
## 1. 1. Setup and project outline, Setting up an Apollo Client
* Movieql server, client 멀티 모듈 세팅
   * https://github.com/gaepury/movieql
* Apollo client
   * https://www.apollographql.com/docs/react/get-started/
   * npm install apollo-boost @apollo/react-hooks graphql
      * v2.6기준 (강의와 조금 다름), 3.0 beta나옴
* APollo react dev tool 설치
   * client에서 api query docs를 볼수있고 playground처럼 실행해볼수 있음
* Setting up React Router
```
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
