<p align="center">
 <img src="http://simplaio.github.io/rucksack/logo.png" alt="rucksack logo" height="325" />
</p>

<p align="center">
  <a href="https://npmjs.org/package/rucksack-css" target="_blank"><img src="https://badge.fury.io/js/rucksack-css.svg" alt="NPM version" /></a>
  <a href="https://travis-ci.org/simplaio/rucksack" target="_blank"><img src="https://travis-ci.org/simplaio/rucksack.svg?branch=master" alt="Build satus" /></a>
  <a href="https://david-dm.org/simplaio/rucksack" target="_blank"><img src="https://david-dm.org/simplaio/rucksack.svg?theme=shields.io" alt="Dependency Status" /></a>
</p>

<br/>

A little bag of CSS superpowers, built on [PostCSS][postcss].

Rucksack makes CSS development less painful, with the features and shortcuts it should have come with out of the box.

Made with &#9829; by the folks at [Simpla][simpla].

--

### Install

```sh
$ npm install --save rucksack-css postcss
```

--

### Usage

###### Gulp
Use [gulp-rucksack][gulp-rucksack]
```js
var gulp = require('gulp');
var rucksack = require('gulp-rucksack');

gulp.task('rucksack', function() {
  return gulp.src('src/style.css')
    .pipe(rucksack())
    .pipe(gulp.dest('style.css'));
});```

<br/>

###### Grunt
Use [grunt-rucksack][grunt-rucksack]

```js
require('load-grunt-tasks')(grunt);

grunt.initConfig({
	rucksack: {
		compile: {
			files: {
				'style.css': 'src/style.css'
			}
		}
	}
});

grunt.registerTask('default', ['rucksack']);
```

<br/>

###### Broccoli
Use [broccoli-rucksack][broccoli-rucksack]

```js
var rucksack = require('broccoli-rucksack');
tree = rucksack(tree, [options]);
```

<br/>

###### CLI
Process CSS directly on the command line

```sh
$ rucksack src/style.css style.css [options]
```

<br/>

###### PostCSS
Rucksack is built on PostCSS, and can be used as a PostCSS plugin.

```js
var postcss = require('postcss'),
    rucksack = require('rucksack-css');

postcss([ rucksack() ])
  .process(css, { from: 'src/style.css', to: 'style.css' })
  .then(function (result) {
      fs.writeFileSync('style.css', result.css);
      if ( result.map ) fs.writeFileSync('style.css.map', result.map);
  });
```
 See the [PostCSS Docs][postcss] for examples for your environment.

 <br/>

###### Stylus
Stylus can be used as a Stylus plugin with [PostStylus][poststylus]

```js
stylus(css).use(poststylus('rucksack-css'))
```

See the [PostStylus Docs][poststylus] for more examples for your environment.

--

### Core Features

_Automagical responsive typography_
```css
.foo {
  font-size: responsive;
}
```
![Responsive Type Demo][type-demo]


_Shorthand syntax for positioning properties_
```css
.foo {
  absolute: 0 20px;
  relative: 20% 0 30px;
}
```

_Native clearfix_
```css
.foo {
  clear: fix;
}
```

_Hex shortcuts for RGBA_
```css
.foo {
  color: rgba(#fff, 0.8);
}
```

_Shorthand `@font-face` src sets (becomes [FontSpring syntax][fontspring])_
```css
@font-face {
  font-family: 'My Font';
  font-path: '/path/to/font/file';
}
```

_Whole library of modern easing functions_
```css
.foo {
  transition: all 250ms ease-out-elastic;
}
```

_Powerful quantity pseudo-selectors_
```css
li:at-least(4) {
  color: blue;
}

li:between(4,6) {
  color: red;
}
```

_CSS property aliases_
```css
@alias {
  fs: font-size;
  bg: background;
}

.foo {
  fs: 16px;
  bg: #fff;
}
```

--

### Optional Extras

###### Autoprefixing
Automatically apply vendor prefixes to relevant properties based on data from [CanIUse][caniuse].


###### Legacy Fallbacks
Automatically insert legacy fallbacks for modern properties.
```css
/* before */
.foo {
  color: rgba(0,0,0,0.8);
  width: 50vmin;
}

.foo::before{
  opacity: 0.8;
}

/* after */
.foo {
  color: rgb(0,0,0);
  color: rgba(0,0,0,0.8);
  width: 50vm;
  width: 50vmin;
}

.foo:before{
  opacity: 0.8;
  -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=80)";
}
```

###### New Default Colors
Swap out those ugly default colors with replacements from [Material Design Colors][material-colors].

--

### Options

Pass booleans to toggle optional extras on/off
```js
.rucksack({
  /* options */
})
```

`autoprefixer`: Toggle autoprefixing on/off (default: `true`).

`fallbacks`: Toggle legacy fallbacks on/off (default: `true`).

`colors`: Toggle color replacements on/off (default: `true`).

--

### License

MIT © [Simpla][simpla]

[simpla]: http://simpla.io
[postcss]: https://github.com/postcss/postcss
[gulp-rucksack]: https://github.com/simplaio/gulp-rucksack
[grunt-rucksack]: https://github.com/simplaio/grunt-rucksack
[broccoli-rucksack]: https://github.com/simplaio/broccoli-rucksack
[poststylus]: https://github.com/simplaio/poststylus
[type-demo]: /type-demo.gif?raw=true
[fontspring]: http://blog.fontspring.com/2011/02/further-hardening-of-the-bulletproof-syntax/
[caniuse]: http://caniuse.com
[material-colors]: https://www.google.com/design/spec/style/color.html
