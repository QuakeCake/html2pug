# html2pug [![Build Status](https://travis-ci.org/QuakeCake/html2pug.svg?branch=master)](https://travis-ci.org/QuakeCake/html2pug)

## Why the fork?

I needed an implementation of this module that would support conditionals so I modified it. 

Not sure if the original author wants this feature pulled into the main repo so I'm waiting for a reply [here](https://github.com/izolate/html2pug/issues/38)

### Conditionals Usage

You can use the made up html tags `<if>` `<else>` `<unless>` and having the condition in the condition attribute

This HTML:

```html
<if condition="false">Will not be shown</if>
<else if condition="true">Will be shown</else>
<else>Will never be shown</else>
```

Will become:

```pug
if false
  | Will not be shown
else if true
  | Will be shown
else
  | Will never be shown
```

## What does it do?

Converts **HTML** to **Pug** templating language (_formerly Jade_).  
Requires Node.js version `7.6` or higher.

Turns this :unamused:
```html
<!doctype html>
<html lang="en">
  <head>
    <title>Hello World!</title>
  </head>
  <body>
    <div id="content">
      <h1 class="title">Hello World!</h1>
    </div>
  </body>
</html>
```

Into this :tada:
```pug
doctype html
html(lang='en')
  head
    title Hello World!
   body
    #content
      h1.title Hello World!
```

## Install

Get it on [npm](https://www.npmjs.com/package/html2pug):

```bash
npm install -g html2pug
```

## Usage

### CLI
Accept input from a file or stdin and write to stdout:

```bash
# choose a file
html2pug < example.html

# use pipe
echo '<h1>foo</h1>' | html2pug -f
```

Write output to a file:
```bash
html2pug < example.html > example.pug
```

See `html2pug --help` for more information.

### Programmatically

```js
const html2pug = require('html2pug')

const html = '<header><h1 class="title">Hello World!</h1></header>'
const pug = html2pug(html, { tabs: true })
```

### Options

Name | Type | Default | Description
--- | --- | --- | ---
`tabs` | `Boolean` | `false` | Use tabs instead of spaces for indentation
`commas` | `Boolean` | `true` | Use commas to separate node attributes
`doubleQuotes` | `Boolean` | `false` | Use double quotes instead of single quotes for attribute values
`fragment` | `Boolean` | `false` | Wraps result in enclosing `<html>` and `<body>` tags if false
