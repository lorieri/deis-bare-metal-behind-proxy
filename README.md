# Deis Behind Proxy Bare Metal

## Notes:

 * tested on v0.15.0
 * python boto ignores no_proxy, database and registry can't use proxy, fails creating ceph bucket
 * changed units to use public ip
 * using docker exec to inject proxy into the builder slugs' Dockerfiles
 * _etc_environment is /etc/environment
 * moved  /run/deis/bin to /etc/deis/bin (I know...) so reboots with no user-data are easier

## Tips:

 * most confd parser erros are units waiting other units to activate
 * if you run the user-data manually, do not forget to enable fleet.socket on all host, it is used by the controller
  * `systemctl enable fleet.socket`
 * if you clone a host, change the file /etc/machine-id
 * for java buildpack, if you put a settings.xml with proxy settings at your project root the slugbuilder will use it

## How:

 * install CoreOs
 * install deisctl, before 'deis install platform'
  * copy _etc_environment to all hosts on /etc/environment
  * copy units to your ~/.deis/units/
 * run: deisctl install platform

## Tested with
 * https://github.com/deis/example-java-jetty.git (using a custom settings.xml)
 * https://github.com/deis/example-nodejs-express
 * https://github.com/deis/example-ruby-sinatra.git
 * https://github.com/heroku/php-getting-started.git
 * https://github.com/heroku/python-getting-started.git
	
		
