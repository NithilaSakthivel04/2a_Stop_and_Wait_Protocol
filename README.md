AIM
To write a python program to perform stop and wait protocol

ALGORITHM
Start the program.
Get the frame size from the user
To create the frame based on the user request.
To send frames to server from the client side.
If your frames reach the server it will send ACK signal to client
Stop the Program
PROGRAM
CLIENT:

import socket
import time
client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  
while True:
    msg = input("Enter a message (or type 'exit' to quit): ")
    client.send(msg.encode())  
    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break
    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue  
SERVER:

import socket
server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")
while True:
    data = conn.recv(1024).decode()
    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())
        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break
OUTPUT
CLIENT: Screenshot 2025-04-29 200122

SERVER: Screenshot 2025-04-29 200140

RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
