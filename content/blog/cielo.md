+++
title = "CieloScript"
date = "2024-02-07T06:54:11-05:00"
description = "Describe a new language, CieloScript"
tags = []
+++

I want to create a new language named **CieloScript** that is an
extension of CoffeeScript with these features:

1. Auto-imports and auto-install via `.symbols` file
2. Statement to allow async code within sync functions
3. multi-type HEREDOC syntax
4. Typing syntax to allow 1) documentation, 2) assertions
5. #include - to include files
6. #define - to define variables
7. __END__ ends a file
8. Allow additional type of quote: « (ALT+0171) » (ALT+0187)
9. Retain JavaScript style shebang line
10. The only **for** loop is `for <item> in <iterable>`
11. Add a config file to allow, e.g. ...lItems to gather, lItems... to spread
