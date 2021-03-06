# Check Contrail

## Links

* Upstream [github](https://github.com/sbadia/contrail-nagios/) URL.
 * `pandoc -f markdown -t mediawiki -s README.md -o README.mediawiki`

## Requirements

* ruby

## Checks

### Check\_vrouter\_xmpp

Check vrouter's xmpp connection with controller peers

### Arguments

* `-H, --host`: Hostname to run on (default: localhost)
* `-p, --port`: Vrouter API port (default: 8085)
* `-c, --cfg-ctrl`: Check only cfg-controller (default: false)
* `-m, --mcast-ctrl`: Check only mcast-controller (default: false)
* `-i, --ip-ctrl(s)`: Check this controller IPs (default: false)
* `-h, --help`: Display this help message

### Usage

* Check localhost vrouter on port 8085 (default)

>     check_vrouter_xmpp
>     UNKNOWN: Could not connect to localhost:8085 (please check)

* Check only the xmpp connection with `10.10.0.58` and `10.10.0.57` peer controller IP

>     check_vrouter_xmpp -H tt.net -i 10.10.0.58,10.10.0.57
>     OK: Peer with 10.10.0.58 is Established (last state OpenSent at 2014-Jun-22 08:10:48.772736)
>     OK: Peer with 10.10.0.57 is Established (last state OpenSent at 2014-Jun-25 20:08:29.642435)

* Check only the xmpp connection with the config controller peer

>     check_vrouter_xmpp -H tt.net -c
>     OK: Peer with 10.10.0.57 is Established (last state OpenSent at 2014-Jun-22 08:09:30.065507)

* Check only the xmpp connection with the multicast controller peer

>     check_vrouter_xmpp -H tt.net -m
>     OK: Peer with 10.10.0.57 is Established (last state OpenSent at 2014-Jun-22 08:09:30.065507)

* Check all xmpp connection peers (warning if one session is down, and critical if all are down)

>     check_vrouter_xmpp -H tt.net
>     OK: Peer with 10.10.0.57 is Established (last state OpenSent at 2014-Jun-22 08:09:30.065507)
>     OK: Peer with 10.10.0.58 is Established (last state OpenSent at 2014-Jun-22 08:10:48.772736)

### Check\_vrouter\_agent

Check vrouter's agent state

### Arguments

* `-H, --host`: Hostname to run on (default: localhost)
* `-p, --port`: Vrouter API port (default: 8085)
* `-h, --help`: Display this help message

### Usage

* Check the state of the vrouter agent

>     check_vrouter_agent -H tt.net
>     OK: tt.net in «InitDone» state

### Check\_bgp\_neighbor

Check controller's BGP neighbor

### Arguments

* `-H, --host`: Hostname to run on (default: localhost)
* `-p, --port`: Controller API port (default: 8083)
* `-a, --peer-asn(s)`: Check only this peer ASN (default: false)
* `-i, --peer-ip(s)`: Check only this peer IP (default: false)
* `-h, --help`: Display this help message

### Usage

* Check a specific ASN

>     check_bgp_neighbor -H a.tt.net -a 60940 -v
>     OK: Peer with 10.5.250.9 AS60940 (BGP) is Established

* Check two specific ASN

>     check_bgp_neighbor -H a.tt.net -a 60940,64516 -v
>     OK: Peer with 10.5.250.9 AS60940 (BGP) is Established
>     OK: Peer with 10.10.0.58 AS64516 (BGP) is Established

* Check a specific peer

>     check_bgp_neighbor -H a.tt.net -i 10.5.250.9 -v
>     OK: Peer with 10.5.250.9 AS60940 (BGP) is Established

* Check a list of specific peer

>     check_bgp_neighbor -H a.tt.net -i 10.5.250.9,10.10.0.58 -v
>     OK: Peer with 10.5.250.9 AS60940 (BGP) is Established
>     OK: Peer with 10.10.0.58 AS64516 (BGP) is Established

* Check all controller sessions (warning if one session is down, and critical if all are down)

>     check_bgp_neighbor -H a.tt.net -v
>     OK: Peer with 10.5.250.9 AS60940 (BGP) is Established
>     OK: Peer with 10.10.0.58 AS64516 (BGP) is Established
>     OK: Peer with 10.10.1.57 AS0 (XMPP) is Established
>     OK: Peer with 10.10.1.55 AS0 (XMPP) is Established
>     OK: Peer with 10.10.1.56 AS0 (XMPP) is Established

* Check localhost on port 8083

>     check_bgp_neighbor
>     UNKNOWN: Could not connect to localhost:8083 (please check)
