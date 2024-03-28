+++
title = "Binary"
date = "2024-03-08T10:46:38-05:00"
tags = []
+++

Adding a binary to a project
============================

Here, we define a binary as a command that, when you
install an npm project (the "outside project" into
another project (the "current project"), as long as
you're cd'd into the current project's root folder,
the command is available - without having to use `npx` or
`npm run`, i.e. by simply typing the name of the command,
along with any command line arguments.

NOTE: For this to work, you'll need to add the path
`./node_modules/.bin` to your Path environment variable.
If you don't want to do that, you'll have to prefix your
commands with `npx`. When testing a new binary from inside
the project where the binary resides, you'll have to prefix
your command with `npx` because there is not link to it in
your `node_modules/.bin` folder - it only contains links to
binaries the reside inside installed npm projects.

For example, say you create a new project named `newproj`.
In that project, you install the npm project
`@jdeighan/base-utils`. At that point, a command named
`for-each-file` is availabe. To execute that command, you
can enter this in your command shell:

```bash
$ for-each-file "**/*.coffee" -cmd="coffee -cmb --no-header <file>"
```



1. Use the command line `npx for-each-file <args>`, or

2. Add the path "./node_modules/.bin" to your Path environment
	variable, which makes all binaries from all installed
	outside projects available - as long as you're cd'd into
	the current project's root folder. In this case, you can
	just use the command line `for-each-file <args>`

So, how do you add a binary to the current project? Remember
that the point is to create the binary so that when the
current project is published to the npm registry, if someone
installs that project to their own project, they can
use the binary. We will cover how to test the binary that
you're working on in your current project later on.

Create the program implementing the binary
------------------------------------------

There are only 2 options that I'm going to cover:

1. Implement the binary as a JavaScript file

2. Implement the binary as a CoffeeScript file

In either case, the file will be placed in the `src/bin`
folder. If that folder doesn't exist, create it. If you
choose the CoffeeScript option, create a file named
`<name>.coffee`, where `<name>` is the name of your binary.
You'll also have to make sure that when your project is built,
the `*.coffee` file is compiled into a `*.js` file, possibly
with the following command:

```bash
$ coffee -cmb --no-header .
```
This command can be executed manually, or it can be added to
your "build" script in `package.json`.

NOTE:

The `-c` option means to compile one or more `*.coffee`
files to `*.js` files, and is therefore necessary.

The `-m` option causes a "source map" file to be created. If you do
that, error messages will provide you with line number is your
original `*.coffee` file; if not, error message will provide you
with line numbers in the resulting `*.js` file.

The `-b` option will cause CoffeeScript to NOT include a function
wrapper around your JavaScript code. Binaries may not execute
correctly unless you use this option.

The `--no-header` option will prevent CoffeeScript adding the
comment "# created with CoffeeScript" to your JavaScript file, which
is necessary because your code needs a "shebang line" (described
shortly), which will only be recognized if it's the very first line
in the file. Unfortunately, if CoffeeScript adds the comment above,
it will add it ABOVE the "shebang line", which would therefore not
be recognized. FYI, this is a long ago reported bug in CoffeeScript
which, apparently, they refuse to fix.

If you develop in pure JavaScript, the "shebang line" you
need to add as the very first line of the file is:

```js
#!/usr/bin/env node
```

If you develop in CoffeeScript, to be sure that the resulting
JavaScript file includes this as the very first line, your
CoffeeScript file should begin with:

```coffee
`#!/usr/bin/env node
`
```

Add a reference to the binary in your `package.json` file. For
example, the `@jdeighan/base-utils` library has this section
in its `package.json` file:

```json
	"bin": {
		"for-each-file": "./src/bin/for-each-file.js",
		"fef":           "./src/bin/for-each-file.js",
	},
```
This creates 2 commands, `for-each-file` and `fef` which,
in fact, execute the same script. Note that the file that
implements these 2 commands is a JavaScript files, which was
created by developing a CoffeeScript file, which was subsequently
compiled into a JavaScript file.


