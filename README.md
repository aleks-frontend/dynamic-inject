# Dynamic inject
Function for injecting global inputs inside collection or spreadsheets

## Defining Source Elements
Source element should be a dummy div element with `js-inject-src` class and `data-target-id` attribute.

## Defining Target Elements
Target element should be a regular HTML element inside the collection or spreadsheet that needs to have
`data-target` attribute set to exact same value as it's source pair element's `data-target-id`.

### Example for adding text inputs (with or without rich text formatting)
```
<!-- Source Element -->
<div class="js-inject-src" data-target-id="footer-text">
  {{{ text-input }}}
</div>
...

<!-- Target Element -->
<div class="some-class-for-styling" data-target="footer-text"></div>
```
### Example for adding image inputs (without repositional tool enabled)
```
<!-- Source Element -->
<div class="js-inject-src" data-target-id="header-logo" data-is-image="true">
  {{{ image-input-regular }}}
</div>
...

<!-- Target Element -->
<img src="#" alt="Test Image" data-target="header-logo" />
```
Most important part here is to set the `data-is-image` attribute to **true**.

### Example for adding image inputs (WITH repositional tool enabled)
```
<!-- Source Element -->
<div class="js-inject-src" data-target-id="footer-bg" data-is-reposition="true">
  {{{ image-input-repositional }}}
</div>
...

<!-- Target Element -->
<div class="some-class-for-styling" data-target="footer-bg"></div>
```
**Important note:** When adding a source element for the input that is a repositional image, it shouldn't be set to `display:none` and shouldn't be placed inside of the hidden container. All the CSS required for it will be added dynamically here:
```      
if ( repositionCheck ) {
    const targetInfo = targets[0].getBoundingClientRect();
    const sourceCss = `position:absolute;left:0;top:0;opacity:0;width:${targetInfo.width}px;height:${targetInfo.height}px;`;
    source.style.cssText = sourceCss;
}```
   
