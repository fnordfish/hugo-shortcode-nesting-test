Demonstrates an issue with Hugo shortcodes loosing their "html context" when getting nested.

* Hugo GitHub issue: https://github.com/gohugoio/hugo/issues/11298
* Hugo Forum: https://discourse.gohugo.io/t/nested-shortcodes-render-markdown-in-html-content-file/45536

## Steps to reproduce

0. Clone this repo
1. Run `hugo server`
2. View the source of `http://localhost:1313/posts/test/`

Files of interest:

- [`layouts/shortcodes/outer.html`](themes/ananke/layouts/shortcodes/outer.html)
- [`layouts/shortcodes/inner.html`](themes/ananke/layouts/shortcodes/inner.html)
- [`content/posts/test.html`](content/posts/test.html)

## Expected behavior

Generated HTML should be:

```html
<!-- Start -->
<div class="page">
    <div class="inner">Test</div>
    <hr>
    <div class="inner">Test</div>
    <hr>
    No **markdown** expected here
    <hr>
    <div class="inner">Test</div>
    <div class="outer">
    
        <div class="inner">Test</div>
        <hr>
        <div class="inner">Test</div>
        <hr>
        No **markdown** expected here
        <hr>
        <div class="inner">No **markdown** expected here</p>
</div>
    
</div>
</div>
<!-- END -->
```

## Actual behavior

Generated HTML is:

```html
<!-- Start -->
<div class="page">
    <div class="inner">Test</div>
    <hr>
    <div class="inner">Test</div>
    <hr>
    No **markdown** expected here
    <hr>
    <div class="inner">Test</div>
    <div class="outer">
    
        <div class="inner"><p>Test</p>
</div>
        <hr>
        <div class="inner">Test</div>
        <hr>
        No **markdown** expected here
        <hr>
        <div class="inner"><p>No <strong>markdown</strong> expected here</p>
</div>
    
</div>
</div>
<!-- END -->
```
