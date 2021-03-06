# torim
Updated version of tor.nim from original of tor.nim from https://github.com/FedericoCeratto/nim-tor, please give credit to original author. This would not have been possible without them.

== Tor helper for Nim

### Features

* Wrap sockets to use the SOCKS proxy provided by Tor
* Wrap sockets to connect to Onion Services
* Authenticates against a local Tor daemon to create / list / delete traditional and ephemeral Onion Services
* Tested on Linux
* Basic functional tests
* Functions to look and work more like the net module
* Add your own functions for torim using the ProxySocket type 

### Usage

Install the library:

[source,bash]
----
nimble install torim
----

.Usage:
[source,nim]
----
import tor

# connect over Tor
var s = newProxySocket()
s.connect("1.1.1.1", 80.Port)
s.send("GET / HTTP/1.1\nHost: facebook.com\n\n")
discard s.recvLine(timeout=9000)
echo s.recv(200)

# connet to Onion Service
s = newProxySocket()
s.connect("facebookcorewwwi.onion", 80.Port)
s.send("GET / HTTP/1.1\nHost: facebook.com\n\n")
echo s.recvLine(timeout=9000)
----

See the tests/ dir for more usage examples.

To enable authentication with the Controller, install the libsodium wrapper and pass -d:usesodium

### Contributing

Testing and PRs are welcome.
