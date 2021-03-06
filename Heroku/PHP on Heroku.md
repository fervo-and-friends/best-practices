# Running PHP on Heroku

## Heroku in general

* Use multiple buildpacks
* Useful buildpacks:
  * https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-apt
  * https://github.com/kollegorna/heroku-buildpack-autossh
* If you need to manipulate (rename, split etc.) enviornment variables, [do it in .profile](https://devcenter.heroku.com/articles/dynos#the-profile-file)
  * You can parse URLs using only bash with this: http://wp.vpalos.com/537/uri-parsing-using-bash-built-in-features/
* Remember that you can often attach addons to multiple apps
* Remember that you can (using heroku-cli) create addons with other names, or rename addons

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
* Use the `DYNO` environment variable to determine if your app i running on Heroku, and thus should trust the front router.
* Use [ReleasePhaseMigrationsBundle](https://github.com/fervo/ReleasePhaseMigrationsBundle) to do release phase migrations with advisory locks.

## Symfony on Heroku behind Cloudflare

* Be mindful that Cloudflare doesn't use X-Forwarded-Proto to report wheter it's using SSL. If you're using "Full SSL", it's not a problem, but if you're using "Flexible SSL" ([which you shouldn't](http://webmasters.stackexchange.com/a/67946)), where the connection between Heroku and Cloudflare is not encrypted, Symfony will consider your request insecure.

## Heroku CI

* PHPUnit removed support for TAP in 6.0. [gh640/phpunit-tap](https://github.com/gh640/phpunit-tap) adds it back.
* PHPSpec has support for TAP built in.
* Behat doesn't come with TAP support, use [rdey/BehatTapFormatter](https://github.com/rdey/BehatTapFormatter) to add it.
* If you use multiple testing tools, you should write a shell script to run as your test script. If so, using `set -e` in the script may be useful. `set -e` means that if any of the lines in the script fail (i.e. return a non-zero exit code) the entire script will immediately abort with a non-zero exit code (triggering Heroku CI to mark the test run as failed).
