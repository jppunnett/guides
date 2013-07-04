# Lessons in CentOS 5
## Installing CentOS
## Setting up Apache
### Configure to listen on a different port
Normally, Apache listens for HTTP connects on port 80. That's great for public sites, but for internal sites you should listen on some other port, for security reasons.

To change the default port to, say, port 8888, edit Apache's configuration file, httpd.conf. To find out where httpd.conf resides, run `apachectl -V` and look at the values for `HTTPD_ROOT` and `SERVER_CONFIG_FILE`. Combine the values and you've found httpd.conf's location. In my case that's, /etc/httpd/conf/httpd.conf.

Once you've found httpd.conf, edit the file and find the `Listen` directive. It'll be set to port 80 (`Listen 80`). Change it to listen on port 8888 (`Listen 8888`) and restart Apache (`apachectl restart`).

If you haven't disabled the Welcome page, point your browser to http://yourhost:8888/ and you should see the default Apache Welcome page. (yourhost is the host running Apache.)

### Configure to not run as root
The reasons why you'd want to do this is described here, (http://httpd.apache.org/docs/2.2/misc/security_tips.html)

### Configure to start automatically on reboot.
TODO
### Create a site.
TODO
### Deploy files to site.
TODO
### Disable the Welcome Page
Once Apache starts successfully, disable the Welcome page. Edit the `/etc/httpd/conf.d/welcome.conf` file and comment out the `<LocationMatch>` element.
