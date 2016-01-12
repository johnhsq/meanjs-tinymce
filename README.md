Add tinymce to [MEAN.JS](http://meanjs.org/)
===================
Using MEAN.JS and ng-file-upload to enable image upload to the Article module.

**Notes**: [MEAN.JS 0.4.2 (2015-11-11)](https://github.com/meanjs/mean/releases/tag/v0.4.2) [tinymce 4.3.2 (2015-12-14)](https://www.tinymce.com/docs/) [Angular ui-tinymce](https://github.com/angular-ui/ui-tinymce)


#### Install tinymce and angular-ui-tinymce
```bash
$ bower install tinymce --save
$ bower install angular-ui-tinymce --save
$ cd public/lib/angular-ui-tinymce/
$ bower install
```

#### Change MEAN.JS configuration
* /config/assets/default.js
```js
'public/lib/tinymce-dist/tinymce.js',
'public/lib/angular-ui-tinymce/src/tinymce.js'
```
* /modules/core/client/app/config.js
Inject ui.tinymce module to dependencies
```js
  var applicationModuleVendorDependencies = ['ngResource', 'ngAnimate', 'ngMessages', 'ui.router', 'ui.bootstrap', 'ui.utils', 'angularFileUpload', 'ui.tinymce'];
```
#### Configure tinymce for your needs
* /modules/articles/client/controllers/articles.client.controller.js

Add tinymce options for your needs; For more tinymce options, please refer to [tinymce's document](https://www.tinymce.com/docs/get-started/basic-setup/)
```js
// Configure tinymce options
$scope.tinymceOptions = {
  selector: 'textarea',
  inline: false,
  skin: 'lightgray',
  theme: 'modern',
  plugins: [
    'advlist autolink link image lists charmap print preview hr anchor pagebreak spellchecker',
    'searchreplace wordcount visualblocks visualchars code fullscreen insertdatetime media nonbreaking',
    'save table contextmenu directionality emoticons template paste textcolor'
  ],
  menubar: 'edit insert view format',
  toolbar: ['undo redo cut copy paste | link image | print preview fullscreen',
    'alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | forecolor backcolor | formatselect fontselect fontsizeselect '
  ],
  file_browser_callback: function(field_name, url, type, win) {
    //configure the file browser callback 
  }
};
```
#### Change Article Views
* /modules/articles/client/views/create-article.client.view.html

Add tinymce directives to your view
```html
<div class="form-group">
  <label for="content">Content</label>
  <textarea ui-tinymce="tinymceOptions" name="content" ng-model="article.content" class="form-control" cols="30" rows="12" placeholder="Content"></textarea>
</div>
```
