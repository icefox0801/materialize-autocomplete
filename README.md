# materialize-autocomplete
Materialize-css styled autocomplete 


## Install
+ npm 
```sh
$ npm install materialize-autocomplete
```
+ bower
```sh
$ bower install materialize-autocomplete
```

## Usage
![demo](https://cloud.githubusercontent.com/assets/3138397/16448711/6fbbb510-3e25-11e6-9d1d-3f28a97d640b.png)
+ When typing inside an input, autocomplete prompts will show on dropdown list
+ Choosing an option by click or `↑`, `↓`, `Enter` keys
+ Removing a selection by click `x` when enable multiple selection

```javascript
var autocomplete =$('#el').autocomplete({
    limit: 20,
    multiple: {
        enable: true,
        maxSize: 10,
        onExist: function (item) { /* ... */ },
        onExceed: function (maxSize, item) { /* ... */ }
    },
    appender: {
        el: '#someEl'
    },
    getData: function (value, callback) {
        // ...
        callback(value, data);
    }
});
```

## $.fn.materialize_autocomplete
+ `$.fn.materialize_autocomplete(options) [function]`: Initialize an `autocomplete` widget and return an `Autocomplete` instance

## Autocomplete options
+ `cacheable [boolean]`: Dropdown data cacheable or not, default: `true`
+ `limit [number]`: Max number of items show in dropdown, default: `10`
+ `multiple [object]`: Configuration of multiple selection
    + `multiple.enable [boolean]`: Enabled or not, default: `false`
    + `multiple.maxSize [number]`: Max number of selections，default: `4`
    + `multiple.onExist [function]`: Callback when selection to append exists
    + `multiple.onExceed [function]`: Callback when selections exceed `maxSize`
    + `multiple.onAppend [function]`: Callback after appending a selection
    + `multiple.onRemove [function]`: Callback after removing a selection
+ `hidden [object]`: Configuration of hidden input (used for storing **ids** joined by selections)
    + `hidden.enable [boolean]`: Enabled or not, default: `false`
    + `hidden.el [string|object]`: Applying an existing DOM element if not null, otherwise created one, default: `''`
    + `hidden.inputName [string]`: `name` attribute of hidden input, default: `''`
    + `hidden.required [boolean]`: `required` attribute of hidden input, default: `false`
+ `appender [object]`: Configuration of appender (where to append selections when multiple selection is enabled)
    + `appender.el [string|object]`: Applying an existing DOM element if not null, otherwise created one, default: `''`
    + `appender.tagName [string]`: `TagName` of appender when `appender.el` is null, default: `ul`
    + `appender.className [string]`: `ClassName` attribute of appender, default: `ac-appender`
    + `appender.tagTemplate [string]`: Template string of selections inside appender, using [undescore template](http://underscorejs.org/#template), **`data-id` and `data-text` attributes should be specified on outest DOM**
+ `dropdown [object]`: Configuration of dropdown
    + `dropdown.el [string|object]`: Applying an existing DOM element if not null, otherwise created one, default: `''`
    + `dropdown.tagName [string]`: `TagName` of dropdown when `dropdown.el` is null, default: `ul`
    + `dropdown.className [string]`: `ClassName` attribute of dropdown, default: `ac-dropdown`
    + `dropdown.itemTemplate [string]`: Template string of items inside dropdown, using [undescore template](http://underscorejs.org/#template), **`data-id` and `data-text` attributes should be specified on outest DOM**
    + `dropdown.noItem [string]`: Prompt for no data`，default: `''`
+ `handlers [object]`: Event handlers of the widget
+ `getData(value, callback) [function]`: Function for getting dropdown list data, asynchronous called with a `callback`
    + `value [string]`: Input value，when `input` event triggered, `getData` function will be called with input value
    + `callback(value, data) [function]`: Callback function
        + `value [string]`: Same as `value` above
        + `data [array]`: Data array，should be formatted as `[{ 'id': '1', 'text': 'a' }, { 'id': '2', 'text': 'b'}]`
+ `options.throttling [boolean]`: Throttling for `getData` function or not，default: `true`


## Autocomplete
### Constructor
+ `new Autocomplete(el, options) [function]`: Constructor
    + `el [string|object]`: DOM element on which the widget applys
    + `options [object]`: Configuration of the widget

### Instance property:
+ `autocomplete.options [object]`: Configuration object
+ `autocomplete.$el [object]`: JQuery object on which the widget applys
+ `autocomplete.$wrapper [object]`: Wrapper jQuery object，equal to `autocomplete.$el.parent()`
+ `autocomplete.compiled [object]`: Compiling functions for `tagTemplate` and `itemTemplate`
+ `autocomplete.$dropdown [object]`: JQuery object of dropdown
+ `autocomplete.$appender [object]`: JQuery object of appender
+ `autocomplete.$hidden [object]`: JQuery object of hidden input
+ `autocomplete.resultCache [object]`: Result cache object of `getData` when `cacheable` is `true`
+ `autocomplete.value [array]`: Value of widget, when multiple selection is enabled, `autocomplete.value` is **ids** joined by selections, otherswise `autocomplete.value` is **id** of a selection

### Instance methods:
+ `autocomplete.initialize() [function]`: Initializing method
+ `autocomplete.render() [function]`: Rendering method
+ `autocomplete.setValue(item) [function]`: Value setting method
    + `item [object]`: Selection object, e.g. `{ id: '1', text: 'a'}`
+ `autocomplete.append(item) [function]`: Appending an selection, called when **`options.multiple.enable` is `true`**
+ `autocomplete.remove(item) [function]`: Removing an selection, called when **`options.multiple.enable` is `true`**
+ `autocomplete.select(item) [function]`: Setting the value, called when **`options.multiple.enable` is `false`**
