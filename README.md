
THIS REPOSITORY DOES NOT EVEN HAVE ANY CODE YET.

ubus-https-forwarder is a planned daemon that will receive ubus requests locally and forward them to a ubus instance on a remote host by accessing the remote host's uhttpd-mod-ubus via https.

This will allow a ubus instance on a single host to manage other hosts securely through a unified luci2 GUI. sudo mesh uses this in conjunction with notdhcpserver and nothdcpclient in a setup where a single indoor router has e.g. a street-facing nanostation and a rooftop nanobridge connected over ethernet, but the nanostation and nanobridge are simply operating in bridge mode and are managable through the GUI of the indoor router. In effect the user can pretend that the nanostation and nanobridge are simply extra wifi interfaces on the indoor node.

# How to implement

We should implement as a ubus server daemon written in C that receives RPC requests destined for a remote host and forwards them using https. There is a nice libubus server example in the examples directory in the [ubus git repo](http://nbd.name/gitweb.cgi?p=luci2/ubus.git;a=tree) that can be used as basis for the daemon. We don't have to implement anything special to receive ubus requests over http since uhttpd-mod-ubus already takes care of that, but we need an https client library in order to forward the request to a remote uhttpd-mod-ubus instance. The OpenWRT Barrier Breaker repo includes [libcurl 4.3 compiled with polarssl support](https://downloads.openwrt.org/barrier_breaker/14.07/ar71xx/generic/packages/base/libcurl_7.38.0-1_ar71xx.ipk) and of course the package depends on polarssl which is also in the repo.

# License

This project is licensed under the GNU General Public License v3.
