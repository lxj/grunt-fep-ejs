# grunt-fep-ejs

> Compile ejs templates.



## Getting Started
This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-fep-ejs --save-dev
```

```js
grunt.loadNpmTasks('grunt-fep-ejs');
```

## ejs task
_Run this task with the `grunt jade` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.
### Options

#### data
Type: `Object`

Sets the data passed to Jade during template compilation. Any data can be passed to the template (including grunt templates).

This value also might be a function taking source and destination path as arguments and returning a data object. Within the function, `this` is bound to the file configuration object.

```js
options: {
  data: function(dest, src) {
    return {
      from: src,
      to: dest
    };
  }
}
```

or you can have options from a required JSON file:

```js
options: {
  data: function(dest, src) {
    // Return an object of data to pass to templates
    return require('./locals.json');
  }
}
```

#### compileDebug
Type: `Boolean`
Default: **true**

Add Jade debug instructions to generated JS templates.

#### client
Type: `Boolean`
Default: **false**

Compile to JS template functions for client-side use rather than directly to HTML.

Make sure to also include the Jade runtime (only `runtime.js`) as described in the [Jade documentation](https://github.com/visionmedia/jade#browser-support).

#### namespace
Type: `String`, `Boolean`
Default: **JST**

The namespace in which the precompiled templates will be assigned. Use dot notation (*e.g.* `App.Templates`) for nested namespaces or `false` for no namespace wrapping.

When set to `false` with **amd** option set to `true`, the templates will be returned directly from the AMD wrapper.



#### parseContent
Type: `Function`
Default: `function(content) { return content; };`

This option accepts a function that lets you perform additional content processing.

### Usage Examples

```js
ejs: {
  compile: {
    files: {
      'tmp/function.html': ['test/function.ejs'],
      'tmp/list.html': ['test/list.ejs']
    },
    options: {
      open : "<%",
      close: "%>",
      data: {
        test: true,
        year: '<%= grunt.template.today("yyyy") %>',
        names : ["Tobi","Loki","Sean","bei"],
        users : [{ name: 'Tobi', age: 2, species: 'ferret' },{ name: 'Loki', age: 2, species: 'ferret' },{ name: 'Jane', age: 6, species: 'ferret' }],
        navs : [{ name: 'index', href: 'index.html'},{ name: 'demo', href: 'demo.html'},{ name: 'about', href: 'about.html'},{ name: 'download', href: 'download.html'}]
      }
    }
  }
}
```

