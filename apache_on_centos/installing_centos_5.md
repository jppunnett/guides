# Apache On CentOS 5
## Installing CentOS
TODO
## Install & Configure Apache

### Install Apache
The easiest way to install Apache on CentOS 5, is to use yum. You *should* learn more about yum so go visit [yum](http://yum.baseurl.org/). Do get you going quickely, though, here's the command to install Apache.

	yum install httpd

On my system, this installs Apache version 2.2.3. This is not the latest version of Apache, but you can install the latest version if you want. I'll cover that in another guide TODO.

### Configure to listen on a different port
Normally, Apache listens for HTTP connects on port 80. That's great for public sites, but for internal sites you should listen on some other port, for security reasons.

To change the default port to, say, port 8888, edit Apache's configuration file, httpd.conf. To find out where httpd.conf resides, run `apachectl -V` and look at the values for `HTTPD_ROOT` and `SERVER_CONFIG_FILE`. Combine the values and you've found httpd.conf's location. In my case that's, /etc/httpd/conf/httpd.conf.

Once you've found httpd.conf, edit the file and find the `Listen` directive. It'll be set to port 80 (`Listen 80`). Change it to listen on port 8888 (`Listen 8888`) and restart Apache (`apachectl restart`).

If you haven't disabled the Welcome page, point your browser to http://yourhost:8888/ and you should see the default Apache Welcome page. (yourhost is the host running Apache.)

### Configure to not run as root
When you start Apache (`apachectl start`), you're actually starting one or more `httpd` processes. The first instance of `httpd` starts as the root user, but the remaining instances start under a different user. By default, this differnt user is set to "apache". For example, in my httpd.conf file, I find,

	User apache
	Group apache

This says that the httpd process that Apache uses to handle requests, should run as the user "apache".

I suggest you leave the User directive set to the default. If you do want to change it, simply update the User and Group directives. Please read about Apache's User directive before you change it, though. [User Directive](http://httpd.apache.org/docs/2.2/mod/mpm_common.html#user)

### Create a site.
TODO

### Deploy files to site.
TODO

### Disable the Welcome Page
Once Apache starts successfully, disable the Welcome page. Edit the `/etc/httpd/conf.d/welcome.conf` file and comment out the `<LocationMatch>` element.


### Configure to start automatically on reboot.
TODO
