# Numenta Unicorn

> Cross-platform Desktop Application to demonstrate basic HTM functionality to
> users using their own data files.

<p style="color:red; font-size:200%;">CURRENTLY UNDER HEAVY DEVELOPMENT!</p>


## Repository

The `gui/` directory contains Cross-platform Desktop Application GUI code,
running Javascript/HTML/CSS/etc. on [Node.js](https://nodejs.org/),
[Electron](https://github.com/atom/electron), and
[Google Chromium](https://www.chromium.org/Home). This code exposes the
functionality of the HTM Engine in the sibling `engine/` directory.

The `engine/` directory contains NuPIC HTM Engine and Util code (Python / C++),
which drives the main functionality of the app, which it is our goal to demo
to the user.

```shell
DEPENDENCIES.md     # Module dependency overview file
LICENSE.txt         # Dual: Commercial and GPLv3
README.md           # This file, a project overview
engine/             # NuPIC HTM Engine and Utils, Python/C++ code here!
  README.md         # Overview for HTM/NuPIC part of project
  requirements.txt  # Engine main Python module dependencies
gui/                # GUI that exposes NuPIC HTM functionality to the User
  browser/          # Javascript, HTML, CSS act as GUI inside browser window
    bundle.js       # WebPack automated output compiled Javascript bundle
    index.html      # App main startup browser window contents
    css/            # GUI Styles for App in browser
    img/            # GUI Imagery for App in browser
    js/             # GUI Javascript for App in browser
      app.js        # GUI Web App entry point script, compiles to bundle.js
  lib/              # Javascript that lives outside the browser window
  main.js           # Electron App entry point, creates browser GUI window(s)
  test/             # GUI Unit and Web tests run by Mocha
    unit/           # GUI Unit tests (code)
    web/            # GUI Web tests (user)
gulpfile.js         # Config file for the Gulp build tool
node_modules/       # Where `npm` installs packages to
package.json        # Node.js `npm` packages, dependencies, and App config
```


## Technology

### Engine

> See: `engine/requirements.txt`

* Languages:
  * [Python](http://python.org)
  * [C++](https://isocpp.org/)
* Machine Intelligence:
  * [NuPIC](htts://github.com/numenta/nupic)

The Machine Intelligence behind this app is a technology known as Hierarchical
Temporal Memory (HTM). NuPIC is Numenta's open source HTM engine. NuPIC runs
on streams of data, predicting future values, and detecting pattern anomalies.

### GUI

> See: `package.json`

* Languages:
  * Javascript
    * [ECMAScript 5.1](https://es5.github.io/) (>= IE9)
    * [ECMAScript 6](https://babeljs.io/docs/learn-es2015/) (aka ES2015) via
      [Babel](https://babeljs.io/)
  * [HTML5](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)
  * [CSS3](https://developer.mozilla.org/en-US/docs/Web/CSS) with
    [SASS](http://sass-lang.com/) via
    [node-sass](https://github.com/sass/node-sass)
* Framework: [Electron](https://github.com/atom/electron)
  * Engines: [Chromium](https://www.chromium.org/Home),
    [IO.js](https://iojs.org/), [Node](https://github.com/joyent/node)
  * Module Loader: [WebPack](https://github.com/webpack/webpack)
  * User Interface:
    * Architecture: [Fluxible](http://fluxible.io/)
      ([Flux](https://facebook.github.io/flux/docs/overview.html#content)
      Uni-directional data flow)
    * View Components: [React](https://github.com/facebook/react),
      [JSX](https://facebook.github.io/jsx/)
* Testing:
  * Test Runner, Unit Tests: [Mocha](https://github.com/mochajs/mocha)
  * Web Tests: [Casper](https://github.com/n1k0/casperjs)
* Tooling:
  * Streaming builder: [Gulp](https://github.com/gulpjs/gulp)
  * JS transpiling (ES6, JSX, etc): [Babel](https://github.com/babel/babel)
* @TODO for future:
  * JS formatting: [jsfmt](https://github.com/rdio/jsfmt) - no ES6 yet

The GUI for this application is web code. Javascript, HTML, and CSS are loaded
into a browser. For Desktop, this browser is a bare-bones Chrome window opened
by the Electron framework. Electron also runs IO.js (Node.js edge) to connect
with the host Operating System, allowing for cross-platform native controls.

In the browser, we run a one-way Uni-directional data flow, an Architecture
known as "Flux".

Below is an example of tracing of our way through GUI initialization, GUI first
loop run, and GUI loop continuation:

1. Electron loads `gui/main.js`
1. .. which (or Browser directly) loads `gui/browser/index.html`
1. .. which loads `gui/browser/js/app.js`
1. .. which inits Fluxible
1. .. and then Fluxible fires off an initial Action
1. .. which dispatches Events with state data to Stores
1. .. which then integrate state data into themselves
1. .. and then View Components tied to updated Stores render
1. .. and then The User interacts with the app firing off a new Action
1. .. GOTO #6, RINSE and REPEAT.


## Development

### Setup

Example of setting up development environment:

```shell
brew install git node  # darwin
git clone https://github.com/numenta/numenta-apps
cd numenta-apps/unicorn
npm install
```

### Targets

#### Desktop App

Start code via Electron as a Desktop App:

```shell
npm run start
```

#### Web App

This is *nice-to-have*, and *not* required like the Desktop App. The more this
Web version stays synced with the Desktop version, the easier it will be to
later port this to a real Web App, or to Android/iOS mobile via
[React Native](https://facebook.github.io/react-native/).

Start app on local webserver, you can open it with Chrome Browser
at `http://localhost:9999`:

```shell
npm run dev
```


## Guidelines

* HTML and CSS
  * [Living Styleguide]() @TODO
* Javascript
  * [ES5 Styleguide](https://github.com/felixge/node-style-guide)
  * ES6 styleguide? AirBnB? @TODO