electron
========

From video course:

```bash
$ mkdir videoinfo
$ cd videoinfo
$ npm init -y
$ npm install electron
```

```bash
node ./src/bin/make-new-project.js temp -type=electron
```

Create file `main.coffee`:

```coffee
import {app} from 'electron'

app.on 'ready', () =>
	console.log "App is ready"

```
