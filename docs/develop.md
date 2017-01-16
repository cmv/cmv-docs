# Setting up a development environment

This project uses grunt to automate tasks like minifying css and js as well as js linting and css prefixing.

## To get started setup you dev machine:

1. Install [node](http://nodejs.org).

2. Install the grunt cli (command line interface) globally from the command line with : `npm install -g grunt-cli`, this only needs to be done once per dev machine.

3. Install jshint globally from the command line with : `npm install -g jshint`, this only needs to be done once per dev machine.

## Get the code and install dev dependencies:

1. Fork the repo into your own github account.

2 Clone your fork and in cloned directory:

    - Install the local dev dependencies for the project in the repo from the command line: `npm install`, this only needs to be done once per dev machine.

    - Run grunt from the repo with: `grunt` this will launch a mini dev server and lint your js as you code.

    - Run grunt from the repo with: `grunt build` this will create a `dist` folder with minified code ready for deployment.

    - There are other grunt tasks, use: `grunt -h` to see a list.
