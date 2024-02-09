+++
title = "TextTable"
date = "2024-02-09T11:08:38-05:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = []
+++

I've implemented a class named TextTable, for creating plain old
text tables, but with column widths automatically adjusted to fit
the data. Here is a simple usage example. It's in CoffeeScript,
but it should be easy to understand if you know that:

1. Parentheses around a function's parameters are not required,
	though, personally, I only omit them for a top level function
	or method call, to avoid ambiguity.
2. You must include the parentheses if you're calling a function
	or method that has no parameters.

```coffee
	import {TextTable} from '@jdeighan/base-utils/TextTable'

	table = new TextTable('l r%.2f r%.2f')
	table.title   'My Expenses'
	table.fullsep '-'
	table.labels  '', 'Jan', 'Feb'
	table.sep()
	table.data    'coffee', 30, 40
	table.data    'dining', 130, 40
	table.sep     '-'
	table.subtotals()
	table.data    'one time', 10, 20
	table.data    'other', 1000, 40
	table.fullsep '='
	table.totals()
	str = table.asString()
```

The variable `str` will contain:

```text
      My Expenses
-----------------------
             Jan    Feb
-------- ------- ------
coffee     30.00  40.00
dining    130.00  40.00
-------- ------- ------
          160.00  80.00
one time   10.00  20.00
other    1000.00  40.00
=======================
         1170.00 140.00
```

The string passed to the constructor establishes:

1. The number of columns, established by splitting the string
	on whitespace
2. The alignment of the data in each column, l=left, c=center, r=right
3. In addition to the alignment, you can provide a format specifier,
	which must begin with a `%` and uses the library `sprintf-js` to
	format the data.
