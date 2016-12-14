# Upload

<p class="uk-text-lead">Upload files through a file input form element or a placeholder area.</p>

## Usage

This JavaScript component utilizes the latest XMLHttpRequest Level 2 specification and provides the ability of uploading files via Ajax including tracking of the upload progress. The component provides two ways of uploading files: `select` and `drop`. While the `select` request can only be applied to `<input type="file">` elements, you can basically use any element with `drop`, which enables you to simply drag and drop files from your desktop into the specified element to upload them. Note that this component does not handle your file uploads on the server.

***

## Select

In this example we are using a simple button which opens up the file select window.

```example
<button class="uk-form-custom uk-button uk-button-default">
    Select
    <input type="file" multiple="">
</button>
```

***

## Drop Area

This example shows how to realize a drop area with the option to select the file from a file window. 

```example
<div class="test-upload uk-placeholder uk-text-center">
    <span uk-icon="icon: cloud-upload"></span>
    <span class="uk-text-middle">Attach binaries by dropping them here or</span>
    <a class="uk-form-custom">selecting one<input type="file" multiple></a>
</div>

<progress id="progressbar" class="uk-progress" value="0" max="100" hidden></progress>

<script>

(function ($) {

    var bar = $("#progressbar")[0];

    UIkit.upload('.test-upload', {

        url: '',
        multiple: true,

        beforeSend: function() { console.log('beforeSend', arguments); },
        beforeAll: function() { console.log('beforeAll', arguments); },
        load: function() { console.log('load', arguments); },
        error: function() { console.log('error', arguments); },
        complete: function() { console.log('complete', arguments); },

        loadStart: function (e) {
            console.log('loadStart', arguments);

            bar.removeAttribute('hidden');
            bar.max =  e.total;
            bar.value =  e.loaded;
        },

        progress: function (e) {
            console.log('progress', arguments);

            bar.max =  e.total;
            bar.value =  e.loaded;

        },

        loadEnd(e) {
            console.log('loadEnd', arguments);

            bar.max =  e.total;
            bar.value =  e.loaded;
        },

        completeAll: function () {
            console.log('completeAll', arguments);

            setTimeout(function () {
                bar.setAttribute('hidden', 'hidden');
            }, 1000);

            alert('Upload Completed');
        }
    });

})(jQuery);

</script>

```

***

## JavaScript

To create `select` and `drop` upload listeners, you need to instantiate each upload class with the target element and options, which define callbacks and useful settings.

```html
<script>

(function ($) {

    var bar = $("#progressbar")[0];

    UIkit.upload('.test-upload', {

        url: '',
        multiple: true,

        beforeSend: function() { console.log('beforeSend', arguments); },
        beforeAll: function() { console.log('beforeAll', arguments); },
        load: function() { console.log('load', arguments); },
        error: function() { console.log('error', arguments); },
        complete: function() { console.log('complete', arguments); },

        loadStart: function (e) {
            console.log('loadStart', arguments);

            bar.removeAttribute('hidden');
            bar.max =  e.total;
            bar.value =  e.loaded;
        },

        progress: function (e) {
            console.log('progress', arguments);

            bar.max =  e.total;
            bar.value =  e.loaded;

        },

        loadEnd(e) {
            console.log('loadEnd', arguments);

            bar.max =  e.total;
            bar.value =  e.loaded;
        },

        completeAll: function () {
            console.log('completeAll', arguments);

            setTimeout(function () {
                bar.setAttribute('hidden', 'hidden');
            }, 1000);

            alert('Upload Completed');
        }
    });

})(jQuery);

</script>
```

***

## Component options

| Option | Value | Default | Description |
| --- | --- |
| `url` | String | '' | The request url. |
| `multiple` | Boolean | false | Allow multiple files to be uploaded. |
| `name` | String | 'files[]' | The name parameter. |
| `type` | String | POST | The request type. |
| `params` | Object | {} | Additional parameters. |
| `allow` | String | false | File name filter. (eg. *.png) |
| `mime` | String | false | File MIME type filter. (eg. images/*) |
| `concurrent` | Number | 1 | Number of files that will be uploaded simultaneously. |
| `dataType` | String | (xml, json, script, or html) | The expected response data type. |
| `msg-invalid-mime` | String | Invalid File Type: %s | Invalid MIME type message. |
| `msg-invalid-name` | String | Invalid File Name: %s | Invalid name message. |
| `clsDragover` | String | 'uk-dragover' | File name filter. |
| `abort` | Function | null | The abort callback. |
| `beforeAll` | Function | null | The beforeAll callback. |
| `beforeSend` | Function | null | The beforeSend callback. |
| `complete` | Function | null | The complete callback. |
| `completeAll` | Function | null | The completeAll callback. |
| `error` | Function | null | The error callback. |
| `load` | Function | null | The load callback. |
| `loadEnd` | Function | null | The loadEnd callback. |
| `loadStart` | Function | null | The loadStart callback. |
| `progress` | Function | null | The progress callback. |
| `fail` | Function | alert | The fail callback. If name or MIME type are invalid. |