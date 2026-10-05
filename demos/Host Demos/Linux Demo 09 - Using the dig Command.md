# Linux Demo 9

## Using the *dig* command to display DNS information

1. Connect and login to one of the dual-stack Linux nodes.
2. At the prompt, run the command `dig` without any arguments and observe the output. 

```console
user@ubuntu-24:~$ dig @ns1.hexabuild.net

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> @ns1.hexabuild.net
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51954
;; flags: qr rd ra; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 27

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1220
; COOKIE: fc89632300b5134a010000006963ddcd3bffc32e797dcacb (good)
;; QUESTION SECTION:
;.				IN	NS

;; ANSWER SECTION:
.			515610	IN	NS	i.root-servers.net.
.			515610	IN	NS	j.root-servers.net.
.			515610	IN	NS	m.root-servers.net.
.			515610	IN	NS	h.root-servers.net.
.			515610	IN	NS	g.root-servers.net.
.			515610	IN	NS	f.root-servers.net.
.			515610	IN	NS	a.root-servers.net.
.			515610	IN	NS	b.root-servers.net.
.			515610	IN	NS	c.root-servers.net.
.			515610	IN	NS	d.root-servers.net.
.			515610	IN	NS	e.root-servers.net.
.			515610	IN	NS	l.root-servers.net.
.			515610	IN	NS	k.root-servers.net.

;; ADDITIONAL SECTION:
a.root-servers.net.	515610	IN	AAAA	2001:503:ba3e::2:30
b.root-servers.net.	515610	IN	AAAA	2801:1b8:10::b
c.root-servers.net.	515610	IN	AAAA	2001:500:2::c
d.root-servers.net.	515610	IN	AAAA	2001:500:2d::d
e.root-servers.net.	515610	IN	AAAA	2001:500:a8::e
f.root-servers.net.	515610	IN	AAAA	2001:500:2f::f
g.root-servers.net.	515610	IN	AAAA	2001:500:12::d0d
h.root-servers.net.	515610	IN	AAAA	2001:500:1::53
i.root-servers.net.	515610	IN	AAAA	2001:7fe::53
j.root-servers.net.	515610	IN	AAAA	2001:503:c27::2:30
k.root-servers.net.	515610	IN	AAAA	2001:7fd::1
l.root-servers.net.	515610	IN	AAAA	2001:500:9f::42
m.root-servers.net.	515610	IN	AAAA	2001:dc3::35
a.root-servers.net.	515610	IN	A	198.41.0.4
b.root-servers.net.	515610	IN	A	170.247.170.2
c.root-servers.net.	515610	IN	A	192.33.4.12
d.root-servers.net.	515610	IN	A	199.7.91.13
e.root-servers.net.	515610	IN	A	192.203.230.10
f.root-servers.net.	515610	IN	A	192.5.5.241
g.root-servers.net.	515610	IN	A	192.112.36.4
h.root-servers.net.	515610	IN	A	198.97.190.53
i.root-servers.net.	515610	IN	A	192.36.148.17
j.root-servers.net.	515610	IN	A	192.58.128.30
k.root-servers.net.	515610	IN	A	193.0.14.129
l.root-servers.net.	515610	IN	A	199.7.83.42
m.root-servers.net.	515610	IN	A	202.12.27.33

;; Query time: 3 msec
;; SERVER: 3fff:1d00:3001:1d32::53#53(ns1.hexabuild.net) (UDP)
;; WHEN: Sun Jan 11 17:28:46 UTC 2026
;; MSG SIZE  rcvd: 851

user@ubuntu-24:~$
```

2. Note the output reflects the DNS server being queried (**@ns1.hexabuild.net** - which is also shown near the bottom in the *SERVER* field, along with the IPv4 or IPv6 address the domain name is mapped to).
   
   The *status* field indicates **NOERROR** meaning the DNS server received a valid answer. Had the query failed, the status error code would have shown either **SERVFAIL** (typically when no server could be reached) or **NXDOMAIN** (for when the server could be reached but the domain queried for does not exist).
   
   Also of note are the results shown in the *flags* field: **qr**, **rd**, and **ra**, which mean respectively **query response**, **recursion desired**, and **recursion available**. Finally, because no domain was specified in the original dig request, the *answer section* displays the root nameservers along with their associated IPv6 and IPv4 addresses.

3. Now use the `dig` command to query for records within the local hexabuild.net domain. Including the query type desired will narrow the results. For example, to find the IPv6 address associated with the nameserver **infoblox.hexabuild.net** try: `dig AAAA infoblox.hexabuild.net`

```console
user@ubuntu-24:~$ dig AAAA infoblox.hexabuild.net

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> AAAA infoblox.hexabuild.net
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16378
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;infoblox.hexabuild.net.		IN	AAAA

;; ANSWER SECTION:
infoblox.hexabuild.net.	6847	IN	AAAA	3fff:1d00:3001:1d32::53

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sun Jan 11 18:16:37 UTC 2026
;; MSG SIZE  rcvd: 79
```
4. To see if the IPv6 address maps back to the domain name use the `-x` argument with dig: `dig -x 3fff:1d00:3001:1d32::53`. Note the response pointing to the PTR records in the ip6.arpa reverse domain mapped to the IPv6 prefix.

```console
user@ubuntu-24:~$ dig -x 3fff:1d00:3001:1d32::53

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 3fff:1d00:3001:1d32::53
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 65365
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;3.5.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.3.d.1.1.0.0.3.0.0.d.1.f.f.f.3.ip6.arpa. IN PTR

;; ANSWER SECTION:
3.5.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.3.d.1.1.0.0.3.0.0.d.1.f.f.f.3.ip6.arpa. 28800	IN PTR infoblox.hexabuild.net.
3.5.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.3.d.1.1.0.0.3.0.0.d.1.f.f.f.3.ip6.arpa. 28800	IN PTR ns1.hexabuild.net.

;; Query time: 2 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sun Jan 11 18:18:28 UTC 2026
;; MSG SIZE  rcvd: 155
```

4. Run these additional command examples of `dig` and interpret the results:
   
    `dig A www.hexabuild.net`

    `dig A www.hexabuild.net @ns1.hexabuild.net`
   
    `dig A www.hexabuild.net @3fff:1d00:3001:1d32::53`

    `dig AAAA www.hexabuild.net @3fff:1d00:3001:1d32::53`

    `dig AAAA ipv6-only.hexabuild.net @192.168.50.53`

    `dig A www.hexabuild.net @3fff:1d00:3001:1d32::53`

    `dig A www.hexabuild.net @1.1.1.1`

    `dig AAAA github.com`
