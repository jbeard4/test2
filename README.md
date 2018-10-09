### What I Wanted to Do

I want to install a package which has a dependency on licensezero-postinstall.
licensezero-postinstall has a devDependency on the `standard` library, and a
dependency on `wordwrap`. I expect that when I run `npm install --production`,
the dependency `wordwrap` will be installed, and `standard` will not be installed. 

I also expect that running `npm ls --production` will not show any extraneous
dependencies.

This is important because, for example, `vsce` uses `npm ls --production`
command to build packages for the visual studio code marketplace, and expects
`npm ls` to not have any extraneous dependencies.

Finally, `npm prune --production` does not remove the `standard` library.

### What Happened Instead

`standard` will be installed, and `npm ls` will show `standard` as an
extraneous dependency.

### Reproduction Steps

```
git clone git@github.com:jbeard4/test2.git`
cd test2
npm install --production
npm ls --production
```

Shows extraneous dependency:

```
test2@1.0.0 /Users/jbeard4/tmp/test2
└─┬ licensezero-postinstall@1.0.0
  ├── standard@11.0.1 extraneous
  └── word-wrap@1.2.3

npm ERR! extraneous: standard@11.0.1 /Users/jbeard4/tmp/test2/node_modules/licensezero-postinstall/node_modules/standard
```


### Details

<!-- Add more details and comments if you'd like -->

<!-- If available, please attach the npm-debug.log file -->

### Platform Info

```
$ npm --versions
{ test2: '1.0.0',
  npm: '6.4.1',
  ares: '1.10.1-DEV',
  cldr: '32.0',
  http_parser: '2.8.0',
  icu: '60.1',
  modules: '57',
  napi: '3',
  nghttp2: '1.32.0',
  node: '8.12.0',
  openssl: '1.0.2p',
  tz: '2017c',
  unicode: '10.0',
  uv: '1.19.2',
  v8: '6.2.414.66',
  zlib: '1.2.11' }
$ node -p process.platform
darwin
```
