<img src="https://rackt.github.io/react-router/img/vertical.png" width="300">

[![npm package](https://img.shields.io/npm/v/react-router.svg?style=flat-square)](https://www.npmjs.org/package/react-router)
[![build status](https://img.shields.io/travis/rackt/react-router/master.svg?style=flat-square)](https://travis-ci.org/rackt/react-router)
[![Coverage Status](https://img.shields.io/coveralls/rackt/react-router.svg?style=flat-square)](https://coveralls.io/github/rackt/react-router)
[![#rackt on freenode](https://img.shields.io/badge/irc-rackt_on_freenode-61DAFB.svg?style=flat-square)](https://webchat.freenode.net/)

A complete routing library for React

React Router keeps your UI in sync with the URL. It has a simple API
with powerful features like lazy code loading, dynamic route matching,
and location transition handling built right in. Make the URL your first
thought, not an after-thought.

### Docs & Help

- [Guides and API Docs](/docs)
- [Upgrade Guide](/UPGRADE_GUIDE.md)
- [Changelog](/CHANGELOG.md)
- [#react-router channel on reactiflux](http://www.reactiflux.com/)

**Note:** *If you are still using React Router 0.13.x [the docs](https://github.com/rackt/react-router/tree/0.13.x/docs/guides) can be found on [the 0.13.x branch](https://github.com/rackt/react-router/tree/0.13.x).*

### Browser Support

We support all browsers and environments where React runs.

### Installation

#### npm + webpack/browserify

Install using [npm](https://www.npmjs.com/):

    $ npm install history react-router@latest

Note that you need to also install the [history](https://www.npmjs.com/package/history) package since it is a peer dependency of React Router and won't automatically be installed for you in npm 3+.

Then with a module bundler or webpack, use as you would anything else:

```js
// using an ES6 transpiler, like babel
import { Router, Route, Link } from 'react-router'

// not using an ES6 transpiler
var Router = require('react-router').Router
var Route = require('react-router').Route
var Link = require('react-router').Link
```

You can require only the pieces you need straight from the `lib` directory:

```js
import Router from 'react-router/lib/Router'
```

### UMD

There's also a UMD build in the `umd` directory:

```js
// using an es6 transpiler, like babel
import { Router, Route, Link } from 'react-router/umd/ReactRouter'

// using globals
var Router = window.ReactRouter.Router;
var Link = window.ReactRouter.Link;
var Route = window.ReactRouter.Route;
```

#### CDN

If you just want to drop a `<script>` tag in your page and be done with it, you can use the UMD/global build [hosted on cdnjs](https://cdnjs.com/libraries/react-router).

### What's it look like?

```js
import React from 'react'
import { render } from 'react-dom'
import { Router, Route, Link } from 'react-router'

const App = React.createClass({/*...*/})
const About = React.createClass({/*...*/})
// etc.

const Users = React.createClass({
  render() {
    return (
      <div>
        <h1>Users</h1>
        <div className="master">
          <ul>
            {/* use Link to route around the app */}
            {this.state.users.map(user => (
              <li key={user.id}><Link to={`/user/${user.id}`}>{user.name}</Link></li>
            ))}
          </ul>
        </div>
        <div className="detail">
          {this.props.children}
        </div>
      </div>
    )
  }
})

const User = React.createClass({
  componentDidMount() {
    this.setState({
      // route components are rendered with useful information, like URL params
      user: findUserById(this.props.params.userId)
    })
  },

  render() {
    return (
      <div>
        <h2>{this.state.user.name}</h2>
        {/* etc. */}
      </div>
    )
  }
})

// Declarative route configuration (could also load this config lazily
// instead, all you really need is a single root route, you don't need to
// colocate the entire config).
render((
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About}/>
      <Route path="users" component={Users}>
        <Route path="/user/:userId" component={User}/>
      </Route>
      <Route path="*" component={NoMatch}/>
    </Route>
  </Router>
), document.body)
```

See more in the [Introduction](/docs/Introduction.md), [Advanced Usage](/docs/guides/advanced/README.md), and [Examples](/examples).

### Thanks

React Router was initially inspired by Ember's fantastic router. Many thanks to the Ember team.

Also, thanks to [BrowserStack](https://www.browserstack.com/) for providing the infrastructure that allows us to run our build in real browsers.
