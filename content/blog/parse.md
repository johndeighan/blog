+++
title = "Parser design"
date = "2024-02-16T12:03:31-05:00"
tags = []
+++

I want to implement a simple parser object with the
following characteristics:

1. Each rule name looks like `<expr>`, i.e. delimited by
	`<` and `>`, with the inside being an identifier.

2. Rules look like:
	```text
	<expr>
		part1
			code
		part2
			code
		...etc.
	```
	That is, the syntax is indentation style, using TAB
	characters by default.

3. Each **part** can be either 1) a literal string, quoted
	as in a JavaScript string, 2) a regular expression or
	3) a rule name. Empty parts are allowed and ignored.

4. Regular expressions are **extended** regular expressions,
	meaning that whitespace in the regexp is NOT significant
	so to match a space, TAB or newline, you have to include
	it explicitly, e.g. as `\x20`.

5. Comments and empty lines are allowed anywhere; a comment
	starts with a '#' character and extends to the end of
	the line.

6. **code** is initially CoffeeScript code implementing
	semantic actions. Eventually, I want the code to be
	CieloScript code, which is an extension of CoffeeScript.

7. The code following a regular expression part has available
	the array of matches from the regular expression. The code
	following a rule has access to whatever was returned by
	the rule when it matches.

Here is a more extensive example, though I haven't decided
completely on the syntax:

```text
<expr>
	<number>
	"+"
	<number>
		return $1 + $2
<expr>
	<identifier>
	"("
	<expr>
	( , <expr> )*
	")"
		return $1($3, $4...);
```
