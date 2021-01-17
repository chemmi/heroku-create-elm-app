# Heroku create-elm-app

This is a minimal example for deploying an elm app with [Heroku](https://www.herokucdn.com/deploy/button.svg) using the fantastic [create-elm-app](https://github.com/halfzebra/create-elm-app).

It uses the [nodejs buildpack](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-nodejs) to provide `create-elm-app`.
Installation of elm and building of the app is done using the [inline buildpack](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-inline).
The [static buildpack](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-static) is used to provide the app after building.

## Deployment using Heroku Button

Just use the following button to deploy this example on Heroku.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Deployment using Heroku CLI

Follow these steps to deploy this example on Heroku via Heroku CLI.

Clone this repository and add Heroku settings.

``` bash
# Clone and browse repo
git clone https://github.com/chemmi/heroku-create-elm-app
cd heroku-create-elm-app

# Create heroku app
heroku create
# heroku create my-fancy-app-name

# Add buidpacks
heroku buildpacks:add https://github.com/heroku/heroku-buildpack-nodejs.git
heroku buildpacks:add https://github.com/heroku/heroku-buildpack-inline.git
heroku buildpacks:add https://github.com/heroku/heroku-buildpack-static.git
```

Push to Heroku to deploy the app.

``` bash
git push heroku master
```

## Usage in your own elm-app

This repo can be used as boilerplate for other projects.
Just copy some files to your local project and follow the deployment steps.

``` bash
cp -r app.json package.json static.json bin /path/to/your/elm-app
```

You may want to update the fields `name`, `description` and `repository` in your copy of `app.json`.

## Buildpack Files

__app.json__ is mainly used for config-as-code buildpacks and the deployment button.

__package.json__ is used for the nodejs buildpack to provide `create-elm-app` and node for subsequent build steps.

__bin/*__ is used for the inline buildpack.
_detect_ and _release_ are more or less dummies.
_compile_ does install elm and builds the application using `elm-app build`.

__static.json__ is used for the static buildpack to provide the application after building.

## Kudos

Thanks [halfzebra](https://github.com/halfzebra/create-elm-app) for [create-elm-app](https://github.com/halfzebra/create-elm-app)!

A different approach for deployment using Heroku via local build of the app is done by [MainShayne233](https://mainshayne233.github.io/2019-11-23-deploy-create-elm-app-to-heroku/).

Boilerplates for the use of the inline buildpack are taken from [JetThoughts](https://jtway.co/deploying-subdirectory-projects-to-heroku-f31ed65f3f2).

The compile-part is mostly adapted from [srid's elm buildpack](https://github.com/srid/heroku-buildpack-elm).

## Todos

- [ ] Add caching (binary, elm-stuff, ...)
- [ ] Add support for different elm versions (mind differet release formats!)
