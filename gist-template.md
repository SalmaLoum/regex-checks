# Regex tutorial - Matching a URL

This tutorial explains how regex, or a specific regular expression, functions.
Each part of the expression's functionality will be broken down in details.

## Summary

In this tutorial, we'll break down the below expression for Matching a URL:

```md
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]_)_\/?\$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors:

- ~/~ `^` ~(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]_)_\/?~ `$` ~/~

- In this expression the characters `^` and `$` are both considered to be anchors.

- The `^` character is claimed at start of the string

- The character `$` is claimed at the end of the string.
- ## For example, in this `^xyz$` expression the `^` has to come before the `x` signaling for the beginning of the string and the `$` has to come after the `z` signaling for the end of the string.

### Quantifiers:

- Quantifiers match as many occurrences of particular patterns as possible. They are known as inherently greedy, in this example:

- ~/^(https~ `?` ~:\/\/)~ `?` ~([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]_)_\/~ `?` ~\$/~

- The `?` character is a quantifier that matches zero or one time.

  - The first `?` indicates that `https` matches zero or one times, then to show that `https//` matches zero or one times, and finally at the end indicating that `/` matches zero or one times.
  - For example, `Me?ne?` can match the `Me` in `Mendocino` and the `en` in `enemy`.
  - If a `?` used after another quantifier `(?,+,*, {})`, it switch the quantifier to being non-greedy or **Lazy**, which matches the minimum number of times instead of it's normal state, of matcing the maximum number of times

  ***

- ~/^(https?:\/\/)?([\da-z\.-]~ `+` ~)\.([a-z\.]{2,6})([\/\w \.-]_)_\/?\$/~

- The character `+` is another quantifier that matches zero or one time.

  - It's used once following the pattern `[\da-z\.-]` indicating that the previous token matches between one and many times as possible, giving back as needed.
  - For example, `/Z+/` matches `Z`, `Zoo` , or `Zebra`.

  ***

- ~/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]~`*` ~)~ `*`~\/?\$/~

- The `*` is another quantifier that shows `[\/\w \.-]` may match zero or more times and that `([a-z\.]{2,6})([\/\w \.-]*)` may match zero or more times.

  - It matches the preceding pattern zero or more times.
  - For example: `/sad*/` matches `sad` in `sadly` and `ad` in `advertising`, but has no matches in `pond`.

  ***

- ~/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]~ `{2,6}` ~)([\/\w \.-]_)_\/?\$/~
- The `{2,6}` matches the previous token `[a-z\.]` a minmum of two times and a maximum of six times, giving back as needed. It all depends on how the characters are placed in the `{}`
  - For exmaple:
  - { 5 } - Matches the preceding pattern exactly 5 times.
  - { 5, } - Matches the preceding pattern at least 5 times.
  - { 5, 20 } - Matches the preceding pattern a minimum of 5 times and a maximum of 20 times.
  ***

### Grouping Constructs:

- ~/^~ `(https?:\/\/)` ~?~ `([\da-z\.-]+)` ~\.~ `([a-z\.]{2,6})` `([\/\w \.-]*)` ~\*\/?\$/~

- Grouping constructs are identified by `()`, wrapping subexpressions to seperate strings or sections for different specifications.

- The following grouping constructs are in our url, each of these subexpressions are specific for what they require:

  - `(https?:\/\/)`
  - `([\da-z\.-]+)`
  - `([a-z\.]{2,6})`
  - `([\/\w \.-]*)`
  - Subexpressions usually search for specific matches.
  - For example, `(xyz):(abc)` , `xyz:abc` would match, where `zyx:cba` would not.

  ***

### Bracket Expressions:

- ~/^(https?:\/\/)?(~ `[\da-z\.-]` ~+)\.(~ `[a-z\.]` ~{2,6})(~ `[\/\w \.-]` ~_)_\/?\$/~

- Bracket Expressions are known as the Positive Character Groups, meaning, we can include all characters that we want to match within the brackets, or seperate the first and the last character with hyphen to represent a range of these characters.

  - For example, `[stuvwxyz]` has the same meaning as `[s-z]`, they both represent the same string of `s` or `t` or `u` or `v` or `w` or `x` or `y` or `z`. As long as the string includes one of the characters indicated, it will be considered a match.

- `[\da-z\.-]` - this bracket expression will match any single lowercase character in the range between a and z, before one digit equivalent to `[0-9]`, a slash, a dot, or a hyphen.

- `[a-z\.]` - this bracket expression will match any single lowercase character in the range between a and z, a slash, or a dot.

- `[\/\w \.-]`- this bracket expression will match any slash. The `w` will match any word character equivalent to `[a-zA-Z0-9_]` , a dot, or a hyphen.

  ***

### Character Classes:

- ~/^(https?:\/\/)?([~ `\d` ~a-z\.-]+)\.([a-z\.]{2,6})([\~~ `\w` ~\.-]_)_\/?\$/~

- Character Classes will match any defined sets of characters in a string. One of the most popular types of character classes are Bracket Expressions (mentioned in the above section).

- Some examples of character classes are:

- `/d` - will match any numerical digit

- `/w` - will match alphanumeric character including an underscore (_), `[a-zA-Z0-9_]`

- `/s` - will match a single whitespace character, tabs and line breaks.

- `.` - will match any character except for `/n` for a new line.

- In our URL we see two types of character classes:

- First is the `/d` within`[\da-z\.-]` which will match any numerical digit within this bracket expression.

- Second, is the `/w` within `[\/\w \.-]` which will match any `[a-zA-Z0-9_]` alphanumeric character within this bracket expression.

  ***

### Character Escapes:

~/^(https?:\/\/)?([\da-z~ `\.` ~-]+)~ `\.` ~([a-z~ `\.` ~]{2,6})([~\/ \ w~ `\.` ~-]_)_\/?\$/~

- A backslash `\` indicates a Character escape. They are used to interpret a character but not in it's literal form. However, all epcial charactes including character escapes lose their functionality when included inside bracket expressions.

  - For example, { usually indicates the beginning of a quantifier, but if we precede the curly brace with a backslash (\{), regex will look for an opening curly brace rather than the beginning of a quantifier. This can be useful when looking for strings that include special characters.

- In our matching a URL example, the `\.` used to indicate that we are looking for the character `.` literally , and not a character's class

  ***

## Author

Reach me at the links below with additional questions:

- Salma Loum: https://github.com/SalmaLoum
