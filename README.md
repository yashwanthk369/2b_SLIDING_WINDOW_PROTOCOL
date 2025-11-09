# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

# Name : Yashwanth K
# Reg No : 212224040369

## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

server.py

```
import socket

s = socket.socket()
s.bind(('localhost', 6000))   # Server binds to port 6000
s.listen(5)
c, addr = s.accept()

size = int(input("Enter number of frames to send : "))
l = list(range(size))
w = int(input("Enter Window Size : "))

st = 0
i = 0
while True:
    while i < len(l):
        st += w
        c.send(str(l[i:st]).encode())
        ack = c.recv(1024).decode()
        if ack:
            print("Received ACK:", ack)
            i+=w
```

client.py

```
import socket

c = socket.socket()
c.connect(('localhost', 6000))   # Client connects to server

while True:
    data = c.recv(1024).decode()
    if not data:
        break
    print("Received frames:", data)
    ack = input("Enter ACK to send back: ")
    c.send(ack.encode())
```

## OUPUT

<img width="1353" height="445" alt="image" src="https://github.com/user-attachments/assets/879ada9d-261c-4448-bedf-bdbf18b0fe9e" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
