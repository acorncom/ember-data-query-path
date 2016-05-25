# Ember-data-query-path

This mixin makes it easy for Ember Data to issue request to url paths.

## Requirements
* Ember >= 1.13.0
* Ember Data >= 1.13.0
* Ember CLI

## Installing

* ember-cli >= 0.2.3 `ember install ember-data-query-path`

## Upgrading

Please clear `node_modules` and `bower_components` before reporting issues after upgrading.

## Usage

To setup the plugin you must mix it into your store service.
```js
// app/services/store.js
import DS from 'ember-data';
import QueryPath from 'ember-data-query-path/mixins/query-path';

export default DS.Store.extend(QueryPath);
```

Then you can use `queryPath` and `queryPathRecord` methods on your store.

`queryPath` can be used to make a request a path that is expected to return an array of results.

```js
{
  /**
   `store.queryPath` will make a request to the findAll url for the type + the `path` argument provided as the 2nd parameter.
   A optional query object can be provided as the 3rd parameter. This method assumes your api will return an array of records as its response.

   This method is asynchronaous.

   @method queryPath
   @param {String} type
   @param {String} path
   @param {Object} query
   @return {Promise}
  */
  queryPath: function(type, path, query),
}
```

##### Example

```js
// app/routes/my-route.js
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    // request to /posts/recent?include=comments
    return this.store.queryPath('post', 'recent', { include: 'comments' });
  }
});
```

`queryRecordPath` can be used to make a request a path that is expected to return an a single record.

```js
{
  /**
   `store.queryRecordPath` will make a request to the findAll url for the type + the `path` argument provided as the 2nd parameter.
   A optional query object can be provided as the 3rd parameter. This method assumes your api will return a single record as its response.

   This method is asynchronaous.

   @method queryRecordPath
   @param {String} type
   @param {String} path
   @param {Object} query
   @return {Promise}
  */
  queryRecordPath: function(type, path, query),
}
```

##### Example

```js
// app/routes/my-route.js
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    // request to /users/current?include=permissions
    return this.store.queryRecordPath('user', 'current', { include: 'permissions' });
  }
});
```

The urls generated by `queryPath` and `queryPathRecord` will be prefixed by your any `host` and `namespace` properties you set on your adapter. If the `path` parameter starts with a `/` Ember Data will treat this as a absolute url and will not prefix it with the adapter `namespace` or the record type. If the record startys with `//` or `http` Ember Data will treat this as a fully qualified url and not prefix it with the adapter's `host` property.


## Development

* `git clone` this repository
* `npm install`
* `bower install`
* `ember server`
* Visit your app at http://localhost:4200.

## Running Tests

* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
