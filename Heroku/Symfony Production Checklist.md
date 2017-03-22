* Running at least 2 production grade dynos
* All addons are production grade
* Automatic backups have been scheduled for databases et c.
* Logplex drain has been set up (e.g. by using Papertrail)
* Symfony logs to console in prod
* SSL has been set up
* Symfony/PHP is not using file based sessions (instead store sessions in e.g. Redis or a database)
* The [Heroku Router is trusted](https://devcenter.heroku.com/articles/getting-started-with-symfony#trusting-the-load-balancer) by Symfony
* [APC for Doctrine metadata](https://devcenter.heroku.com/articles/getting-started-with-symfony#recommended-extensions) is used
