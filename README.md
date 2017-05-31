# metalsmith-debug-ui

![nodei.co](https://nodei.co/npm/metalsmith-debug-ui.png?downloads=true&downloadRank=true&stars=true)

![npm](https://img.shields.io/npm/v/metalsmith-debug-ui.svg)

![github-issues](https://img.shields.io/github/issues/leviwheatcroft/metalsmith-debug-ui.svg)

![stars](https://img.shields.io/github/stars/leviwheatcroft/metalsmith-debug-ui.svg)

![forks](https://img.shields.io/github/forks/leviwheatcroft/metalsmith-debug-ui.svg)

Browser based debug interface for [metalsmith](https://metalsmith.io)

Provides nice ui to navigate metalsmith files and metadata, allowing you to
view any stage of the build process

Features:

 * nice ui for exploring files & metadata
 * can jump forwards and backwards through the build process
 * cool react based client

![files interface][files]
![log interface][log]

See the [annotated source][1] or [github repo][2]

## install

`npm i --save metalsmith-debug-ui`

## usage

`metalsmith-debug-ui` clones your metalsmith files and metadata strutures at
different times during the build process and stores this history. Then it
injects a browser based client into your build output which allows you to view
that history.

### report on every plugin

In this mode you need to patch your metalsmith instance with `debugUi.patch`.

```javascript
import Metalsmith from 'metalsmith'
import debugUi from 'metalsmith-debug-ui'

let ms = Metalsmith('src')

debugUi.patch(ms)

ms
.use(...)
.build(...)
```

### report at specific points

Just call `debugUi.report` as a plugin

```javascript
import Metalsmith from 'metalsmith'
import debugUi from 'metalsmith-debug-ui'

let ms = Metalsmith('src') // no need to patch

debugUi.patch(ms)

ms
.use(myFirstPlugin({...}))
.use(mySecondPlugin({...}))
.use(debug.report('stage 1'))
.use(myFirstPlugin({...}))
.use(debug.report('stage 2'))
.build(...)
```

### viewing output

The client should be built with the rest of your site, and will be located at
`debug-ui/index.html` in your build directory. You should use your favourite
static development server to view it in the same way you would view anything
else in your build directory.

## options

nil

## plugin compatibility

Some plugins may not write to the `debug-ui` log, although I haven't found any
yet. In theory any plugins using `debug v2.x.x` should work. If you find one
please post an issue.

## testing

nil.

## building

Deprecation warning re: parseQuery is from upstream package. Don't worry about
it.

`npm run watch`

## Author

Levi Wheatcroft <levi@wht.cr>

## Contributing

Contributions welcome; Please submit all pull requests against the master
branch.

## License

 - **MIT** : http://opensource.org/licenses/MIT

[1]: https://leviwheatcroft.github.io/metalsmith-debug-ui "annotated source"
[2]: https://github.com/leviwheatcroft/metalsmith-debug-ui "github repo"
[files]: http://leviwheatcroft.github.io/metalsmith-debug-ui/images/files.png
[log]: http://leviwheatcroft.github.io/metalsmith-debug-ui/images/log.png
