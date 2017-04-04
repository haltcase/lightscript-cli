# lightscript-cli &middot; [![LightScript](https://img.shields.io/badge/written%20in-lightscript-00a99d.svg)](http://www.lightscript.org)

> CLI utility for creating & managing LightScript packages.

_note: this project is a currently not the official lightscript-cli,
stands more as a prototype than as the final solution, and is incomplete._

## installation

Currently you'll need to:

```console
git clone https://github.com/citycide/lightscript-cli.git
cd lightscript-cli
npm run build
npm link
```

The `lightscript` command is then available from anywhere, as well as
the shorter form `lsc`.

Eventually any offically recommended LightScript CLI would be available on NPM.

## usage

```console
# compile the entire `src` directory into `dist`
lightscript src -d dist

# add custom plugins
lightscript src -d dist --plugins lodash
```

## see also

- [LightScript](http://www.lightscript.org) - the compile-to-JS language this tool is written in and for, leveraging [Babel](https://babeljs.io)

## contributing

Pull requests and any [issues](https://github.com/citycide/lightscript-cli/issues)
found are always welcome.

1. Fork the project, and preferably create a branch named something like `feat-make-better`
2. Modify as needed, where `src` contains the LightScript source of the project
3. Make sure all tests continue to pass, and it never hurts to have more tests
4. Push & pull request! :tada:

## license

MIT © [Bo Lingen / citycide](https://github.com/citycide)
