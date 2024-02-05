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

