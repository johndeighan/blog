Hugo web site deploy
====================

Use hugo-bearblog

```bash
$ hugo new site blog
$ cd blog
$ git init
$ git branch -m main
$ git submodule add https://github.com/janraasch/hugo-bearblog.git themes/hugo-bearblog
```

Add `theme = 'hugo-bearblog'` to `hugo.toml`

NOTE: The theme `hugo-bearblog` requires you to put
blog posts inside the content/blog folder.

```bash
$ hugo new blog/first.md
```

Edit the file blog/first.md. Test site with:

```bash
$ hugo serve -D
```

Upload to GitHub
----------------

```bash
$ gh repo create
```

Choose 'Push an existing local repository to GitHub'
Create a new remote named origin

```bash
$ git add -A
$ git commit -m "first commit"
$ git push --set-upstream origin main
```

Add a file named `README.md`

```bash
$ git add -A
$ git commit -m "add a README file"
$ git push
```

Deploy to GitHub pages
----------------------

1. Log in to GitHub.com
2. Select your repository
3. Click on Settings
4. Click on Pages
5. Switch `Source` to `GitHub Actions`
6. Click on "Browse all workflows" and look for "Hugo"
	and click on "Configure"

Add a new blog post
-------------------

Locally, in your terminal, enter:

```bash
$ hugo new blog/second.md
```

Note that in this theme, when you create a new blog post,
the fontmatter does not include `draft:true`. Because of that,
the new post isn't considered a draft and you don't need the
`-D` on the command line when you start the dev server.

Edit the page created to contain your post in markdown format.

Test site with:

```bash
$ hugo serve -D
```

If everything is working ok, deploy with:

```bash
$ git add -A
$ git commit -m "<messaage>"
$ git push
```


