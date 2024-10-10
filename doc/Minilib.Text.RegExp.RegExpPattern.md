# `module Minilib.Text.RegExp.RegExpPattern`

Character class and Pattern parser. This is internal module of `RegExp`.

# Types and aliases

## `namespace Minilib.Text.RegExp.RegExpPattern`

### `type CharClass = unbox struct { ...fields... }`

Type of a character class.

#### field `label : Std::String`

#### field `f : Std::U8 -> Std::Bool`

### `type PAssertion = unbox union { ...variants... }`

Type of an assertion for regular expressions, such as `^`, `$`.

#### variant `pa_begin : ()`

#### variant `pa_end : ()`

### `type Pattern = box union { ...variants... }`

Type of a parsed regular expression.

#### variant `pclass : Minilib.Text.RegExp.RegExpPattern::CharClass`

#### variant `passert : Minilib.Text.RegExp.RegExpPattern::PAssertion`

#### variant `psequence : Std::Array Minilib.Text.RegExp.RegExpPattern::Pattern`

#### variant `peither : (Minilib.Text.RegExp.RegExpPattern::Pattern, Minilib.Text.RegExp.RegExpPattern::Pattern)`

#### variant `pquant : (Minilib.Text.RegExp.RegExpPattern::Pattern, Std::I64, Std::I64)`

#### variant `pgroup : (Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern)`

# Traits and aliases

# Trait implementations

### `impl Minilib.Text.RegExp.RegExpPattern::CharClass : Std::ToString`

Converts a character class to a string.

### `impl Minilib.Text.RegExp.RegExpPattern::PAssertion : Std::ToString`

Converts an assertion to a string.

### `impl Minilib.Text.RegExp.RegExpPattern::Pattern : Std::ToString`

Converts a pattern to a string.

# Values

## `namespace Minilib.Text.RegExp.RegExpPattern::CharClass`

### `@f : Minilib.Text.RegExp.RegExpPattern::CharClass -> Std::U8 -> Std::Bool`

Retrieves the field `f` from a value of `CharClass`.

### `@label : Minilib.Text.RegExp.RegExpPattern::CharClass -> Std::String`

Retrieves the field `label` from a value of `CharClass`.

### `act_f : [f : Std::Functor] ((Std::U8 -> Std::Bool) -> f (Std::U8 -> Std::Bool)) -> Minilib.Text.RegExp.RegExpPattern::CharClass -> f Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by applying a functorial action to field `f`.

### `act_label : [f : Std::Functor] (Std::String -> f Std::String) -> Minilib.Text.RegExp.RegExpPattern::CharClass -> f Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by applying a functorial action to field `label`.

### `add : Std::U8 -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Adds a character to the character class.

### `cls_digit : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\d`. (digits)

### `cls_dot : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `.`. (any character except newlines)

### `cls_non_digit : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\D`. (non-digits)

### `cls_non_whitespace : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\S`. (non-whitespaces)

### `cls_non_word_char : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\W`. (ie. `[^A-Za-z0-9_]`)

### `cls_whitespace : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\s`. (whitespaces)

### `cls_word_char : Minilib.Text.RegExp.RegExpPattern::CharClass`

A character class of `\w`. (ie. `[A-Za-z0-9_]`)

### `consists_of : Std::String -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Creates a character class whose members are characters in the specified string.

### `contains : Std::U8 -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Std::Bool`

Returns true if the character is a member of the class.

### `empty : Minilib.Text.RegExp.RegExpPattern::CharClass`

An empty character class.

### `make : Std::String -> (Std::U8 -> Std::Bool) -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Creates a character class from a label and a member function.

### `mod_f : ((Std::U8 -> Std::Bool) -> Std::U8 -> Std::Bool) -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by applying a function to field `f`.

### `mod_label : (Std::String -> Std::String) -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by applying a function to field `label`.

### `negate : Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Negate the member function of a character class.

### `range : Std::U8 -> Std::U8 -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Creates a character class whose members are characters from start to end.

### `set_f : (Std::U8 -> Std::Bool) -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by setting field `f` to a specified one.

### `set_label : Std::String -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Updates a value of `CharClass` by setting field `label` to a specified one.

### `singleton : Std::U8 -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Creates a character class whose only member is the specified character.

### `to_table : Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

For optimization, creates a lookup table of same members, and returns a character class
using that table.

### `union : Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Creates union of two character classes.

## `namespace Minilib.Text.RegExp.RegExpPattern::PAssertion`

### `as_pa_begin : Minilib.Text.RegExp.RegExpPattern::PAssertion -> ()`

Unwraps a union value of `PAssertion` as the variant `pa_begin`.
If the value is not the variant `pa_begin`, this function aborts the program.

### `as_pa_end : Minilib.Text.RegExp.RegExpPattern::PAssertion -> ()`

Unwraps a union value of `PAssertion` as the variant `pa_end`.
If the value is not the variant `pa_end`, this function aborts the program.

### `is_pa_begin : Minilib.Text.RegExp.RegExpPattern::PAssertion -> Std::Bool`

Checks if a union value of `PAssertion` is the variant `pa_begin`.

### `is_pa_end : Minilib.Text.RegExp.RegExpPattern::PAssertion -> Std::Bool`

Checks if a union value of `PAssertion` is the variant `pa_end`.

### `mod_pa_begin : (() -> ()) -> Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Updates a value of union `PAssertion` by applying a function if it is the variant `pa_begin`, or doing nothing otherwise.

### `mod_pa_end : (() -> ()) -> Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Updates a value of union `PAssertion` by applying a function if it is the variant `pa_end`, or doing nothing otherwise.

