# materialize-autocomplete
Autocomplete styled with materialize-css


## Install
```sh
fecom install zhaojianfei/autocomplete
```

## Usage
Seeing [http://gitlab.58corp.com/zhaojianfei/searchRankPlatform](http://gitlab.58corp.com/zhaojianfei/searchRankPlatform)
![demo](https://cloud.githubusercontent.com/assets/3138397/16448711/6fbbb510-3e25-11e6-9d1d-3f28a97d640b.png)
+ When inputing, autocomplete prompts will show on dropdown list
+ Choosing an option use mouse or `↑`, `↓`, `Enter` keys
+ When enable multiple selection，click `x` to remove a tag

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
+ `$.fn.materialize_autocomplete(options) [function]: Bootstarp an `autocomplete` widget and returns an `Autocomplete` instance

## Autocomplete Constructor
+ `new Autocomplete(el, options) [function]`: Constructor
    + `el [string|object]`: DOM element on which the widget boostraped on
    + `options [object]`: Configuration object of the widget
        + `options.cacheable [boolean]`: Is dropdown data cacheable，default: `true`
        + `options.limit [number]`: Max items dropdown list shows，default: `10`
        + `options.multiple [object]`: Configuration object of multiple selection
            + `options.multiple.enable [boolean]`: Enabled or not, default: `false`
            + `options.multiple.maxSize [number]`: Max number of selections，default: `4`
            + `options.multiple.onExist [function]`: Callback when selection to append exists
            + `options.multiple.onExceed [function]`: Callback when selections exceed `maxSize`
            + `options.multiple.onAppend [function]`: Callback after appending a selection
            + `options.multiple.onRemove [function]`: Callback after removing a selection
        + `options.hidden [object]`: Configuration object of hidden input
            + `options.hidden.enable [boolean]`: Enabled or not, default: `false`
            + `options.hidden.el [string|object]`: Using an existing DOM element if not null, created one if null
            + `options.hidden.inputName [string]`: `name` attribute of hidden input
            + `options.hidden.required [boolean]`: `required` attribute of hidden input, default: `false`
        + `options.appender [object]`: Configuration object of appender (multiple is enabled)
            + `options.appender.el [string|object]`: Using an existing DOM element if not null, created one if null
            + `options.appender.tagName [string]`: TagName of appender if `options.appender.el` is null
            + `options.appender.className [string]`: `ClassName` attribute of appender
            + `options.appender.tagTemplate [string]`: Template string of appender item, using [undescore template](http://underscorejs.org/#template), **`data-id` and `data-text` attributes must be specified on outest DOM**
        + `options.dropdown [object]`: Configuration object of dropdown list
            + `options.dropdown.el [string|object]`: Using an existing DOM element if not null, created one if null
            + `options.dropdown.tagName [string]`: TagName of dropdown if `options.dropdown.el` is null
            + `options.dropdown.className [string]`: `ClassName` attribute of dropdown
            + `options.dropdown.itemTemplate [string]`: Template string of dropdown item, using [undescore template](http://underscorejs.org/#template), **`data-id` and `data-text` attributes must be specified on outest DOM**
            + `options.dropdown.noItem [string]`: Prompt for no data`，default is null
        + `options.handlers [object]`: Handlers for events of the widget
        + `options.getData(value, callback) [function]`: Function for getting data, asynchronous with a `callback` function，**arguments of callback**
            + `value [string]`: value of widget input element，when `input` event triggered, `value` will be passed to `getData` function
            + `callback(value, data) [function]`: Callback function
                + `value [string]`: Same as `value` above
                + `data [array]`: Data array，must be formatted as `[{ 'id': '1', 'text': 'a' }, { 'id': '2', 'text': 'b'}]`
        + `options.throttling [boolean]`: Throttling for `options.getData` function or not，default: `true`

`autocomplete` instance property:
+ `autocomplete.options [object]`: Configuration object
+ `autocomplete.$el [object]`: JQuery object the widget boostraped on
+ `autocomplete.$wrapper [object]`: Wrapper jQuery object，equal to `autocomplete.$el.parent()`
+ `autocomplete.compiled [object]`: Compiling functions for `tagTemplate` and `itemTemplate`
+ `autocomplete.$dropdown [object]`: JQuery object of dropdown
+ `autocomplete.$appender [object]`: JQuery object of appender
+ `autocomplete.$hidden [object]`: JQuery object of hidden input
+ `autocomplete.resultCache [object]`: Data cache object，used if `options.cacheable` is `true`
+ `autocomplete.value [array]`: Value

`autocomplete` instance methods:
+ `autocomplete.initialize() [function]`: Initializing method
+ `autocomplete.render() [function]`: Rendering method
+ `autocomplete.setValue(item) [function]`: Set-value method
    + `item [object]`: Selection object, formatted as `{ id: '1', text: 'a'}`
+ `autocomplete.append(item) [function]`: Method for appending an selection, called when **`options.multiple.enable` is `true`**
+ `autocomplete.remove(item) [function]`: Method for removing an selection, called when **`options.multiple.enable` is `true`**
+ `autocomplete.select(item) [function]`: Method for setting the value, called when **`options.multiple.enable` is `false`**
