ngixctl - script to control the functioning of Nginx server
===========================================================

nginxctl - a lightweight clone of apachectl script. It act as a SysV init script, 
taking simple one-word arguments like start, restart, and stop, and translating them into 
appropriate signals to nginx.

Features
--------

* Not passthru mode.
* apachectl-like status.
* configtest

Configuration
-------------

Edit variables inside nginxctl script.

```shell
PIDFILE=/var/run/nginx.pid      # pidfile location

NGINX=/usr/local/sbin/nginx     # nginx binary location

LYNX="lynx -dump"               # Browser for text dump

STATUSURL="http://127.0.0.1:999/stub_status" # URL for nginx statistic
```

For statistic add some lines into nginx.conf. For our example:
```nginx
    server {
        listen          127.0.0.1:999;
        server_name     localhost;
        access_log      off;
        location = /stub_status {
        stub_status     on;
        allow           127.0.0.0/8;
        deny            all;
    }

```

Usage
-----

```
nginxctl (start|stop|restart|fullstatus|status|graceful|configtest|help)
 
start      - start nginx 
stop       - stop nginx 
restart    - restart nginx if running by sending a SIGHUP or start if. 
             not running 
fullstatus - dump a full status screen; requires lynx and 'stub_status on;' directive 
status     - dump a short status screen; requires lynx and 'stub_status on;' directive 
graceful   - do a graceful restart by sending a SIGHUP or start if not running 
configtest - do a configuration syntax test 
help       - this screen 
```

The exit codes returned are:
* 0 - operation completed successfully
* 1 - 
* 2 - usage error
* 3 - nginx could not be started
* 4 - nginx could not be stopped
* 5 - nginx could not be started during a restart
* 6 - nginx could not be restarted during a restart
* 7 - nginx could not be restarted during a graceful restart
* 8 - configuration syntax error

TODO
----

1. Implement Upgrading Executable on the Fly function.
2. Implement reopen logs function.
3. Alter implementation restart command. Do it hardly.
4. Implement graceful stop command.

Applied
-------

Used and tested on the resources of 
* PeterHost.ru hosting
* [DiPHOST](http://diphost.ru/)
* eFind.ru

--
[![LICENSE WTFPL](wtfpl-badge-1.png)](LICENSE)

