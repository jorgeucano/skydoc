---
layout: default
stylesheet: docs
title: FAQ
---

## Why am I getting `TypeError: unsupported operand type(s) for +: 'dict' and 'dict'`?

Skylark currently defines the `+` operator for dictionaries. Because
Skydoc evaluates `.bzl` files as Python code and because the `+` operator
for dictionaries may be [removed][dict-op] from Skylark in the future, we
suggest using the `dict(a.items() + b.items())` syntax instead.

[dict-op]: https://github.com/bazelbuild/bazel/issues/1086

## Is Skydoc used to generate the documentation on [bazel.build](https://bazel.build)?

Not for now. The [Build Encyclopedia](https://bazel.build/docs/be/overview.html)
documents the set of native Bazel build rules written in Java, and the
[Skylark Library](https://bazel.build/docs/skylark/lib/globals.html) documents the
built-in Skylark modules and functions. Because both of these sets of docs are
generated from Bazel's Java source code, they are generated using a [separate
documentation generation
tool](https://github.com/bazelbuild/bazel/tree/master/src/main/java/com/google/devtools/build/docgen).

We are planning to create a catalog of Skylark rule sets to make it easy to
publish and discover Skylark rule sets and browse their documentation. See
[bazelbuild/bazel#1046](https://github.com/bazelbuild/bazel/issues/1046) for
more information.

## Why do the docstrings for rules come after the rule definition?

Unlike in other languages, [Python docstrings
](https://www.python.org/dev/peps/pep-0257/) are special string literals rather
than comments. Because Skylark is a subset of Python, we take the same approach
for Skylark docstrings as well. Because rule declarations are basically global
variables, we follow the same convention for variable docstrings used by Python
documentation generation tools, such as
[epydoc](http://epydoc.sourceforge.net/manual-docstring.html).
