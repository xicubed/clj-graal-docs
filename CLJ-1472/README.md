# CLJ-1472

Clojure 1.10 introduced locking code into clojure.spec.alpha that often causes
GraalVM's `native-image` to fail. The reason for this is that the bytecode
emitted by the locking macro fails bytecode verification. The relevant issue on
the Clojure JIRA for this is
[CLJ-1472](https://clojure.atlassian.net/browse/CLJ-1472).

## TODO

* [incorporate @borkdude's gist](https://gist.github.com/borkdude/dd0857cf1958b25496fddbdbf359ca59) which
is the basis for the script herein

## Scripts

### build-clojure-with-1472-patch.sh

Clojure 1.10 introduced locking code into clojure.spec.alpha that often causes
GraalVM's `native-image` to fail.

[Clojure issue CLJ-1472](https://clojure.atlassian.net/browse/CLJ-1472) includes
potential fixes for this issue.

This script builds and locally installs:

* `org.clojure/clojure` `1.10.1-patch1472`
* `org.clojure/spec.alpha` `0.2.176-patch1472`

The patched version of clojure should work with graal's `native-image`, reference
it via, for example from deps.edn, via:
```
{org.clojure/clojure {:mvn/version "1.10.1-patch1472"}}
```

Prerequisites (installed via brew on macOS)

* clojure
* git
* git-extras
* maven

Tested on macOS Catalina.
