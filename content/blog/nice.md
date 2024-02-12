+++
title = "NICE format"
date = "2024-02-12T08:09:08-05:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = []
+++

I needed a way to print an arbitrary JavaScript value to the console
with the requirement that the output makes it absolutely clear what
that value is, whether it's a simple value like a string or number, or
a complex value like a hash, array or Javscript object. Furthermore,
in a string, it must be absolutely clear where, and how many, spaces,
TAB characters or newline characters are in the string. So, I came up
with a format that I call **NICE** format. No, it's not an acronym.
Here are some examples of its output:

```coffee
import {toNICE} from '@jdeighan/base-utils/nice'

str = "a string"
console.log toNICE(str)
```
It prefers to use single quotes around a string
```text
'a˳string'
```

Notice how space characters are displayed as '˳', a unicode character.
From here on, I'm going to omit the import statement

```coffee
str = "mary's lamb"
console.log toNICE(str)
```
But it will use double quotes if the string contains a single quote
```text
"mary's lamb"
```
A more complex example:
```coffee
str = "mary's \"stuff\""
console.log toNICE(str)
```
If the string contains both single and double quotes, it will
revert to using unicode quote characters
```text
«mary\'s˳"stuff"»
```

To handle things like arrays and hashes, it uses a format similar
to YAML, but using TAB characters by default for indentation:

```coffee
obj = ['a', 42, undefined]
console.log toNICE(obj)
```
results in:
```text
- 'a'
- 42
- undef
```
For a hash (aka **JavaScript object**):
```coffee
func2 = (x) => console.log "arg is x"    # define a named function
obj = {a:1, b:'abc', f: func2}
```
results in:
```text
a: 1
b: 'abc'
f: [Function func2]
```

Now, a much more complex example:

```coffee
obj = {
	key: 'wood'
	value: [
		"a word"
		{a:1, b:2}
		undef,
		[1,2,"mary's lamb","mary's \"stuff\""]
		]
	items: ["\ta", 2, "\t\tb\n"]
	}
console.log toNICE(obj)
```
results in:
```text
key: 'wood'
value:
	- 'a˳word'
	-
		a: 1
		b: 2
	- undef
	-
		- 1
		- 2
		- "mary's˳lamb"
		- «mary's˳"stuff"»
items:
	- '→a'
	- 2
	- '→→b®'
```
