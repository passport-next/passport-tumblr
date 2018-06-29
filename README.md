# Passport-Tumblr

[![Build Status](https://travis-ci.org/passport-next/passport-tumblr.svg?branch=master)](https://travis-ci.org/passport-next/passport-tumblr)
[![Coverage Status](https://coveralls.io/repos/github/passport-next/passport-tumblr/badge.svg?branch=master)](https://coveralls.io/github/passport-next/passport-tumblr?branch=master)
[![Maintainability](https://api.codeclimate.com/v1/badges/cfd3cf93fcbb9b44231e/maintainability)](https://codeclimate.com/github/passport-next/passport-tumblr/maintainability)
[![Dependencies](https://david-dm.org/passport-next/passport-tumblr.png)](https://david-dm.org/passport-next/passport-tumblr)
<!--[![SAST](https://gitlab.com/passport-next/passport-tumblr/badges/master/build.svg)](https://gitlab.com/passport-next/passport-tumblr/badges/master/build.svg)-->

[Passport](http://passportjs.org/) strategy for authenticating with [Tumblr](https://www.tumblr.com/)
using the OAuth 1.0a API.

This module lets you authenticate using Tumblr in your Node.js applications.
By plugging into Passport, Tumblr authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install @passport-next/passport-tumblr

## Usage

#### Configure Strategy

The Tumblr authentication strategy authenticates users using a Tumblr account
and OAuth tokens.  The strategy requires a `verify` callback, which accepts
these credentials and calls `done` providing a user, as well as `options`
specifying a consumer key, consumer secret, and callback URL.

    passport.use(new TumblrStrategy({
        consumerKey: TUMBLR_CONSUMER_KEY,
        consumerSecret: TUMBLR_SECRET_KEY,
        callbackURL: "http://127.0.0.1:3000/auth/tumblr/callback"
      },
      function(token, tokenSecret, profile, done) {
        User.findOrCreate({ tumblrId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'tumblr'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/tumblr',
      passport.authenticate('tumblr'));
    
    app.get('/auth/tumblr/callback', 
      passport.authenticate('tumblr', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/jaredhanson/passport-tumblr/tree/master/examples/login).

## Tests

    $ npm install --dev
    $ make test

