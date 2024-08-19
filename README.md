# Simple-Python-Port-Scanner
Demonstrates how to create an easy-to-use port scanner program written in Python. Assignment from USF Cybersecurity Bootcamp.

Mini-Project 31: Python for Cybersecurity


Mini-Project Overview


Time Estimate: 1 hour


In Section 8: Network Security, you learned about port scanning, specifically using the Nmap tool. As you may recall, port scanning tools display which ports on a network are open for communication. Whether or not a port is open can help with determining the next steps a pen tester might want to take in launching attacks against a network. 
Creating a simple port scanning tool in Python is easy, and is a great way to both learn socket programming with Python, and learn how port scanners work.

NOTE: This exercise has been written and tested in Python 3.9 and PyCharm 2021.3 (Community Edition). The final program can be run from the command line, or you can run them from within PyCharm.


This project will demonstrate how to create an easy-to-use port scanner program written
in Python. You will start with the basic program, and then you will be asked to add enhancements to it.


1. Part One
Begin by downloading the Python script called portscanner.py. You may either copy it to your PC and open it using PyCharm, or cut and paste it into a new Pycharm project.

Before we get started let’s talk about sockets. 
Sockets are the basis for all network communications performed by computers. 
Sockets and the socket API are used to send messages across a network. 
They provide a form of inter-process communication (IPC). 
The best and most obvious example is the Internet, which you connect to via your ISP. 
For more information on socket programming with Python see: https://docs.python.org/3/library/socket.html and https://realpython.com/python-sockets/.

The socket module in Python provides access to the BSD socket interface. 
It includes the socket class, for handling the actual data channel, and functions for network-related tasks such as converting a server’s name to an IP address and formatting data to be sent across the network. 

In order to create and use sockets in Python we must first import the socket library (“import socket”). You will see this statement at the very beginning of the program.

Syntax for creating a socket:

sock = socket.socket (socket_family, socket_type)


Socket Families:

AF_INET refers to Address Family version 4 (or IPv4)

AF_INET6 refers to provides support for the Internet Protocol
version 6 (IPv6)


Socket Types:

SOCK_STREAM refers to TCP connections

SOCK_DGRAM refers to UDP connections



Question 1: In the program, what is the line for creating a socket?

The program will ask the user to input the target host name. Whatever you enter will be assigned to the remoteServer variable.

remoteServer = input("Enter a remote host to scan: ")

For example, if www.springboard.com is entered as the target then remoteServer = www.springboard.com 

NOTE: Please be aware that you should only port scan networks that you are responsible for, or with permission of the network administrators, Actions such as port scanning can be seen as a precursor to hacking as you are looking for open ports on network devices. 
To avoid any issues, just enter the name of your PC, or a PC on your home network. 

Next, we use the range function to specify the ports to scan: 

for port in range(21,81):

This will cause the program to scan all ports between 21 and 81, and if a port is open it will display on the screen. 
Note that a result of 0 (if result == 0) means success. In other words, the port is open.

Lastly, we need to show the time it took to perform the scan using the datetime module, and we do this by appending now() to it. This will give us the current time. We do this twice, and then subtract the first value from the second value.




Question 2: In the program, what are the three lines that are used to obtain the start time, end time and elapsed time?

When you run the program, it will prompt you to enter a remote host to scan. 
Once you enter the hostname, hit Enter and it should start scanning. 

Note that you may not see anything happen for a minute or two since not all ports may be open. If you want to stop the program early from within PyCharm, you can simply click the red Stop button to the left of the runtime window, or hit Ctrl + F2.

2. Part Two
Now let’s add some enhancements to our program. 

Currently, we are scanning ports from 21 to 81. While this will show us some key ports like ftp, ssh and telnet, this range is still pretty narrow, so let’s expand it to cover all of the Well-Known TCP Port Numbers. The Well-Known ports range from 1 to 1024. 

A. Modify the line where we specify the range of ports to scan so that instead of 21 to 81, we are scanning from 1 to 1024.

Next, let’s speed up the scanning process by reducing the default timeout. 
In order to avoid the annoying problem of waiting for an undetermined amount of time for a socket to connect, we can reduce the wait time by setting a shorter timeout. This is done using sock.settimeout(timeout). 
The default timeout is one second, so let’s make it half a second.

B. Add a line to specify the new timeout value. Hint: It should come directly after the line where we create the socket.


Finally, let’s add some error handling. 
There are usually 3 main exceptions that programmers like to account for:
1. Interrupting the program with Ctrl + C
2. Hostname could not be resolved
3. Could not connect to the remote server

In order to accomplish this we must use the try statement. The try statement itself needs to come prior to the code that is executing the scanning process, which in this case is the “for” statement. So, enter “try:” (remember to add the colon directly after the “try” statement) just before the “for” statement, and make sure it’s indented to the left. If the indent is off then the program will throw an error.

Now that we have the try statement in there, we need to add the 3 exceptions. This is done using the except keyword, followed by the error condition (or exception). All exceptions must be added AFTER the sock.close() statement.

Let’s add the Ctrl + C error first by referencing the KeyboardInterrupt exception:

except KeyboardInterrupt:
print ("You pressed Ctrl+C")
sys.exit()

Next, let’s add the “Hostname could not be resolved” error. 
For this, we need to reference the gaierror exception. Go ahead and do this yourself using the previous code as an example.


Finally, let’s add the “Could not connect to remote server” exception. 
For this one we will reference the socket.error exception. As before, go ahead and do this yourself using the above code as an example.

You should have now added all three exceptions to the code, so go ahead and run it again. 
Feel free to play around to see if you can get one or more of the exceptions to occur.
