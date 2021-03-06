# HoseJS [![CircleCI](https://circleci.com/gh/deptno/hosejs.svg?style=svg)](https://circleci.com/gh/deptno/hosejs)

[![npm](https://img.shields.io/npm/dt/hosejs.svg?style=for-the-badge)](https://www.npmjs.com/package/hosejs)

> :tada: Data handling with ramda.js (version 1.3 or higher)

![hosejs](https://github.com/deptno/hosejs/raw/master/asset/hosejs.gif)

> 100% code coverage.

You can transform JSON(or NOT) data with just **JavaScript** in terminal.

`jq`? javascript is clearly better option for people already use javascript.

## Feature

### Data handling with ramda.js (version 1.3 or higher)

You can use [ramda.js](https://ramdajs.com>)

eg. `http https://swapi.co/api/people/1/ | j -r "props(['name', 'height'])"`  
eg. `http https://swapi.co/api/people/1/ | j -ramda "props(['name', 'height'])"`  
eg. `http https://swapi.co/api/people/1/ | j "props(['name', 'height'])(_)"`

## Options

- `--file` option provide you to apply pre-defined script first
- `--tab` if result is Object, print JSON format with specified tab size (default: 2)

## Install

```
npm -g install hosejs
```

## Command

`j` or `js`


## Usage

`_` is everything you need to know

```bash
$ cat some.json | j '_.map(x => x.timestamp)'
$ cat some.json | j '_.map(x => x.timestamp)' --tab 4
$ cat some.json | j '_.map(x => x.timestamp)' --file pre.js --tab 2
$ cat some.json | j '_.map(x => x.timestamp)' > some.json
$ cat some.json | j '[_].map(x => x.some_property + '👍')[0]'
$ cat some.json | j '_.map(x => new Date(x.timestamp).toISOString())'
$ cat some.json | j --file preload.js '_.map(x => x.timestamp)'
$ http https://swapi.co/api/people/ | j 'Object.keys(_)'
$ http https://swapi.co/api/people/ | j '_.count'
$ http https://swapi.co/api/people/ | j '_.results.map(x => x.name)'
$ echo 'not json string \n !!' | j '_.split("\n")'
$ http https://swapi.co/api/people/1/ | j -r "props(['name', 'height'])"  
$ http https://swapi.co/api/people/1/ | j -ramda "props(['name', 'height'])"  
$ http https://swapi.co/api/people/1/ | j "props(['name', 'height'])(_)"

```

### Inject script file

#### IIFE

```js
// cw-oneline.js
(() => {
  const time = time => new Date(time).toISOString().slice(0, -5).replace('T', ' ')
  return _.map(x => `${time(x.timestamp)} ${x.message}`)
})()
```

```bash
cat downloaded-cw-log.json | j -f cw-oneline.js > deptno.latest.json
```

> Hmm ... Is it easy to look upside down?

add `_.reverse()`

```bash
cat downloaded-cw-log.json | j -f cw-oneline.js '_.reverse()' > deptno.latest.json
```

## License

MIT
