# `module Minilib.Text.RegExp`

Simple regular expression.

Currently it only supports patterns below:
- Character classes: `[xyz]`, `[^xyz]`, `.`, `\d`, `\D`, `\w`, `\W`, `\s`,
  `\S`, `\t`, `\r`, `\n`, `\v`, `\f`, `[\b]`, `x|y`
- Assertions: `^`, `$`
- Groups: `(x)`
- Quantifiers: `x*`, `x+`, `x?`, `x{n}`, `x{n,}`, `x{n,m}`

For details, see
[mdn web docs: Regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions).

LIMITATION:

Currently, only single byte characters (U+0001..U+007F) can be specified in character classes.
Non-ASCII characters (U+0080..U+10FFFF) are encoded to two or more bytes in UTF-8, so they cannot be specified in character classes.
And the null character (U+0000) cannot be used in Fix strings.

# Types and aliases

## `namespace Minilib.Text.RegExp`

### `type RegExp = unbox struct { ...fields... }`

Type of a compiled regular expression.

#### field `flags : Std::String`

#### field `nfa : Minilib.Text.RegExp.RegExpNFA::NFA`

# Traits and aliases

# Trait implementations

# Values

## `namespace Minilib.Text.RegExp::RegExp`

### `@flags : Minilib.Text.RegExp::RegExp -> Std::String`

Retrieves the field `flags` from a value of `RegExp`.

### `@nfa : Minilib.Text.RegExp::RegExp -> Minilib.Text.RegExp.RegExpNFA::NFA`

Retrieves the field `nfa` from a value of `RegExp`.

### `_convert_groups_to_string : Std::Array (Std::I64, Std::I64) -> Std::String -> Std::Array Std::String`

### `act_flags : [f : Std::Functor] (Std::String -> f Std::String) -> Minilib.Text.RegExp::RegExp -> f Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by applying a functorial action to field `flags`.

### `act_nfa : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp::RegExp -> f Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by applying a functorial action to field `nfa`.

### `compile : Std::String -> Std::String -> Std::Result Std::String Minilib.Text.RegExp::RegExp`

`RegExp::compile(pattern, flags)` compiles `pattern` into a regular expression.
`flags` change behavior of regular expression matching.
Currently only global flag (`"g"`) is supported.

### `match : Std::String -> Minilib.Text.RegExp::RegExp -> Std::Result Std::String (Std::Array Std::String)`

`regexp.match(target)` matches `target` against `regexp`.

If the global flag (`"g"`) is not set, it returns an array of the groups of the first match.
Group 0 is a substring that matches the entire regular expression.
Group 1 and beyond are the captured substrings in each group. If not captured, the group will be an empty string.

Example:
```
let regexp = RegExp::compile("[a-z]+([0-9]+)", "").as_ok;
let groups = regexp.match("abc012 def345").as_ok;
// groups == ["abc012", "012"]
```

If the global flag (`"g"`) is set, all matching results will be returned, but captured groups will not be included.

Example:
```
let regexp = RegExp::compile("[a-z]+([0-9]+)", "g").as_ok;
let groups = regexp.match("abc012 def345").as_ok;
// groups == ["abc012", "def345"]
```

If the match against the regular expression fails, an error `"NotMatch"` is reported.

This function is similar to [String.match()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/match)
function of JavaScript.

### `match_all : Std::String -> Minilib.Text.RegExp::RegExp -> Std::Array (Std::Array Std::String)`

`regexp.match_all(target)` matches `target` against `regexp`.
All matching results will be returned including captured groups.

If the match against the regular expression fails, an empty array is returned.

This function is similar to [String.matchAll()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)
function of JavaScript.

### `mod_flags : (Std::String -> Std::String) -> Minilib.Text.RegExp::RegExp -> Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by applying a function to field `flags`.

### `mod_nfa : (Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp::RegExp -> Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by applying a function to field `nfa`.

### `replace_all : Std::String -> Std::String -> Minilib.Text.RegExp::RegExp -> Std::String`

`regexp.replace_all(target, replacement)` matches `target` against `regexp`,
and replace all matching substrings with `replacement`.
If `replacement` contains `$&`, it is substituted with entire matched substring.
If `replacement` contains `$n` where `n` is an integer, it is substituted with
the captured group.
If `replacement` contains `$$`, it is substituted with single `$`.

Example:
```
let regexp = RegExp::compile("(\\w\\w)(\\w)", "").as_ok;
let result = regexp.replace_all("abc def ijk", "$2$1");
// result == "cab fde kij"
```

This function is similar to [String.replaceAll()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/replaceAll)
function of JavaScript.
Note that `$'`, `` $` ``, `$<Name>` are not supported yet.

### `set_flags : Std::String -> Minilib.Text.RegExp::RegExp -> Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by setting field `flags` to a specified one.

### `set_nfa : Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp::RegExp -> Minilib.Text.RegExp::RegExp`

Updates a value of `RegExp` by setting field `nfa` to a specified one.