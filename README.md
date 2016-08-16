# hyy-voting-frontend

## Prerequisites

- Install Node 0.12 with NVM
- `npm install -g grunt-cli bower yo generator-karma generator-angular`
- Install RVM
- After installing RVM, let RVM install Ruby version defined in .ruby-version (chdir out & back from project directory).
- `gem install bundler`

## Setup

~~~
bundle install
npm install
bower install
~~~

## Configuration

### Environment variables
When served locally with `grunt serve`:
- Edit `app/_environment.js` which contains environment specific configuration.

When being served from the API's `public/` folder:
- Set API's environment variables which begin with `FRONTEND_`, see API's README for details about setting API's environment variables in `.env`, `.env.example`.
- In Heroku, environment variables are set with `heroku config`. See API's README for further details.

## Development

Run `grunt serve` and access http://localhost:9000


### Accessing the local web server

- When the development API is running, you will have TWO frontends available: one served locally by `grunt serve` (localhost:9000) and the one which is served by Rails from `API/public` folder (localhost:3000). Use only either of them at the same time.
  * If you need to access localhost:3000 (ie. `API/public` served by Rails), prevent confusion by *not* running `grunt serve` at the same time. :)

- See `app/scripts/app.coffee` for application routes.

- RollbarError monitoring can be simulated with
    `window.onerror("TestRollbarError: testing window.onerror", window.location.href)`



## Generators

`yo angular:controller cat`

## Testing

Running `grunt test` will run the unit tests with karma.

## Deploy Frontend alongside with API

```bash
# Setup Frontend's git submodule (first time only)
git submodule add git@github.com:pre/hyy-voting-frontend-dist.git
```

```bash
# Update code in Frontend's git submodule (for each deploy)
(in Frontend) grunt build
(in Frontend) cd dist
(in Frontend) git status
(in Frontend) git add -A .
(in Frontend) git commit -m 'Theme of this deploy'
(in Frontend) git push

# Apply Frontend's new deploy in API
(in API) cd public
(in API) git checkout master
(in API) git pull
In API/public, `git log` should now display 'Theme of this deploy' as the newest commit.
```

```bash
# Commit 'Theme of this deploy' into API's git repository:
(in API) git add public && git commit -m 'deploy Theme of this deploy'
```
