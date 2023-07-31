Demonstrates an issue with Hugo shortcodes loosing their "html context" when getting nested.

## Steps to reproduce

0. Clone this repo
1. Run `hugo server`
2. View the source of `http://localhost:1313/posts/test/`

Files of interest:

- `layouts/shortcodes/outer.html`
- `layouts/shortcodes/inner.html`
- `content/posts/test.md`

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
