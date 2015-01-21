# grunt-csv-json [![Build Status][travis-image]][travis-url]

> Generate static JSON from CSV key/value data.

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-csv-json --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-csv-json');
```

## The "csvjson" task

### Overview

This task builds JSON structures from key/value data defined in CSV format.

In your project's Gruntfile, add a section named `csvjson` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  csvjson: {
    options: {
      // Task-specific options go here.
    },
    your_target: {
      // Target-specific file lists and/or options go here.
    }
  }
});
```

### CSV format

The expected format is one row per value, with the first column containing the key and the second the value.

#### Object hierarchy

Object hierarchy is expressed with dot notation in the key.

The following data:

| key         | value |
| ----------- | ----- |
| person.name | Bob   |
| person.sex  | male  |
| person.age  | 54    |

Will generate:

```json
{
	"person": {
		"name": "Bob",
		"sex": "male",
		"age": 54
	}
}
```

#### Implicit array syntax

Arrays of values can be implicitly defined by duplicating keys.

The following data:

| key           | value   |
| ------------- | ------- |
| shopping.day  | Sunday  |
| shopping.list | fruit   |
| shopping.list | candy   |
| shopping.list | pasta   |
| shopping.list | spinach |

Will generate:

```json
{
	"shopping": {
		"day": "Sunday",
		"list": ["fruit", "candy", "pasta", "spinach"]
	}
}
```

#### Explicit array syntax

Arrays of values can be explicitly defined by using integer keys.

The following data:

| key       | value   |
| --------- | ------- |
| list.0.0  | fruit   |
| list.0.1  | candy   |
| list.1.0  | pasta   |
| list.1.1  | spinach |

Will generate:

```json
{
	"list": [
		["fruit", "candy"],
		["pasta", "spinach"]
	]
}
```

[travis-url]: http://travis-ci.org/jpweeks/grunt-csv-json
[travis-image]: http://img.shields.io/travis/jpweeks/grunt-csv-json/master.svg?style=flat
