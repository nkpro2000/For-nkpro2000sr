## Added support to use socket object
This added support to directly use connected socket.socket object while calling pypsexec.client.Client() instead of giving ip and port.
#### For Example :
```python
import socket
server = socket.socket()
server.connect((server_ip, server_port))
from pypsexec.client import Client
client = Client(server, username="user_name", password="password")
clinet.connect()
```
> otherwise normally
> ```python
> from pypsexec.client import Client
> clinet = Client(server_ip, port=server_port, username="user_name", password="password")
> clinet.connect()
> ```
_____
this support to accept socket object is useful while making our own relays or other bidirectional socket communication to control remote machine.
#### sample situation :
```
                         XXXXXXXXXXXXXXXXXX
         +------------> XX  SSH Server     X +----------------+   Initial Connection
         | +----------X XX               XXX <----------- --+ |   X---------------->
         | |             XXXXXXXXXXXXXXXXX                  | |
         | |                                                | |
    +-+  + v  +-+                                    +-+    X v                    +-+
    |Remote Port|                                    | bidirectional connected socket|
    |Forwarding |                                    | two-way communication         |
    +-+  ^ X  +-+                                    +-+    ^ X                    +-+
         | |                                                | |
         | |                                                | |
         | |                                                | |
+--------+-v-------+                              +---------+-v------+
|                  |                              |      Remote      |
|      Client      |                              |  windows machine |
| running pypsexec |                              |listening port 445|
+------------------+                              +------------------+
```
