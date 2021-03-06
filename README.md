# markdown-it-footnote-conventional

This is a fork of [`markdown-it-footnote`](https://github.com/markdown-it/markdown-it-footnote "markdown-it-footnote").

Here are the differences between this fork, and the `master` branch:

1. `<div class="footnotes">` is used in lieu of `<section class="footnotes">`
2. `<hr class="footnotes-sep">` is now a child of the `<div class="footnotes">` instead of a sibling

The first change I made is just a personal preference. Based on the [spec](https://www.w3.org/TR/html5/sections.html#the-section-element), I don't believe the footnotes section at the bottom of a post/page has the same *semantic* meaning as a `<section>`.

The second change I made allows [Bigfoot.js](http://www.bigfootjs.com "Bigfoot.js") to work more consistently. The Bigfoot JavaScript already removed the `<section class="footnotes">`, but it was not removing the `<hr class="footnotes-sep">`, because the `master` branch of `markdown-it-footnote` placed the `<hr class="footnotes-sep">` *outside* of the `<section class="footnotes">`---not within it. As a sibling and not a child of the `<section class="footnotes">`, Bigfoot wouldn't remove the `<hr class="footnotes-sep">`. It does now :)

***

[![Build Status](https://img.shields.io/travis/markdown-it/markdown-it-footnote/master.svg?style=flat)](https://travis-ci.org/markdown-it/markdown-it-footnote)
[![NPM version](https://img.shields.io/npm/v/markdown-it-footnote.svg?style=flat)](https://www.npmjs.org/package/markdown-it-footnote)
[![Coverage Status](https://img.shields.io/coveralls/markdown-it/markdown-it-footnote/master.svg?style=flat)](https://coveralls.io/r/markdown-it/markdown-it-footnote?branch=master)

> Footnotes plugin for [markdown-it](https://github.com/markdown-it/markdown-it) markdown parser.

__v2.+ requires `markdown-it` v5.+, see changelog.__

Markup is based on [pandoc](http://johnmacfarlane.net/pandoc/README.html#footnotes) definition.

__Normal footnote__:

```
Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

    Subsequent paragraphs are indented to show that they
belong to the previous footnote.
```

html:

```html
<p>Here is a footnote reference,<sup class="footnote-ref"><a href="#fn1" id="fnref1">[1]</a></sup> and another.<sup class="footnote-ref"><a href="#fn2" id="fnref2">[2]</a></sup></p>
<p>This paragraph won’t be part of the note, because it
isn’t indented.</p>
<div class="footnotes">
<hr class="footnotes-sep">
<ol class="footnotes-list">
<li id="fn1"  class="footnote-item"><p>Here is the footnote. <a href="#fnref1" class="footnote-backref">↩</a></p>
</li>
<li id="fn2"  class="footnote-item"><p>Here’s one with multiple blocks.</p>
<p>Subsequent paragraphs are indented to show that they
belong to the previous footnote. <a href="#fnref2" class="footnote-backref">↩</a></p>
</li>
</ol>
</div>
```

__Inline footnote__:

```
Here is an inline note.^[Inlines notes are easier to write, since
you don't have to pick an identifier and move down to type the
note.]
```

html:

```html
<p>Here is an inline note.<sup class="footnote-ref"><a href="#fn1" id="fnref1">[1]</a></sup></p>
<div class="footnotes">
<hr class="footnotes-sep">
<ol class="footnotes-list">
<li id="fn1"  class="footnote-item"><p>Inlines notes are easier to write, since
you don’t have to pick an identifier and move down to type the
note. <a href="#fnref1" class="footnote-backref">↩</a></p>
</li>
</ol>
</div>
```


## Install

node.js, browser:

```bash
npm install markdown-it-footnote-conventional --save
bower install markdown-it-footnote-conventional --save
```

## Use

```js
var md = require('markdown-it')()
            .use(require('markdown-it-footnote-conventional'));

md.render(/*...*/) // See examples above
```

_Differences in browser._ If you load script directly into the page, without
package system, module will add itself globally as `window.markdownitFootnote`.


## License

[MIT](https://github.com/markdown-it/markdown-it-footnote/blob/master/LICENSE)
