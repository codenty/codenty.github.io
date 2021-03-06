---
layout: post
author: "0x4D5041"
title: Requests over TOR network
icon: python
date: 2022-03-31 18:09 -03:00
modified: 2022-04-14 16:43 -03:00
tags: [python, TOR]
description: Anonymizing HTTP requests with TOR proxies
---

<img src="../assets/img/python-requests-over-tor/python-requests-tor-network.png" alt="python-requests-and-tor-proxies">


### TOR network

This network allows to people to anonymize their internet activity, using thousands of proxies around the world.
Get more information [here](https://www.torproject.org/about/history/)

To start using TOR, just install it typing (Ubuntu 20):

```bash
sudo apt install tor
```

before install, launch the tor service

```bash
service tor start
```
check if the service is running, it should say _active_
```bash
service tor status

● tor.service - Anonymizing overlay network for TCP (multi-instance-master)
     Loaded: loaded (/lib/systemd/system/tor.service; enabled; vendor preset: enabled)
     Active: active (exited) since XX XXXX-XX-XX XX:XX:XX XX; 5s ago
    Process: XXXX ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: XXXX (code=exited, status=0/SUCCESS)
```

*TOR service runs on **9050** port

if you want stop the service...
```
service tor stop
```

### Using with Python requests

Before use requests with the tor, you can check your ip without using proxies

```python
>>> import requests
>>> requests.get('https://api.ipify.org').text #This display you real IP address
```
with the TOR service active, declare a proxy dictionary

```python
>>> import requests
>>> proxies = {
...         'http': 'socks5://127.0.0.1:9050',
...         'https': 'socks5://127.0.0.1:9050'
...    }
>>> requests.get('https://api.ipify.org', proxies=proxies).text
'199.249.230.176' # Proxy IP
```

### Requests Session

also it's possible to implement a [Session Object](https://docs.python-requests.org/en/master/user/advanced/) _it allows to keep on certain parameters across requests, like cookies_

```python

>>> import requests
>>> session = requests.Session()
>>> session.proxies = {
...         'http': 'socks5://127.0.0.1:9050',
...         'https': 'socks5://127.0.0.1:9050'
...    }
>>> session.get('https://api.ipify.org').text
'51.15.250.93' # proxy IP
```