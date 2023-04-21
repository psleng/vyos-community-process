# VCP5: WAN load-blancing rework

Up to VyOS 1.3 there is a dedicated CLI tree `load-balancing wan` used to
aggregate multiple WAN links for either load-sharing or backup.

When reworking this implementation for VyOS 1.4 we should rethink the CLI design
and also the concept behind it.

## Current status

load-balancing relies on a dedicated "daemon" written in C that directly interacts
with iptables/nftables and the routing. It also comes with a duplicate copy of the
NAT CLI nodes only used for WAN load balancing which is quiet redundant.

## Design Goals for a redesign

* Make use of the common `nat source` CLI tree
* Make use of failover-route implementation
* Get rid of any additional daemon monitoring those routes
