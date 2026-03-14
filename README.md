# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
server.py
~~~
# arp_server.py
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(1)

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

print("ARP Server Started")

c, addr = s.accept()

while True:
    ip = c.recv(1024).decode()

    if ip in arp_table:
        mac = arp_table[ip]
    else:
        mac = "IP not found"

    c.send(mac.encode())
~~~
client .py
~~~
# arp_client.py
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    ip = input("Enter IP Address: ")
    s.send(ip.encode())

    mac = s.recv(1024).decode()
    print("MAC Address:", mac)
~~~

## OUPUT - ARP

## PROGRAM - RARP
server.py
~~~
# rarp_server.py
import socket

s = socket.socket()
s.bind(('localhost', 9002))
s.listen(1)

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

print("RARP Server Started")

c, addr = s.accept()

while True:
    mac = c.recv(1024).decode()

    if mac in rarp_table:
        ip = rarp_table[mac]
    else:
        ip = "MAC not found"

    c.send(ip.encode())
~~~
client.py
~~~
# rarp_client.py
import socket

s = socket.socket()
s.connect(('localhost', 9002))

while True:
    mac = input("Enter MAC Address: ")
    s.send(mac.encode())

    ip = s.recv(1024).decode()
    print("IP Address:", ip)
~~~

## OUPUT -RARP

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
