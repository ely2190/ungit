These are the contributing guidelines as well as some documentation on how the code is structured. Read up before contributing to make everything as smooth as possible.

Posting issues
==============

Just common sense; do a quick search before posting, someone might already have created an issue (or resolved the problem!). If you're posting a bug; try to include as much relevant information as possible (ungit version, node and npm version, os, any git errors displayed, output from cli console and output from the browser console).

Developing for Ungit
====================

I do accept pull requests, but I also reserve the right to not do so for things I don't think fit with Ungit. If you are developing anything new you should almost always also provide tests for it, preferably clicktests but it doesn't hurt to write REST-interface tests as well if applicable. Try to post pull requests early, even at a concept stage, to get feedback and increase chances it's merged.

What you need to get started
----------------------------

You'll need the same as for Ungit; node, npm and git. You will also need grunt (`npm install -g grunt-cli`).

Getting started
---------------

To get started developing on Ungit:

 1. Make sure you have [node.js](http://nodejs.org), [npm](https://npmjs.org/), [git](http://git-scm.com/) and [grunt](http://gruntjs.com/) installed.
 2. Clone the repository to a local directory.
 3. Run `npm install` to install dependencies.
 4. Run `grunt` to build (compile templates, css and js).
 5. Type `npm start` to start ungit, or `npm test` to run tests.
 6. (Optional). Run `grunt watch` to automatically rebuild stuff when you change files.

Architecture overview
---------------------

Ungit has two major parts; the server and the ui. The server exposes a REST interfaces, which enables it to be run on a remote server. The UI is a single-page web-app, built using Knockout.js.

Folders
-------

* `assets/` Raw assets used for development.
* `bin/` "Binary" files, the ungit launcher script and the credentials-helper, which is invoked by git to acquire credentials when using http authentication.
* `clicktests/` Phantom.js clicktest; basically tests that run on the rendered DOM. Since these run all the way, from the DOM down to the server, they're also the most powerful of the tests.
* `public/` The UI web-app.
* `public/css/` CSS generated by the grunt script.
* `public/fonts/` & `public/images` Assets, some of which are compiled into the CSS by the grunt script, others (for instance those that are too large to compile into the CSS efficiently) are served directly.
* `public/js/` An ungit.js file generated by the grunt script, as well as raven files which handle exception logging.
* `public/less/` Less files, which are the "source" used to generate the CSS.
* `public/source/` Javascript source code, which is turned into the public/js/ungit.js file by the grunt script.
* `public/templates/` HTML source code, compiled into the index.html file by the grunt script.
* `public/vendor/` Various 3rd-party libs.
* `source/` Server and shared (i.e. used by both server and UI) source code.
* `test/` Unit tests and REST interface tests.

Running tests
-------------

`grunt test` will run both unit tests, REST-interface tests, and clicktests. `grunt unittest` only runs the tests in the test/ folder, `grunt clicktest` runs only the tests in the clicktests/ folder. Install mocha (`npm install -g mocha`) to run specific tests in the test folder and get better stack traces: `mocha test/spec.git-api.js`.

Things to consider when developing
----------------------------------

* Try to make everything as touch friendly as possible, for instance no mouse over tooltips (try to make it clear without that). Everything doesn't adhere 100% to that right now but I'm trying to move it more in that direction.
* Write tests. The most important tests to write are usually the clicktests since they will cover the most code (both ui and backend).