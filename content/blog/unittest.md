+++
title = "Unit Testing"
date = "2024-02-20T08:52:34-05:00"
tags = []
+++

My unit tests are set up this way:

1. Create your project using `npm init` so that, e.g.
	there is a `package.json` file in your project root.

2. Use `npm install -D` to install these npm packages:
	- ava
	- coffeescript

3. Use `npm install` to install these npm packages:
	- @jdeighan/base-utils

4. Create the file `.gitignore` in your project root:

```text
node_modules/
.npm
.env
.env.test
test/temp*.*
```

5. Create the file `.npmrc` in your project root:

```text
engine-strict=true
loglevel=silent
```

6. Create a `test` folder in your project root.

7. Include these scripts under the `script` key in
	your `package.json` file:
	- `"build": "clear && npx coffee -cm -b --no-header .",`
	- `"test": "npm run build && npx ava ./test/*.test.js && git status"`

	NOTE: I prefer clearing the screen before a build, but if
	you don't, just remove that. Feel free to pass other options
	to the coffee command and to add other steps to the build.
	If you have CoffeeScript installed globally, you can remove
	the "npx" from "npx coffee".

8. Add this to your `.bashrc` file:

```bash
function utest
{
clear
npm run build
npx ava test/$1.test.js
}
```
	(when you first do this, you'll need to either restart your
	terminal or enter the command `source ../.bashrc` or whatever
	the path is to your .bashrc file)

Running unit tests
------------------

You can now run all unit test with the command `npm test`.
Alternatively, you can run a specific unit test with the
command `utest <name>`. To illustrate, let's create 2 unit
test files:

Create the file `./test/add.test.coffee`:

```coffee
import {u} from '@jdeighan/base-utils/utest'

u.equal 2+3, 5
u.equal 12+23+4, 39
```

Create the file `./test/mult.test.coffee`:

```coffee
import {u} from '@jdeighan/base-utils/utest'

u.equal 2*3, 6
u.equal 12*23*4, 1104
```

Now you can run individual tests with:

```bash
$ utest add
```

You can run all unit tests with:

```bash
$ npm test
```

Which, if all tests pass, will tell you which files
have not been committed to git yet.

Note the following:

1. There is no need to name tests. The result of each
	test is reported by line number in the unit test
	file, which is all you need to identify the test.
2. The intent of the test is so clear that the unit
	tests serve as documentation for, e.g., functions
	that are invoked in the test. For example, if you
	have a function that centers text in a given width,
	you might have tests like this:

```coffee
u.equal center('abc', 3), 'abc'
u.equal center('abc', 0), 'abc'
u.equal center('abc', 4), 'abc '
u.equal center('abc', 10), '   abc    '
```

