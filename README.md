## notice
this package is forked from https://github.com/pourquoi/ckeditor5-simple-upload

there is the change:

1. change `xhr.withCredentials = true` to `xhr.withCredentials = false`
2. change  `data.append('upload', this.loader.file)` to ` data.append('file', this.loader.file);`
## standard image upload button

### build integration

https://docs.ckeditor.com/ckeditor5/latest/builds/guides/development/custom-builds.html

```npm install ckeditor5-ice-upload```

add this plugin and remove the ckfinder and easyimage plugins

```javascript
// build-config.js

module.exports = {
	// ...
	
	plugins: [
        '@ckeditor/ckeditor5-essentials/src/essentials',
        // ...

        //'@ckeditor/ckeditor5-adapter-ckfinder/src/uploadadapter',
        //'@ckeditor/ckeditor5-easy-image/src/easyimage',

        'ckeditor5-ice-upload/src/iceupload'

        // ...
    ],

    // ...

    config: {
        toolbar: {
            items: [
                'headings',
                'bold',
                'italic',
                'imageUpload',
                'link',
                'bulletedList',
                'numberedList',
                'blockQuote',
                'undo',
                'redo'
            ]
        },
        // ...
    }
}
        
```

### configuration

```javascript
ClassicEditor.create(document.querySelector( '#editor' ), {
    iceUpload: {
        uploadUrl: 'http://127.0.0.1/my-upload-endpoint'
    }
})
```

```javascript
var cb = function() { return (new Date()).getTime() }
ClassicEditor.create(document.querySelector( '#editor' ), {
    iceUpload: {
        uploadUrl: {url:'http://127.0.0.1/my-upload-endpoint', headers:{ 'x-header':'myhead', 'x-header-cb': cb } }
    }
})
```

### backend

the endpoint will receive a file named **upload** and should return the image url

success response :
```json
{
    "uploaded": true,
    "url": "http://127.0.0.1/uploaded-image.jpeg"
}
```

failure response :
```json
{
    "uploaded": false,
    "error": {
        "message": "could not upload this image"
    }
}
```
