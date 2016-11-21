# Running PHP on Heroku

## Heroku in general

* Use multiple buildpacks
* Useful buildpacks:
  * https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-apt
  * https://github.com/kollegorna/heroku-buildpack-autossh

## PHP on Heroku in general

* Read this: https://devcenter.heroku.com/articles/deploying-php
* Use a .user.ini
  * Disable phpinfo
  * Set your timezone, maybe
* If you need private Github packages: https://devcenter.heroku.com/articles/php-support#custom-github-oauth-tokens
  * That entire page is full of useful info
* Get your session handler in order
* Use Bernard and Simplebus Asynchronous for your background worker needs.

## Symfony on Heroku in particular

* Read this: https://devcenter.heroku.com/articles/getting-started-with-symfony#best-practices
* Read this: https://blog.fervo.se/blog/2016/03/22/symfony-on-heroku/
* Use Symfony >=3.2 which has native support for environment variables
* Enable Dyno Metadata and use that to determine if you should trust the front router
