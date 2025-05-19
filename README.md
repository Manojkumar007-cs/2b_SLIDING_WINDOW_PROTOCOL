# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## CLIENT
```

import socket

# Create a socket object
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

# Accept a connection
c, addr = s.accept()

# Get the number of frames to send
size = int(input("Enter number of frames to send: "))
frames = list(range(size))

# Get the window size
window_size = int(input("Enter Window Size: "))

start = 0
i = 0

while True:
    while i < len(frames):
        start += window_size
        # Send a batch of frames based on the window size
        c.send(str(frames[i:start]).encode())
        ack = c.recv(1024).decode()
        if ack:
            print(ack)
            i += window_size

```
## SERVER
```

import socket

# Create a socket object
s = socket.socket()
s.connect(('localhost', 8000))

while True:
    # Receive data from the client
    data = s.recv(1024).decode()
    print(data)
    # Send acknowledgment back to the client
    s.send("Acknowledgment received from server".encode())

```

## OUPUT

![image](https://github.com/user-attachments/assets/81f910e6-dbfc-44d1-bd58-8a13cbf8fdd8)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
