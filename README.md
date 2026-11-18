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
CLIENT:
~~~import socket

s = socket.socket()
s.connect(('localhost', 7000))

while True:
    ip = input("Enter IP Address : ")

    s.send(ip.encode())

    print("MAC Address :", s.recv(1024).decode())
~~~
SERVER:
~~~
import socket

s = socket.socket()
s.bind(('localhost', 7000))
s.listen(5)

print("ARP Server Waiting for Connection...")
c, addr = s.accept()
print("Connected with", addr)

# IP to MAC mapping
address = {
    "10.0.0.1": "AA:BB:CC:11",
    "10.0.0.2": "DD:EE:FF:22",
    "10.0.0.3": "GG:HH:II:33"
}

while True:
    ip = c.recv(1024).decode()

    try:
        mac = address[ip]
        c.send(mac.encode())
    except KeyError:
        c.send("MAC Address Not Found".encode())
~~~
## OUPUT - ARP
CLIENT:

<img width="553" height="201" alt="image" src="https://github.com/user-attachments/assets/4df1a39c-a5b7-4b59-a0fa-8c547f484518" />

SERVER:

<img width="552" height="87" alt="image" src="https://github.com/user-attachments/assets/7d202f06-402a-46cd-ac85-1f59f174aabc" />

## PROGRAM - RARP
CLIENT:
~~~
# rarp_client.py
import socket

s = socket.socket()

s.bind(('localhost', 7500))
s.listen(5)

print("RARP Server Waiting for Connection...")
c, addr = s.accept()
print("Connected with", addr)

# MAC to IP mapping
address = {
    "AA:BB:CC:11": "172.16.0.10",
    "DD:EE:FF:22": "172.16.0.20",
    "GG:HH:II:33": "172.16.0.30"
}

while True:
    mac = c.recv(1024).decode()

    try:
        ip = address[mac]
        c.send(ip.encode())
    except KeyError:
        c.send("Logical Address Not Found".encode())
~~~
SERVER:
~~~
import socket

s = socket.socket()

s.connect(('localhost', 7500))

while True:
    mac = input("Enter MAC Address : ")

    s.send(mac.encode())

    print("Logical Address :", s.recv(1024).decode())
~~~
## OUPUT -RARP
CLIENT:
<img width="537" height="85" alt="image" src="https://github.com/user-attachments/assets/217ffb77-d891-4b19-8cb9-59eb10999318" />
SERVER:
<img width="527" height="205" alt="image" src="https://github.com/user-attachments/assets/558ac559-a2c0-455c-9747-2fe1d8c36751" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
