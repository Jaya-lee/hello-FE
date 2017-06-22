# material-ui

官网:http://www.material-ui.com/

>Material-UI is a set of React components,

安装

１．装包
```
npm i material-ui -save
npm i react-tap-event-plugin --save

```
2.进入项目，引用
```
import injectTapEventPlugin from 'react-tap-event-plugin';
// Needed for onTouchTap
injectTapEventPlugin();
```
所有的组件均有onTouchTap(),比如点击事件中就需要引用

3.使用
./App.js

```
import React from 'react';
import ReactDOM from 'react-dom';
import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
import MyAwesomeReactComponent from './MyAwesomeReactComponent';

const App = () => (
  <MuiThemeProvider>
    <MyAwesomeReactComponent />
  </MuiThemeProvider>
);

ReactDOM.render(
  <App />,
  document.getElementById('app')
);
```
注意到

```
import RaisedButton from 'material-ui/RaisedButton';
instead of

import {RaisedButton} from 'material-ui';
```
这样使引用的时候速度更快
