# PHP in Go

This is an implementation of PHP, written in pure Go.

## Why?

That's a good question. PHP is a nice language but is having trouble keeping up with modern languages. This implementation, while far from finished, as purpose to allow a few things from within PHP:

* Usage of goroutines, go channels, etc
* Better caching of compiled code
* Use Go's memory management within PHP
* Ability to run functions or code sandboxed (including filesystem)

# Install

In order to run php code as cli:

	go get github.com/MagicalTux/gophp/sapi/php-cli

# Status

This is still a very early implementation and most of the core is missing.

Right now, running PHP's own tests would require pcre, so it is not possible to run the tests yet.

## TODO

* Fix arguments passed by reference → PHP, when a non-existing variable is passed by reference, will set it to NULL in the appropriate context and pass it as a reference.

## Syntax

* Error reporting needs to be done
* Class and object implementation is still very early. Access checks are missing. Class inheritance, etc are missing
* Traits are missing
* Operator precedence is yet to be implemented (see http://php.net/manual/en/language.operators.precedence.php )
* do-while structure
* break/continue needs improvement/fixing
* declare still missing
* include/require missing
* goto missing
* namespaces are missing too
* Exception throwing missing
* generators are missing
* predefined superglobals are missing...

## Extensions

| Extension  | Status | Notes                                          |
|------------|--------|------------------------------------------------|
| standard   |     5% | a lot of work remaining                        |
| ctype      |   100% |                                                |
| pcre       |     5% | might need to use cgo                          |
| gmp        |        | Use math/big ?                                 |
| date       |        |                                                |
| hash       |        |                                                |
| iconv      |        |                                                |
| json       |        | Need custom impl to support php arrays         |
| mbstring   |        |                                                |
| mcrypt     |        |                                                |
| mysqli     |        |                                                |
| openssl    |        | using crypto packages                          |
| Reflection |        |                                                |
| session    |        |                                                |
| tokenizer  |        | already in core/tokenizer, needs to be exposed |
| xml*       |        |                                                |
| gd         |        | without gd                                     |

# Contributing

Right now, code for extensions is the most needed part.

Writing an extension is simple. Create a directory in ext, write code prefixed with a magic function defining comment and run the tools/buildext.php script to generate bindings/etc. Add your newly created extension to the main.go of each sapi to enable it by default.

