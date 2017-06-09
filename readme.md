# lightscript-cli &middot; [![Version](https://img.shields.io/npm/v/lighscript-cli.svg?style=flat-square&maxAge=3600)](https://www.npmjs.com/package/lightscript-cli) [![License](https://img.shields.io/npm/l/lightscript-cli.svg?style=flat-square&maxAge=3600)](https://www.npmjs.com/package/lightscript-cli) [![LightScript](https://img.shields.io/badge/written%20in-lightscript-00a99d.svg)](http://www.lightscript.org)

> command line utility for working with LightScript code & packages

_note: this project is a work in progress and, while usable, is
not considered entirely stable_

## installation

```console
$ npm i -g lightscript-cli
```

The `lightscript` command is then available from anywhere, as well as
the shorter form `lsc`.

## usage

### compile

> compile LightScript source files to JavaScript.

```console
# compile an input file to an output file
$ lsc compile file.lsc -f file.js

# compile a directory of files to an output directory
$ lsc compile src -d dist

# use additional Babel presets or plugins
$ lsc compile src -d dist --presets react --plugins partial-application

# do not use existing .babelrc file
$ lsc compile src -d dist --no-babelrc

# do not apply `babel-preset-env`
$ lsc compile src -d dist --no-env-preset

# look up a configuration file (ie. `lightscript.config.lsc`)
$ lsc compile -c

# specify a path to a configuration file
$ lsc compile -c build/lightscript.config.lsc
```

> **Aliases**: `c`

Note that, by default, `lightscript-cli` will use Babel's usual
`.babelrc` lookup behavior, and merge this with its internally
provided configuration. This means that if there is a `.babelrc`
file present, those presets & plugins will be added after the
relevant `lightscript` plugins. You can use the
`--no-babelrc` flag to disable this.

`babel-preset-env` is also applied by default, but can be disabled
using the `--no-env-preset` flag.

### eval

> run LightScript code or files containing LightScript code (similar to `node -e <code | file>`)

```console
# evaluate the given code and output the result
$ lsc eval "f = (x, y) -> x + y; f(1, 2)"

# run the given file and output the result
$ lsc eval build.js

# same as above, using the `run` alias
$ lsc run build.js
```

> **Aliases**: `run`, `e`

### init

> kickstart a LightScript package

This command currently has no function - input is needed as to how it
should work and what it should do under various circumstances.

See [this issue](https://github.com/citycide/lightscript-cli/issues/1) to
join the discussion.

### repl

> start an interactive REPL for evaluating LightScript code (similar to the `node` command)

```console
$ lsc repl

> fn = (x, y) -> x + y
'use strict'
> fn(1, 2)
3
```

> **Aliases**: `r`

## configuration file

Similar to webpack, you can create a config file for a more clear,
reusable, & dynamic way to apply options. When passed the
`--config` / `-c` flag without a parameter, `lightscript-cli` will
search for a config file within the current working directory in
the following order:

1. `lightscript.config.lsc`
2. `lightscript.config.js`
3. `lightscript.config.json`

Obviously, `lightscript.config.lsc` allows you to use LightScript
syntax to define your configuration. For example:

```coffeescript
comments = process.env.NODE_ENV == 'development'

export default {
  inputs: ['src/**/*', '!src/*.spec.lsc']
  directory: ['dist']

  envPreset: false

  babel: {
    babelrc: false
    comments
    plugins
  }
}
```

The above configuration allows you to run only `lsc compile -c`. The CLI
would locate this file and compile the `inputs` into `directory` while
not using `babel-preset-env` or any existing `.babelrc`.

It also shows a tiny example of dynamic configuration by deciding
whether or not to output comments based on environment.

You can also specify a config file by passing a parameter with the flag:

```console
$ lsc compile -c build/compile-config.lsc
```

## see also

- [LightScript](http://www.lightscript.org) - the compile-to-JS language this tool is written in and for, leveraging [Babel](https://babeljs.io)

## development

```console
git clone https://github.com/citycide/lightscript-cli.git
cd lightscript-cli
npm run build
npm link
```

This will make your local development copy available globally.

## contributing

Pull requests and any [issues](https://github.com/citycide/lightscript-cli/issues)
found are always welcome.

1. Fork the project, and preferably create a branch named something like `feat-make-better`
2. Modify as needed, where `src` contains the LightScript source of the project
3. Make sure all tests continue to pass, and it never hurts to have more tests
4. Push & pull request! :tada:

## license

MIT © [Bo Lingen / citycide](https://github.com/citycide)
