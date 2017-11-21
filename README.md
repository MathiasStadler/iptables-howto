# iptables-howto


# version 
- ```iptables --version```

# Sources
- [iptables handbuch](https://de.m.wikibooks.org/wiki/Linux-Praxisbuch:_Linux-Firewall_mit_IP-Tables)
- [HEISE article](https://www.heise.de/security/artikel/Aufgebohrt-271130.html)
- [desc systemtap](https://serverfault.com/questions/192893/how-i-can-identify-which-process-is-making-udp-traffic-on-linux)
- [network with systemtap](https://sourceware.org/systemtap/wiki/WSNetTop)


# extension
[libxt_LOG](https://fossies.org/linux/iptables/extensions/libxt_LOG.man)


#located iptables 
- ```/sbin/iptables```
- ```which iptables```
- ```ls -lh /sbin/iptables`
/sbin/iptables -> xtables-multi ```

- Attention very often a link to ```/sbin/xtables-multi```

xtables-multi - xtables multi-link binary for netfilter's iptables and
       ip6tables


# dump/see running config

- iptables-save — dump iptables rules to stdout
    - all tables

- ```sudo iptables-save```  

# Ping of Death
- ```iptables -A FORWARD -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT  ```

# flow of iptables rules
- [packet flow](https://de.wikipedia.org/wiki/Iptables#/media/File:Netfilter-packet-flow.svg)
- [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)


# debug
- debug only with packet limitation
- don't destroy your system 


- ```sudo iptables -I FORWARD 1 -m limit -j LOG --log-level 4 --log-prefix "FORWARD => " ```

-```sudo iptables -I OUTPUT 1 -m limit -j LOG --log-level 1 --log-prefix "OUTPUT => "```

-```sudo iptables -L OUTPUT  -n --line-number```
-```sudo iptables -D OUTPUT  1```


- List of debug rules
- ```sudo iptables -L FORWARD  -n --line-number```

- delete Log rule 
- ```sudo iptables -D FORWARD  <Line Number>```




# deact ping


# deact portscanner
- TODO test
- TODO desc

- ```iptables -A FORWARD -p tcp --tcp-flags ALL NONE -m limit --limit 1/h -j ACCEPT ```
- ``` iptables -A FORWARD -p tcp --tcp-flags ALL ALL -m limit --limit 1/h -j ACCEPT ```


# Unsorted
- cat /proc/net/tcp
- netstat 
- https://www.sysdig.org/

# nethogs show trffic 
- https://sourceforge.net/projects/nethogs/
- see github version too


# sysdiag Linux Diagnostic Tools


#  ulogd  is  a  logging  daemon that reads event messages coming from the
       Netfilter connection tracking, the Netfilter packet  logging  subsystem
       and from the Netfilter accounting subsystem. You have to enable support
       for connection tracking event delivery; ctnetlink and the NFLOG  target
       in  your  Linux  kernel  2.6.x  or  load  their respective modules. The
       deprecated ULOG target (which has been superseded  by  NFLOG)  is  also
       supported.

       The received messages can be logged into files or into a mySQL, sqlite3
       or PostgreSQL database. IPFIX and Graphite output are also supported.

# conntrack-logger
- [Link](https://github.com/mk-fg/conntrack-logger)

# netstat-monitor
- [Link](https://github.com/stalexan/netstat-monitor/)