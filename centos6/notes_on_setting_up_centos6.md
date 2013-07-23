# Notes on Setting up CentOS 6

I chose to install CentOS using the "Simple Server" install option. It sounded reasonably uncomplicated, and in retrospect, turned out to be a good choice because of the default security components it installed for me.

By default, CentOS does not configure the network interface card to use DHCP. I used [this article](http://blog.roozbehk.com/post/35277329160/rhel-centos-6-setup-networking) that describes how to configure the NIC to use DHCP.

Used `ntpdate mytimeserver` to sync the server with our internal time servers, where `mytimeserver` is the host name or IP of a time server. **TODO**: schedule to run every hour.

Added a non-admin user before doing anything else. As the root user:

    adduser auser
    passwd auser

**TODO** Configure auser to use sudo.

Used `yum` to update all installed packages. Because I go through a proxy server to reach the Internet, I had to set the `http_proxy` environment variable to refelect my proxy server's details.

    export http_proxy=http://uid:pwd@proxy_ip:proxy_port
    yum -y update

In the middle of the update, just for the hell of it, I rebooted the server. I was curious to see how `yum` would handle that scenario. When I logged back in, I tried running `yum -y update` to pick up where I left off and yum told me to use `yum-complete-transaction` instead. So I did and all went well; the update picked up from where it left off.

Installed nmap: `yum -y install nmap`. (Just because I know I'll need it at some point.)

Installed Apache Web server: `yum -y install httpd`

Tried to get to the default Apache Welcome page but the browser timed out. Check to see if at least something was listening on port 80 (indeed there was):

    netstat -tan | grep 80

After chatting with local guru, used `sestatus` to check if Security Enhanced Linux (SELinux) was in enforcing mode. You should learn more about SELinux [here](http://wiki.centos.org/HowTos/SELinux). In my case SELinux was running in enforcing mode. I decided to disable it until I could learn more about it.

After disabling SELinux, I still couldn't get to the Apache Welcome page. I pulled up [Wireshark](http://www.wireshark.org/) and discovered that the server was returning with "Destination unreachable (Host administratively prohibited)". I suspected a firewall on the CentOS server was dropping the packets. I know nothing about Linux firewals, so did some reading.

On Linux, firewalls are usually implemented using the iptables application. Since iptables was new to me, I wanted to first confirm that it was indeed a firewall issue before going further and decided to temporarily turn off the firewall:

    /etc/init.d/iptables save
    /etc/init.d/iptables stop

Then I pointed my browser to http://myserver/ and got the Apache Welcome page. Once I figured out that it was the firewall, I restarted it:

    /etc/init.d/iptables start

To allow HTTP traffic on the default port 80 to get through the firewall, I made the following changes:

    iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT

In near-English, this says, "At rule 4 in the filter table's INPUT chain, insert a new rule to accept TCP traffic on port 80." In English, it says, "Allow traffic on port 80."

Now, with the firewall configured to accept HTTP traffic, I was able to navigate to the Apache Welcome screen. (To learn how to configure your Linux firewall, look no further than `man iptables`. It's not all that difficult.)

So that the new firewall rule is applied on a reboot, I used the following command to save the rules:

    /etc/init.d/iptables save
