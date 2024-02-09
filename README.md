Hugo web site setup and deploy
==============================

Use hugo-bearblog

```bash
$ hugo new site blog
$ cd blog
$ npm init -y
$ git init
$ git branch -m main
$ git submodule add https://github.com/janraasch/hugo-bearblog.git themes/hugo-bearblog
```

Change `package.json` to:

```json
```

Copy the contents of `themes/hugo-bearblog/exampleSite/hugo.toml`
to `hugo.toml`

Next, you should update these parts of your `hugo.toml` file:

1. `baseURL` which should be the URL of your blog,
	i.e. `https://johndeighan.github.io/blog/`
2. `title` - displayed at the top of your home page
3. `author` - your name
4. `copyright` - correct name and year
5. `description` - describe your web site

NOTE: The theme `hugo-bearblog` requires you to put
blog posts inside the content/blog folder.

```bash
$ hugo new blog/first.md
```

Edit the file blog/first.md. Test site with:

```bash
$ hugo serve -D
```

Add a new top-level page
------------------------

```bash
$ hugo new contact.md
```

Change the new page (`content/contact.md`) to:

```markdown
+++
title = 'Contact'
date = 2024-02-06T07:52:54-05:00
menu = "main"
+++

**John Doe**

You can email me at `<some email address>`
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
$ hugo serve
```

If everything is working ok, deploy with:

```bash
$ git add -A
$ git commit -m "<messaage>"
$ git push
```

NOTE: If you've made any changes directly on the GitHub.com
site, such as setting up a GitHub Actions workflow as above,
you will need to run `git pull` before it will allow you do
run `git push`.

Your changes will now be live.

