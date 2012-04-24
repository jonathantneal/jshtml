JSHTML
======

JSHTML is a javascript templating system for browsers and Node.js.  It's easy to use, performs exceptionally, and is totally customizable.  It is tested in all vendor supported browsers on both PC and Mac systems, including grandpa IE6+.

How to use it
-------------

First, add the JSHTML script to your site or page.

```html
<script src="jshtml.js"></script>
```

Then, create a new template.

```js
var tpl = new JSHTML();
```

Use JSHTML markup to format your templates.  Templates are compiled into native code on the fly for best performance.

```js
tpl.template("Hello, <%= name %>!");
```

Set a context for the template to use.  Even though templates are compiled, you can change the context whenever you want.

```js
tpl.context({ "name": "World" });
```

Render your templates.  If neither the template or the context changes, caching pumps up performance even more.

```js
document.body.innerHTML = tpl.render();
```

For your convenience, JSHTML is chainable.

```js
document.body.innerHTML = tpl.template("Hello, <%= name %>!").context({ "name": "World" }).render();
```

Customize everything
--------------------

You can customize everything in JSHTML.

```js
tpl.delimiters = {
	START_PROP: '{{',
	END_PROP:   '}}'
};
tpl.template("Hello, {{= name }}");
```

```js
tpl.helpers.u = function (content) {
	return '__out__+=' + content + '.toUpperCase();'; // __out__ is the internal variable name for the rendered content.
};

tpl.template('Hello, {{u name }}!').context({ "name": "World" });

tpl.render(); // "Hello, WORLD!"
```

```js
tpl.extenders.foo = function (content) {
	return '__out__+=' + content + '.toUpperCase();'
};

tpl.template('Hello, {{#foo name }}!').context({ "name": "World" });

tpl.render(); // "Hello, WORLD!"
```

```js
tpl.extenders.bar = function (content, isEnding) {
	return isEnding ? '}}' : 'for(var __property__ in ' + content + '){with(' + content + '[__property__]){';
};

tpl.template('Hello,{{#bar name}} {{u this}}{{/bar}}!').context({ "name": ["World", "Earth", "Planet"] });

tpl.render(); // "Hello, WORLD EARTH PLANET!"
```

Browser support
---------------

* Google Chrome
* Mozilla Firefox 3+
* Apple Safari 4+
* Opera 10+
* Internet Explorer 6+

License
-------

MIT

Acknowledgements
----------------

JSHTML is a project by [Jonathan Neal](http://github.com/jonathantneal).