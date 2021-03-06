# Pliny

Opinionated template Sinatra app for writing excellent APIs in Ruby.

It bundles some of the patterns we like to develop these apps:

- Config: `ENV` wrapper for explicit defining what config vars are mandatory and optional
- Endpoints: the Sinatra equivalent of a Rails Controller
- Initializers: tiny files to configure libraries/etc (equivalent of Rails)
- Mediators: plain ruby classes to manipulate models
- Models: very thin wrappers around the database

And gems/helpers to tie these together and support operations:

- [CORS middleware](vendor/pliny/lib/pliny/middleware/cors.rb) to allow JS developers to consume your API
- [Honeybadger](https://www.honeybadger.io/) for tracking exceptions
- [Log helper](vendor/pliny/test/log_test.rb) that logs in [data format](https://www.youtube.com/watch?v=rpmc-wHFUBs) [to stdout](https://adam.heroku.com/past/2011/4/1/logs_are_streams_not_files)
- [Minitest](https://github.com/seattlerb/minitest) for lean and fast testing
- [Puma](http://puma.io/) as the web server, [configured for optimal performance on Heroku](config/puma.rb)
- [Rack-test](https://github.com/brynary/rack-test) to test the API endpoints
- [Request IDs](vendor/pliny/lib/pliny/middleware/request_id.rb)
- [RequestStore](http://brandur.org/antipatterns), thread safe option to store data with the current request
- [RR](https://github.com/rr/rr/blob/master/doc/03_api_overview.md) for amazing mocks and stubs
- [Sequel](http://sequel.jeremyevans.net/) for ORM
- [Sequel-PG](https://github.com/jeremyevans/sequel_pg) because we don't like mysql
- [Versioning](vendor/pliny/lib/pliny/middleware/versioning.rb) to allow versioning your API in the HTTP Accept header

## Getting started

Clone this repo, then:

```bash
$ bin/setup
$ foreman start web
```

There are some generators to help you get started:

```bash
$ bundle exec pliny-generate model artist
created model file ./lib/models/artist.rb
created migration ./db/migrate/1395873224_create_artist.rb
created test ./test/models/artist_test.rb

$ bundle exec pliny-generate mediator artists/creator
created base mediator ./lib/mediators/base.rb
created mediator file ./lib/mediators/artists/creator.rb
created test ./test/mediators/artists/creator_test.rb

$ bundle exec pliny-generate endpoint artists
created endpoint file ./lib/endpoints/artists.rb
add the following to lib/app/main:
  use App::Main::Artists
created test ./test/endpoints/artists_test.rb

$ bundle exec pliny-generate migration fix_something
created migration ./db/migrate/1395873228_fix_something.rb

$ bundle exec pliny-generate schema artists
created schema file ./docs/schema/schemata/artists.json
```

To test your application:

```bash
createdb pliny-test
rake
```

Or to run a single test suite:

```bash
ruby -Itest test/acceptance/artists_test.rb
```

## Meta

Created by Brandur Leach and Pedro Belo.
