# Pulsar IDE — ccls

This package integrates the [ccls](https://github.com/MaskRay/ccls) C and C++ language server with [Pulsar](https://pulsar-edit.dev/).

It is a Pulsar-oriented fork of [atom-ide-ccls](https://github.com/isundaylee/atom-ide-ccls) and uses the maintained [`@savetheclocktower/atom-languageclient`](https://github.com/savetheclocktower/atom-languageclient).

## Installation

### 1. Install ccls

Install or build [ccls](https://github.com/MaskRay/ccls) for your operating system.

Verify that it is available:

```sh
ccls --version
```

If `ccls` is not available through `PATH`, open this package’s settings in Pulsar and set **ccls executable path** to the full path of the executable.

### 2. Install this package

Until the package is published in the Pulsar Package Registry, install it directly from GitHub:

```sh
pulsar -p install GrishaKirilin/pulsar-ide-ccls
```

The equivalent command using `ppm` is:

```sh
ppm install GrishaKirilin/pulsar-ide-ccls
```

Do not enable this package and the original `ide-ccls` package simultaneously.

### 3. Install UI packages

Install the Atom IDE UI packages used to present language-server features:

```sh
ppm install \
  atom-ide-base \
  atom-ide-datatip \
  atom-ide-definitions \
  atom-ide-hyperclick \
  atom-ide-outline \
  atom-ide-signature-help \
  busy-signal \
  intentions \
  linter \
  linter-ui-default
```

## Project-root discovery

Unlike the original `ide-ccls` package, this package searches upward from each opened C or C++ file for the nearest `.ccls` file.

For example:

```text
large-project/
├── .ccls
├── compile_commands.json
├── library-a/
│   └── source.cpp
└── library-b/
    └── source.cpp
```

You may add only `library-a` and `library-b` to a Pulsar window. When either `source.cpp` is opened, the package discovers `large-project/.ccls` and uses `large-project` as the language-server root.

Files that resolve to the same `.ccls` file share the same ccls server and index.

If no `.ccls` file is found, the package falls back to Pulsar’s normal project-root selection.

## Features

### Diagnostics and autocompletion

The package reports ccls diagnostics and provides context-sensitive completion suggestions as you type.

![Diagnostics and autocompletion](https://raw.githubusercontent.com/GrishaKirilin/pulsar-ide-ccls/master/images/autocomplete-diagnostic.gif)

### Go to declaration or definition

With a compatible definitions or Hyperclick UI package installed, use:

* `Command+Click` on macOS;
* `Control+Click` on Linux and Windows.

![Go to declaration or definition](https://raw.githubusercontent.com/GrishaKirilin/pulsar-ide-ccls/master/images/goto.gif)

### Hover and signature information

With a compatible hover or datatip package installed, hovering over variables and functions displays their types, signatures, and related documentation.

![Type and signature information](https://raw.githubusercontent.com/GrishaKirilin/pulsar-ide-ccls/master/images/signature-help.gif)

### Additional features

Depending on the installed UI packages and the capabilities advertised by ccls, the integration can provide:

* document outlines;
* find references;
* range formatting;
* background-indexing progress;
* semantic highlighting.

Semantic highlighting is disabled by default. Enable it in the package settings.

## Development

Clone the repository and install its dependencies:

```sh
git clone https://github.com/GrishaKirilin/pulsar-ide-ccls.git
cd pulsar-ide-ccls
npm install
```

Link the package into Pulsar’s development environment:

```sh
pulsar -p link --dev
```

Start a development-mode Pulsar window:

```sh
pulsar --dev
```

Disable the normally installed copy of `ide-ccls` or `pulsar-ide-ccls` in the development window so that only the linked development package is active.

## Origin

This project is based on [isundaylee/atom-ide-ccls](https://github.com/isundaylee/atom-ide-ccls).

The Pulsar port replaces the obsolete Atom language-client dependency and adds upward `.ccls` project-root discovery.

## License

[MIT](LICENSE)
