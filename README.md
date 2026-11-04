# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## AIM
To write a python program to perform sliding window protocol 

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program

## PROGRAM
**sender.py**
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

n = int(input("Enter the number of frames: "))
window = int(input("Enter the window size: "))

frames = [f"Frame {i}" for i in range(1, n + 1)]

i = 0

while i < n:
    print("\nSending frames:")

    for j in range(i, min(i + window, n)):
        print("Sending:", frames[j])
        s.send(frames[j].encode())
        ack = s.recv(1024).decode()
        print("Acknowledgement received:", ack)

    i += window

print("\nAll frames sent successfully!")
s.close()
~~~
**receiver.py**
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Receiver is waiting for connection...")

c, addr = s.accept()
print("Sender connected:", addr)

while True:
    data = c.recv(1024).decode()

    if not data:
        break

    print("Received:", data)

    ack = "ACK received"
    c.send(ack.encode())

c.close()
s.close()
~~~

## OUPUT

<img width="792" height="536" alt="image" src="https://github.com/user-attachments/assets/7ad610f6-8c4e-48b9-9002-24eb8c47e0ea" />


<img width="826" height="237" alt="image" src="https://github.com/user-attachments/assets/4b6ac9b9-0825-4e4a-bde4-0777912c852a" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
