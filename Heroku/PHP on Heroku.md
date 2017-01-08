# Running PHP on Heroku

## Heroku in general

* Use multiple buildpacks
* Useful buildpacks:
  * https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-apt
  * https://github.com/kollegorna/heroku-buildpack-autossh
* If you need to manipulate enviornment variables, [do it in .profile](https://devcenter.heroku.com/articles/dynos#the-profile-file)
  * You can parse URLs using only bash with this: http://wp.vpalos.com/537/uri-parsing-using-bash-built-in-features/

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
* [Enable Dyno Metadata](https://devcenter.heroku.com/articles/dyno-metadata) and use that to determine if you should trust the front router
* Use [ReleasePhaseMigrationsBundle](https://github.com/fervo/ReleasePhaseMigrationsBundle) to do release phase migrations with advisory locks.

## Symfony on Heroku behind Cloudflare

* Be mindful that Cloudflare doesn't use X-Forwarded-Proto to report wheter it's using SSL. If you're using "Full SSL", it's not a problem, but if you're using "Flexible SSL" ([which you shouldn't](http://webmasters.stackexchange.com/a/67946)), where the connection between Heroku and Cloudflare is not encrypted, Symfony will consider your request unsecure.
