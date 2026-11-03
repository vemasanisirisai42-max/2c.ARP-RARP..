# 2c.SIMULATING-ARP-RARP-PROTOCOLS
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

# server -ARP
```

import socket

def start_server():
    data = {
        "165.165.80.80": "6A:08:AA:C2",
        "165.165.79.1": "8A:BC:E3:FA"
    }

    server = socket.socket()
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind(("localhost", 9000))
    server.listen(5)

    print("Server waiting...")
    conn, addr = server.accept()

    while True:
        ip = conn.recv(1024).decode()
        if not ip:
            break

        print("Enter logical Address :", ip)
        conn.sendall(data.get(ip, "Not Found").encode())

    conn.close()
    server.close()

start_server()

```



# client-ARP

```


import socket

def find_mac():
    client = socket.socket()
    client.connect(("localhost", 9000))

    while True:
        ip = input("Enter logical Address : ").strip()
        client.sendall(ip.encode())
        print("MAC Address:", client.recv(1024).decode())

find_mac()


```
## OUPUT - ARP

# server -ARP

<img width="660" height="157" alt="image" src="https://github.com/user-attachments/assets/dcf7e100-39df-47ad-a1d4-638a936757fd" />


# client-ARP


 
 <img width="645" height="215" alt="image" src="https://github.com/user-attachments/assets/9233ee1c-05b5-45c9-bebd-c828084d7caf" />
 

## PROGRAM - RARP
# server -RARP
```

import socket

def start_server():
    data = {
        "6A:08:AA:C2": "165.165.80.80",
        "8A:BC:E3:FA": "165.165.79.1"
    }

    server = socket.socket()
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind(("127.0.0.1", 9001))
    server.listen(5)

    print("Server waiting...")
    conn, addr = server.accept()

    while True:
        mac = conn.recv(1024).decode().strip()
        if not mac:
            break

        print("Enter physical Address :", mac)
        ip = data.get(mac.upper(), "Not Found")
        conn.sendall(ip.encode())

    conn.close()
    server.close()

start_server()

```



# client-RARP

```

import socket

def find_ip():
    client = socket.socket()
    client.connect(("127.0.0.1", 9001))

    while True:
        mac = input("Enter physical Address : ").strip()
        client.sendall(mac.encode())
        print("Logical Address:", client.recv(1024).decode())

find_ip()



```
## OUPUT -RARP

# server -RARP

<img width="651" height="137" alt="image" src="https://github.com/user-attachments/assets/1e71abe4-1448-4ed4-bb19-69469dc6e684" />

# client-RARP

<img width="640" height="192" alt="image" src="https://github.com/user-attachments/assets/58d91a57-3551-4dc6-984b-d7b250adde6f" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
