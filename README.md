# gotty-client
:wrench: Terminal client for [GoTTY](https://github.com/yudai/gotty).

![](https://raw.githubusercontent.com/moul/gotty-client/master/resources/gotty-client.png)

[![Build Status](https://travis-ci.org/moul/gotty-client.svg?branch=master)](https://travis-ci.org/moul/gotty-client)
[![GoDoc](https://godoc.org/github.com/moul/gotty-client?status.svg)](https://godoc.org/github.com/moul/gotty-client)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmoul%2Fgotty-client.svg?type=shield)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmoul%2Fgotty-client?ref=badge_shield)
[![Sourcegraph](https://sourcegraph.com/github.com/moul/gotty-client/-/badge.svg)](https://sourcegraph.com/github.com/moul/gotty-client?badge)

```ruby
                                                             ┌─────────────────┐
                                                     ┌──────▶│    /bin/bash    │
                                                     │       └─────────────────┘
                ┌──────────────┐               ┌──────────┐
                │              │               │  Gotty   │
┌───────┐   ┌──▶│   Browser    │───────┐       │          │
│       │   │   │              │       │       │          │
│       │   │   └──────────────┘       │       │          │  ┌─────────────────┐
│  Bob  │───┤                      websockets─▶│          │─▶│ emacs /var/www  │
│       │   │   ╔═ ══ ══ ══ ══ ╗       │       │          │  └─────────────────┘
│       │   │   ║              ║       │       │          │
└───────┘   └──▶║ gotty-client  ───────┘       │          │
                               ║               │          │
                ╚═ ══ ══ ══ ══ ╝               └──────────┘
                                                     │       ┌─────────────────┐
                                                     └──────▶│   tmux attach   │
                                                             └─────────────────┘
```

## Example

Server side ([GoTTY](https://github.com/yudai/gotty))

```console
$ gotty -p 9191 sh -c 'while true; do date; sleep 1; done'
2015/08/24 18:54:31 Server is starting with command: sh -c while true; do date; sleep 1; done
2015/08/24 18:54:31 URL: http://[::1]:9191/
2015/08/24 18:54:34 GET /ws
2015/08/24 18:54:34 New client connected: 127.0.0.1:61811
2015/08/24 18:54:34 Command is running for client 127.0.0.1:61811 with PID 64834
2015/08/24 18:54:39 Command exited for: 127.0.0.1:61811
2015/08/24 18:54:39 Connection closed: 127.0.0.1:61811
...
```

**Client side**

```console
$ gotty-client http://localhost:9191/
INFO[0000] New title: GoTTY - sh -c while true; do date; sleep 1; done (jean-michel-van-damme.local)
WARN[0000] Unhandled protocol message: json pref: 2{}
Mon Aug 24 18:54:34 CEST 2015
Mon Aug 24 18:54:35 CEST 2015
Mon Aug 24 18:54:36 CEST 2015
Mon Aug 24 18:54:37 CEST 2015
Mon Aug 24 18:54:38 CEST 2015
^C
```

## Usage

```console
$ gotty-client -h
NAME:
   gotty-client - GoTTY client for your terminal

USAGE:
   gotty-client [global options] command [command options] GOTTY_URL

AUTHOR:
   Manfred Touron <https://github.com/moul/gotty-client>

COMMANDS:
     help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --debug, -D                  Enable debug mode [$GOTTY_CLIENT_DEBUG]
   --skip-tls-verify            Skip TLS verify [$SKIP_TLS_VERIFY]
   --use-proxy-from-env         Use Proxy from environment [$USE_PROXY_FROM_ENV]
   --detach-keys value          Key sequence for detaching gotty-client (default: "ctrl-p,ctrl-q")
   --v2                         For Gotty 2.0 [$GOTTY_CLIENT_GOTTY2]
   --ws-origin value, -w value  WebSocket Origin URL [$GOTTY_CLIENT_WS_ORIGIN]
   --help, -h                   show help
   --version, -v                print the version
```

## Install

Install latest version using Golang (recommended)

```console
$ go get github.com/moul/gotty-client/cmd/gotty-client
```

---

Install latest version using Homebrew (Mac OS X)

```console
$ brew install https://raw.githubusercontent.com/moul/gotty-client/master/contrib/homebrew/gotty-client.rb --HEAD
```

or the latest released version

```console
$ brew install https://raw.githubusercontent.com/moul/gotty-client/master/contrib/homebrew/gotty-client.rb
```

## Changelog

### master (unreleased)

* Fix TTY restoring by switching to [`github.com/moby/moby/pkg/term`](https://github.com/moby/moby/tree/master/pkg/term) ([#59](https://github.com/moul/gotty-client/pull/59) + ([#60](https://github.com/moul/gotty-client/pull/60) + ([#62](https://github.com/moul/gotty-client/pull/62) ([@Sh4d1](https://github.com/Sh4d1))

[full commits list](https://github.com/moul/gotty-client/compare/v1.7.0...master)

### [v1.7.0](https://github.com/moul/gotty-client/releases/tag/v1.7.0) (2018-04-11)

* Add `--detach-keys` option ([#52](https://github.com/moul/gotty-client/issues/52))
* Cross build on Solaris ([#55](https://github.com/moul/gotty-client/pull/55) ([@dimtion](https://github.com/dimtion))
* Fix terminal resizing issue ([#56](https://github.com/moul/gotty-client/pull/56) ([@byung2](https://github.com/byung2))
* Support for gotty v2.0 ([#58](https://github.com/moul/gotty-client/pull/58) ([@byung2](https://github.com/byung2))
* Support ws-origin (CORS) ([#58](https://github.com/moul/gotty-client/pull/58) ([@byung2](https://github.com/byung2))

[full commits list](https://github.com/moul/gotty-client/compare/v1.6.1...v1.7.0)

### [v1.6.1](https://github.com/moul/gotty-client/releases/tag/v1.6.1) (2017-01-19)

* Do not exit on EOF ([#45](https://github.com/moul/gotty-client/pull/45)) ([@gurjeet](https://github.com/gurjeet))

[full commits list](https://github.com/moul/gotty-client/compare/v1.6.0...v1.6.1)

### [v1.6.0](https://github.com/moul/gotty-client/releases/tag/v1.6.0) (2016-05-23)

* Support of `--use-proxy-from-env` (Add Proxy support) ([#36](https://github.com/moul/gotty-client/pull/36)) ([@byung2](https://github.com/byung2))
* Add debug mode ([#18](https://github.com/moul/gotty-client/issues/18))
* Fix argument passing ([#16](https://github.com/moul/gotty-client/issues/16))
* Remove warnings + golang fixes and refactoring ([@QuentinPerez](https://github.com/QuentinPerez))

[full commits list](https://github.com/moul/gotty-client/compare/v1.5.0...v1.6.0)

### [v1.5.0](https://github.com/moul/gotty-client/releases/tag/v1.5.0) (2016-02-18)

* Add autocomplete support ([#19](https://github.com/moul/gotty-client/issues/19))
* Switch from `Party` to `Godep`
* Fix terminal data being interpreted as format string ([#34](https://github.com/moul/gotty-client/pull/34)) ([@mickael9](https://github.com/mickael9))

[full commits list](https://github.com/moul/gotty-client/compare/v1.4.0...v1.5.0)

### [v1.4.0](https://github.com/moul/gotty-client/releases/tag/v1.4.0) (2015-12-09)

* Remove solaris,plan9,nacl for `.goxc.json`
* Add an error if the go version is lower than 1.5
* Flexible parsing of the input URL
* Add tests
* Support of `--skip-tls-verify`

[full commits list](https://github.com/moul/gotty-client/compare/v1.3.0...v1.4.0)

### [v1.3.0](https://github.com/moul/gotty-client/releases/tag/v1.3.0) (2015-10-27)

* Fix `connected` state when using `Connect()` + `Loop()` methods
* Add `ExitLoop` which allow to exit from `Loop` function

[full commits list](https://github.com/moul/gotty-client/compare/v1.2.0...v1.3.0)

### [v1.2.0](https://github.com/moul/gotty-client/releases/tag/v1.2.0) (2015-10-23)

* Removed an annoying warning when exiting connection ([#22](https://github.com/moul/gotty-client/issues/22)) ([@QuentinPerez](https://github.com/QuentinPerez))
* Add the ability to configure alternative stdout ([#21](https://github.com/moul/gotty-client/issues/21)) ([@QuentinPerez](https://github.com/QuentinPerez))
* Refactored the goroutine system with select, improve speed and stability ([@QuentinPerez](https://github.com/QuentinPerez))
* Add debug mode (`--debug`/`-D`) ([#18](https://github.com/moul/gotty-client/issues/18))
* Improve error message when connecting by checking HTTP status code
* Fix arguments passing ([#16](https://github.com/moul/gotty-client/issues/16))
* Dropped support for golang<1.5
* Small fixes

[full commits list](https://github.com/moul/gotty-client/compare/v1.1.0...v1.2.0)

### [v1.1.0](https://github.com/moul/gotty-client/releases/tag/v1.1.0) (2015-10-10)

* Handling arguments + using mutexes (thanks to [@QuentinPerez](https://github.com/QuentinPerez))
* Add logo ([#9](https://github.com/moul/gotty-client/issues/9))
* Using codegansta/cli for CLI parsing ([#3](https://github.com/moul/gotty-client/issues/3))
* Fix panic when running on older GoTTY server ([#13](https://github.com/moul/gotty-client/issues/13))
* Add 'homebrew support' ([#1](https://github.com/moul/gotty-client/issues/1))
* Add Changelog ([#5](https://github.com/moul/gotty-client/issues/5))
* Add GOXC configuration to build binaries for multiple architectures ([#2](https://github.com/moul/gotty-client/issues/2))

[full commits list](https://github.com/moul/gotty-client/compare/v1.0.1...v1.1.0)

### [v1.0.1](https://github.com/moul/gotty-client/releases/tag/v1.0.1) (2015-09-27)

* Using party to manage dependencies

[full commits list](https://github.com/moul/gotty-client/compare/v1.0.0...v1.0.1)

### [v1.0.0](https://github.com/moul/gotty-client/releases/tag/v1.0.0) (2015-09-27)

Compatible with [GoTTY](https://github.com/yudai/gotty) version: [v0.0.10](https://github.com/yudai/gotty/releases/tag/v0.0.10)

#### Features

* Support **basic-auth**
* Support **terminal-(re)size**
* Support **write**
* Support **title**
* Support **custom URI**

[full commits list](https://github.com/moul/gotty-client/compare/cf0c1146c7ce20fe0bd65764c13253bc575cd43a...v1.0.0)

## License

MIT


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmoul%2Fgotty-client.svg?type=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmoul%2Fgotty-client?ref=badge_large)
