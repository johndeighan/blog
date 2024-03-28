+++
title = "Text Fragments"
date = "2024-03-28T09:40:19-04:00"
tags = []
+++

Text Fragments are a new feature of modern web browsers,
supported by Google Chrome. I don't know
if other browsers support it, but it's a feature that I need,
so I'm using it for code documentation.

The idea is to allow a URL to to link to a particular part
of another document, without having to rely on that other
document containing anchors, i.e. places in the document that
you can link to. In my case, I want to display a file as a
plain text file (it's actually CoffeeScript code), and be able
to automatically scroll to some text that I specify.

There is already a standard for linking, by adding `#<id>` to a
URL, where `<id>` is an HTML element `id` attribute, which must
be added to the linked HTML document. That mechanism 1) only
works for HTML documents and 2) requires the author of the
linked document, which may be different than the author of the
linking document, to add that `id` attribute.

The way it works is that when you specify a URL to the linked
document, you add the string `#:~:text=<text>` to the URL, where
`<text>` is the text to link to. The text `<text>` must be `%`
encoded, e.g. a space character must be specified with `%20`.
You can add additional information, separated by commas, after
the `<text>`. For example:

`#:~:text=without` - will link to the first instance of the
	string "without" in the linked document

`#:~:text=linked%20URL` - will link to the first instance of the
	string "linked URL" in the linked document

`#:~:text=human,URL` - will link to the first instance of a
	string starting with "human" and ending with "URL"
	in the linked document

`#:~:text=without` - will link to the first instance of the
	string "without" in the linked document

You can also specify multiple text fragments by separating
them with a `&`

You can also style the selected text fragments with, e.g.:

```css
::target-text {
	background-color: rebeccapurple;
	color: white;
	}
```
