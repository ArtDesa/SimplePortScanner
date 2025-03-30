# SimplePortScanner
A simple, easy-to-use port scanner script written in Python.

## Overview
Port scanning tools display which ports on a network are open for communication. This tool can help in many different ways. An example is whether or not a port is open can help a penetration tester determine their next steps in launching an attack against a network. 
A simple port scanning script in Python is easy to make and a good way to show socket programming with Python, as well as how port scanners work.

The script can be run from the command line or from within a IDE such as PyCharm.

## How does it work?
Going over the code in .py file to exaplin what is happening.

### Sockets
Sockets are the basis for all network communications performed by computers. A socket is the combination of an IP address and a port number to from a unique connection point. Sockets and the socket API are used to send messages across a network. 
They provide a form of inter-process communication (IPC). The best and most obvious example is the Internet, which you connect to via your ISP. 
For more details and information on socket programming with Python, check the following links: https://docs.python.org/3/library/socket.html and https://realpython.com/python-sockets/.

The socket module in Python provides access to the BSD socket interface. 
It includes the socket class for handling the actual data channel, and functions for network-related tasks such as converting a server’s name to an IP address and formatting data to be sent across the network. 

In order to create and use sockets in Python we import the socket library with 'import socket'.

Syntax for creating a socket:
sock = socket.socket (socket_family, socket_type)

Socket Families:
AF_INET refers to Address Family version 4 (or IPv4)
AF_INET6 refers to provides support for the Internet Protocol
version 6 (IPv6)

Socket Types:
SOCK_STREAM refers to TCP connections
SOCK_DGRAM refers to UDP connections

### Asking for user input
The script will ask the user for the target host name as input to scan. This will be held by the remoteServer variable:
remoteServer = input("Enter a remote host to scan: ")

For example: www.springboard.com

NOTE: Please be aware that you should only port scan networks that you are responsible for, or with permission of the network administrators. Actions such as port scanning can be seen as a precursor to hacking as you are looking for open ports on network devices. 
To avoid any issues, just enter the name of your PC, or a PC on your home network. 

### Range function + Datetime
Next, we use the range function to specify the ports to scan: 

for port in range(1,1024):

This will cause the program to scan all ports between 1 and 1024, and if a port is open it will be displayed to the user. 
Note: A result of 0 (if result == 0), means success. In other words, the port is open.

We also need to show the time it took to perform the scan. To do this we use the datetime module. datetime.now() will give us the current time. We do this twice, once before the scan, and then after. We subtract the first value from the second value to measure the time it took.

### Setting a timeout for the scan
There is a default timeout set for socket connection attempts. 
To avoid the problem of waiting for an undetermined amount of time for a socket to connect, we can reduce the wait time by setting a shorter timeout. This is done using the socket.settimeout() method of socket:
sock.settimeout(<timeout_value_in_seconds>)
 
The default timeout is one second, so I have set it to half a second (0.5).

### Error handling
Finally, let’s add some error handling. 
There are usually 3 main exceptions we should take into account:
1. Interrupting the program with Ctrl + C
2. Hostname could not be resolved
3. Could not connect to the remote server

To do this we make use the try statement. We surround the code executing the scanning process with a try statement. 
NOTE: Make sure it’s indented to the left. If the indent is off then the program will throw an error.

After the try statement, we need to add the 3 exceptions using the except keyword followed by the error condition (or the exception). All exceptions must be added AFTER the sock.close() statement.

1. For the Ctrl + C error, we make use the KeyboardInterrupt exception:
except KeyboardInterrupt:
print ("You pressed Ctrl+C")
sys.exit()

2. For the “Hostname could not be resolved” error, we refer to the gaierror exception:
except socket.gaierror:
print("Hostname could not be resolved")
sys.exit()

3. For the “Could not connect to remote server” error, we refer to the socket.error exception: 
except socket.error:
print("Could not connect to remote server")
sys.exit()
