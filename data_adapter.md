Rendr DataAdapter
=================

#### Overview

The purpose of the DataAdapter is to allow your application to have a completely customisable data layer.

The DataAdapter works with an ApiProxy. This means that you can grab data from anywhere you like on the server, while usingjust one api for your app models, allowing them to fetch data regardless of whether they are on the server or the client.

In a nutshell:

- From a controller, you call `this.app.fetch(spec)`
- Render will then pass the api request on to the provided DataAdapter
- The DataAdapter will then __fetch__ the data using whatever method it wants
- The DataAdapter will then pass the fetched data _(or error)_ back to the Rendr app
- Rendr will __populate__ the model that requested the data

Rendr will take whatever data object the DataAdapter gives it, and then send it to the model that did the fetch.


#### The Default DataAdapter

Render comes with a base [DataAdapter](https://github.com/rendrjs/rendr/blob/0.5.0-rc2/server/data_adapter/index.js) class that comes with no functionality, it is just there for you to extent if you wish. `rendr/server/data_adapter/index.js`

By deault, Rendr sets you up to use their [RestAdapter](https://github.com/rendrjs/rendr/blob/0.5.0-rc2/server/data_adapter/rest_adapter.js). This is great if you are using an API for to fetch your data, and following the REST pattern.


#### Creating a custom DataAdapter

You will only need to do this if the default provided RestAdapter doesn't do what you need.

To get started create a new folder in your project root called `server/`. We keep things like the DataAdapter outside of the `app/` directory because they are server-side only and should never get sent to the Client.

Next create `data_adapter.js` in a new folder called `libs/`.

Overriding the __request__ method

```javascript
MyCustomAdapter.prototype.request = function(req, api, options, callback) {

  // Fetch the data using whatever method you like
  // ...

  // When you're done, send it back to Rendr
  callback(err, response, body);

  // Note: For a simple test, try sending back
  // callback(null, { statusCode: 200 }, { hello: 'world' });

};
```

That's technically all you have to do to build a custom data layer into your app.