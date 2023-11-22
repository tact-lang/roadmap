# The Tact Roadmap

## Introduction

The current version of the roadmap is based on the feedback from Tact/FunC
developers who build their projects using Tact, the feedback from the
participants of the [Tact contest](https://society.ton.org/ton-tact-challenge)
held in October 2023 and, of course, on the
[ROADMAP.md](https://github.com/tact-lang/tact/blob/db595d92c222fd1f8baf78c2355e82df1e3b754a/ROADMAP.md)
by the Tact compiler initial author, Steve Korshakov.

We are open to the feedback from the TON community and invite you to share your
ideas about the future of the Tact smart contract language. Share your
suggestions through the [GitHub
issues](https://github.com/tact-lang/roadmap/issues) in this repository or get
in touch with us in our Telegram [chat group](https://t.me/tactlang).

## Security audit of Tact compiler

We are working closely with established firms in this area to make sure Tact is
secure. As Tact is technically a transpiler into
[FunC](https://docs.ton.org/develop/func/overview), the security of FunC also
needs to be addressed, however, this is a separate concern. We are going to fix
compilation-time arbitrary code execution issue(s) and perform pen-testing to
provide extra guarantees there it won't happen in the future.

## Language improvements

### New types

- Typed tuples support like in FunC.
- `enums`: Many smart contracts implement finite-state machines. It can be more
  expressive to allow developers to encode the `Int` state variable as words
  instead of numbers.
- Arrays (users simulate those with maps at the moment).
- Tact should have more idiomatic ways of handling low level constructs such as
  `Slice` and `Cell`. This requires introducing some more type-level
  constructions.

### Type system improvements

- Local type inference, especially for `let`-expressions.
- Better support for nullable types, for instance, auto-unpacking nullable
  variables to non-null ones.

### Map improvements

- Add map traversals, i.e. the ability to iterate over maps.
- Allow `String` and `coins` as map value type (these are allowed when wrapped
  in a structure anyways).
- Better map key deletion syntax or builtin function.

### New operators and syntactic sugar

- More stateful operators: `+=`, `-=`, `++`, `--` , etc.
- `struct` update syntax.
- More control-flow operators, for instance, `break` with a label.
- Balanced arith operations `(x + d, y - d)` which are useful to ensure token
  amount preservation.

### Error reporting

- Better syntactic error reporting.
- Improve semantic error reporting and make sure error reporting does not leak
  to the level of FunC.

### Contract upgradeability

Contracts and contract families should have an out-of-the-box mechanism for
upgradability.

### Gas optimizations

Our goal is to make Tact contracts consume fewer gas: both for user-written code
and the Tact runtime.

### Misc.

- Doc comments support.
- Improve language consistency: for example, `sender()` vs `context().sender`:
  these two also have different gas usage.
- String and address equality/non-equality operators.
- Improve the way users work with addresses, e.g. `Address` to `String`
  conversion.
- Use of constant strings as the `receive` parameter.
- Numbers: `_` separator for number literals (`1_000_000`), binary number
  literals (`0b1010`).
- Cell-overflow analysis.

## Dev tooling improvements

Overall, we will focus our efforts on the [VS Code
plugin](https://github.com/tact-lang/tact-vscode) as it seems to be one of the
most popular editors, but also as a mid-term effort we are going to
support a standalone
[LSP](https://en.wikipedia.org/wiki/Language_Server_Protocol) server, which
enables many other code editors (Emacs, Vim/NeoVim, Helix, ...) to be pleasant
to work with Tact.

Some more efforts that we will concentrate on are as follows:

- [Tree-sitter](https://tree-sitter.github.io/tree-sitter/) grammar to support
  Vim/Emacs-like editors (short-term) + GitHub repos (long-term) via
  [Linguist](https://github.com/github-linguist/linguist).
- Tact source code formatter. This can actually be done using
  [Topiary](https://topiary.tweag.io), provided we have the Tree-sitter grammar.
- First-class support for Blueprint.
- Support for distribution of Tact libraries and contract traits.

## Documentation

We are planning to put more effort into enhancing the [Tact
documentation](https://docs.tact-lang.org) and encourage the TON community to
contribute to it.

Some ideas and directions for future work:

- Create doc chapters aiming at blockchain newcomers.
- A chapter on Tact idioms.
- Cover anti-patterns and possible attacks on Tact smart-contracts.
- Cover a system of sufficiently large *interacting* realistic contracts.
- Add a troubleshooting page explaining some common infrastructure-related
  errors (like `File not found: tact_Task1.headers.fc`).

If you'd like to work on some things outlined above or have another nice idea on
how to improve the Tact docs, please get in touch using our [Grants and
Bounties](https://github.com/ton-society/grants-and-bounties) program. For
instance, Tact got a very nice [Vim
plugin](https://github.com/tact-lang/tact.vim) through that program. Try out our
[footsteps_helper_bot](https://t.me/footsteps_helper_bot) to create new bounty
proposals.

## Tools to perform security audits of Tact contracts

Unit testing and manual code inspection are good tools but it's easy to miss
something, so we aim at providing some automated tools that help TON devs. We
are going to tap into the state-of-the-art research in static analysis, [model
checking](https://en.wikipedia.org/wiki/Model_checking), [symbolic
execution](https://en.wikipedia.org/wiki/Symbolic_execution) and fuzzing-like
techniques, including [property-based randomized
testing](https://en.wikipedia.org/wiki/Software_testing#Property_testing).

We should mention in this context that one of the most difficult things to
account for is the actor model used in TON, so this is out long-term goal,
rather than a short-term one.

Our first priorities are will be static analyzers, including dead code analysis
and integer overflow detector as well as some simpler tools providing
linter-like experience. Of course, for a smooth dev experience these tools are
going to be integrated with the Tact language server.

We are seeking the ideas from the community on in terms of what you'd like to
have detected in your Tact code.

## Acknowledgments

Tact wouldn't be possible without its original authors, contributors and
supporters:

- [Steve Korshakov](https://github.com/ex3ndr)
- [Oleg Andreev](https://github.com/oleganza)
- [Tal Kol](https://github.com/talkol)
- [Kirill Emelyanenko](https://github.com/EmelyanenkoK)

And also Kirill Malev, Lyubov Shombina, Howard Peng and many others!