### `pa_begin : () -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Constructs a value of union `PAssertion` taking the variant `pa_begin`.

### `pa_end : () -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Constructs a value of union `PAssertion` taking the variant `pa_end`.

## `namespace Minilib.Text.RegExp.RegExpPattern::Pattern`

### `_assign_group_number : Std::I64 -> Minilib.Text.RegExp.RegExpPattern::Pattern -> (Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern)`

`pat._assign_group_number(n)` assigns group number for each group.
The first group number becomes `n`.
It returns the translated pattern along with group count.

### `_normal_chars : Minilib.Text.RegExp.RegExpPattern::CharClass`

A table of normal characters, ie. not a meta character.

### `_parse_backslash_char_class : Std::Bool -> Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::CharClass`

Parses the char class that begins with a backslash.
The backslash itself is parsed already.

### `_parse_bracket_component : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::CharClass`

Parses each component in a bracket.

### `_parse_passert : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses an assertion pattern, ie. `^`, `$` etc.

### `_parse_pclass : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses character class pattern, ie. `.`, `[a-z]`, `\w` etc.

### `_parse_pclass_bracket : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::CharClass`

Parses a character class that begins with '['.
The `[` itself is parsed already.

### `_parse_peither : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses either-pattern, ie. `X|Y`

### `_parse_pgroup : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses Group Pattern, ie. `(X)`

### `_parse_pquant : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses Quantified Pattern, ie. `X?`, `X*`, `X+`, `X{n}`, `X{n,}`, `X{n,m}`

### `_parse_pquant_n_m_inner : Minilib.Text.SimpleParser::Parser (Std::I64, Std::I64)`

Parses inner of `X{n}`, `X{n,}`, `X{n,m}`

### `_parse_psequence : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses sequence of patterns, ie. `XYZ`

### `_parse_quantifiable_item : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses quantifiable item.

### `as_passert : Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Unwraps a union value of `Pattern` as the variant `passert`.
If the value is not the variant `passert`, this function aborts the program.

### `as_pclass : Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Unwraps a union value of `Pattern` as the variant `pclass`.
If the value is not the variant `pclass`, this function aborts the program.

### `as_peither : Minilib.Text.RegExp.RegExpPattern::Pattern -> (Minilib.Text.RegExp.RegExpPattern::Pattern, Minilib.Text.RegExp.RegExpPattern::Pattern)`

Unwraps a union value of `Pattern` as the variant `peither`.
If the value is not the variant `peither`, this function aborts the program.

### `as_pgroup : Minilib.Text.RegExp.RegExpPattern::Pattern -> (Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern)`

Unwraps a union value of `Pattern` as the variant `pgroup`.
If the value is not the variant `pgroup`, this function aborts the program.

### `as_pquant : Minilib.Text.RegExp.RegExpPattern::Pattern -> (Minilib.Text.RegExp.RegExpPattern::Pattern, Std::I64, Std::I64)`

Unwraps a union value of `Pattern` as the variant `pquant`.
If the value is not the variant `pquant`, this function aborts the program.

### `as_psequence : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Array Minilib.Text.RegExp.RegExpPattern::Pattern`

Unwraps a union value of `Pattern` as the variant `psequence`.
If the value is not the variant `psequence`, this function aborts the program.

### `is_passert : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `passert`.

### `is_pclass : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `pclass`.

### `is_peither : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `peither`.

### `is_pgroup : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `pgroup`.

### `is_pquant : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `pquant`.

### `is_psequence : Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Bool`

Checks if a union value of `Pattern` is the variant `psequence`.

### `mod_passert : (Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpPattern::PAssertion) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `passert`, or doing nothing otherwise.

### `mod_pclass : (Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `pclass`, or doing nothing otherwise.

### `mod_peither : ((Minilib.Text.RegExp.RegExpPattern::Pattern, Minilib.Text.RegExp.RegExpPattern::Pattern) -> (Minilib.Text.RegExp.RegExpPattern::Pattern, Minilib.Text.RegExp.RegExpPattern::Pattern)) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `peither`, or doing nothing otherwise.

### `mod_pgroup : ((Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern) -> (Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern)) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `pgroup`, or doing nothing otherwise.

### `mod_pquant : ((Minilib.Text.RegExp.RegExpPattern::Pattern, Std::I64, Std::I64) -> (Minilib.Text.RegExp.RegExpPattern::Pattern, Std::I64, Std::I64)) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `pquant`, or doing nothing otherwise.

### `mod_psequence : (Std::Array Minilib.Text.RegExp.RegExpPattern::Pattern -> Std::Array Minilib.Text.RegExp.RegExpPattern::Pattern) -> Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Updates a value of union `Pattern` by applying a function if it is the variant `psequence`, or doing nothing otherwise.

### `parse : Std::String -> Std::Result Std::String Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses a pattern from specified string.

### `parse_pattern : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpPattern::Pattern`

Parses a pattern from the stream.

### `passert : Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `passert`.

### `pclass : Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `pclass`.

### `peither : (Minilib.Text.RegExp.RegExpPattern::Pattern, Minilib.Text.RegExp.RegExpPattern::Pattern) -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `peither`.

### `pgroup : (Std::I64, Minilib.Text.RegExp.RegExpPattern::Pattern) -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `pgroup`.

### `pquant : (Minilib.Text.RegExp.RegExpPattern::Pattern, Std::I64, Std::I64) -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `pquant`.

### `psequence : Std::Array Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpPattern::Pattern`

Constructs a value of union `Pattern` taking the variant `psequence`.