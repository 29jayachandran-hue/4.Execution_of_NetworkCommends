# 4.Execution_of_NetworkCommands
## AIM :
Use of Network commands in Real Time environment
## Software : 
Command Prompt And Network Protocol Analyzer
## Procedure: 
To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>
## Program
CLIENT
```py
import socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(('localhost', 12345))
print("Connected to Server")
while True:
    command = input("Enter Network Command: ")
    client.send(command.encode())
    if command.lower() == "exit":
        break
    result = client.recv(4096).decode()
    print("Server Output:")
    print(result)
client.close()
```
SERVER
```py
import socket
import subprocess
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('localhost', 12345))
server.listen(1)
print("Server is waiting for client...")
conn, addr = server.accept()
print("Client connected:", addr)
while True:
    command = conn.recv(1024).decode()
    if command.lower() == "exit":
        break
    try:
        result = subprocess.check_output(
            command,
            shell=True,
            stderr=subprocess.STDOUT
        )
        conn.send(result)
    except subprocess.CalledProcessError as e:
        conn.send(e.output)
conn.close()
server.close()
```
## Output
<img width="1293" height="541" alt="image" src="https://github.com/user-attachments/assets/94dce384-6565-4fc7-98cb-fb5225a9e8df" />


## Result
Thus Execution of Network commands Performed 
