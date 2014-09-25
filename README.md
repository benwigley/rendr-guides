render-docs
===========

> "...very unoffical docs..."

For Version 0.5.0

This repo contains some very unoffical docs to help you get started using Rendr. Seeing as I am learning Rendr at present it makes sense to document my journey so others can avoid the initial learning curve I am currently going through.


## Scaffolding

### Folders

Files in the `app/` directory are shared between the client and server by default. If you need server specific files like a global layout, or a custom lib, be sure to use the convention of prepending `__` to the file name.

- `app/` - Contains shared files.
  - `lib/`
    - `config.js`
    - `handlebars/`
      - `helpers.js`
  - `models/` - Models/Collection have the same structure as a regular Backbone app
    - `base.js`
  - `collections/`
    - `base.js`
  - `views/`
    - `base.js`
  - `templates/` - Templates match directly to view files, you can also use the handy built-in Handlebars helper `{{partial 'path/to/template'}}` instead of creating Handlbars partials.


- `server/` - Server only files.
  - `lib/`
    - `data_adapter.js` - A customm DataAdapter (optional) See [DataAdapter](data_adapter.md)



## The Rendr npm module

    npm install rendr --save

The rendr module handles all of the Abrstractions between the Client and Server, which is why we can safely package up all the js files in `app/` and send them to the client.