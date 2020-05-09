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
