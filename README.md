![GitHub release (latest SemVer including pre-releases)](https://img.shields.io/github/v/release/nebula-chat-fork/clients?include_prereleases&label=latest-release&sort=semver)
[![License](https://img.shields.io/github/license/nebula-chat-fork/clients.svg)](https://github.com/nebula-chat-fork/clients/blob/master/LICENSE)

# clients
> [Telegram](https://telegram.org) clients patch by NebulaChat

All client's signIn (signOut) default verify code is *12345*

[Android client for NebulaChat](Telegram-Android) 

[FOSS client for NebulaChat](Telegram-FOSS)

[iOS client for NebulaChat](Telegram-iOS)

[tdesktop for NebulaChat](tdesktop)

**Supported systems:**

* GNU/Linux - [![Build Status](https://github.com/nebula-chat-fork/clients/workflows/tdesktop_linux./badge.svg)](https://github.com/nebula-chat-fork/clients/actions)
* A built image of i2pgram desktop client for Ubuntu 14.04+: http://upvum2vlbkljuvphrremwwlhmypl3te7dr2gyrsw4oady3brhc7q.b32.i2p/

**Currently unsupported systems:**

* TBD Windows - Build status
* TBD Mac OS X - Build Status
* TBD CentOS / Fedora / Mageia - Build Status
* TBD Docker image - Build Status
* TBD Snap - Snap Status
* TBD FreeBSD
* TBD Android
* TBD iOS

**i2pgram Desktop Client**

```
# ./Telegram --help
i2pgram.
options: --dchost= --dcport= --dcpubkey0file= --dcpubkey1file=
public keys must be in -----BEGIN RSA PUBLIC KEY----- format.
# cat nebuladckey0.pub 
-----BEGIN RSA PUBLIC KEY-----
MIIBCgKCAQEAvKLEOWTzt9Hn3/9Kdp/RdHcEhzmd8xXeLSpHIIzaXTLJDw8BhJy1
jR/iqeG8Je5yrtVabqMSkA6ltIpgylH///FojMsX1BHu4EPYOXQgB0qOi6kr08iX
ZIH9/iOPQOWDsL+Lt8gDG0xBy+sPe/2ZHdzKMjX6O9B4sOsxjFrk5qDoWDrioJor
AJ7eFAfPpOBf2w73ohXudSrJE0lbQ8pCWNpMY8cB9i8r+WBitcvouLDAvmtnTX7a
khoDzmKgpJBYliAY4qA73v7u5UIepE8QgV0jCOhxJCPubP8dg+/PlLLVKyxU5Cdi
QtZj2EMy4s9xlNKzX8XezE0MHEa6bQpnFwIDAQAB
-----END RSA PUBLIC KEY-----
# cat nebuladckey1.pub 
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvKLEOWTzt9Hn3/9Kdp/R
dHcEhzmd8xXeLSpHIIzaXTLJDw8BhJy1jR/iqeG8Je5yrtVabqMSkA6ltIpgylH/
//FojMsX1BHu4EPYOXQgB0qOi6kr08iXZIH9/iOPQOWDsL+Lt8gDG0xBy+sPe/2Z
HdzKMjX6O9B4sOsxjFrk5qDoWDrioJorAJ7eFAfPpOBf2w73ohXudSrJE0lbQ8pC
WNpMY8cB9i8r+WBitcvouLDAvmtnTX7akhoDzmKgpJBYliAY4qA73v7u5UIepE8Q
gV0jCOhxJCPubP8dg+/PlLLVKyxU5CdiQtZj2EMy4s9xlNKzX8XezE0MHEa6bQpn
FwIDAQAB
-----END PUBLIC KEY-----
```
