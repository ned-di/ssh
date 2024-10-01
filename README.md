# SSH Protocol 
## Table of Contents

[-Introduction](#Introduction)
   [- What is SSH?](#What-is-SSH?)
    [-Basic Concepts](#Basic-Concepts)
    [-Steps and Explanations](#Steps-and-Explanations)
    [-SSH Connection](#SSH-Connection)
    [-SSH Key Generation](#SSH-Key-Generation)
   [- File Transfer via SCP](#File-Transfer-via-SCP)
   [- Port Forwarding](#Port-Forwarding)
   [- Problems and Solutions](#Problems-and-Solutions)
    [-Why is SSH Secure?](#-Why-is-SSH-Secure?)
    [-Conclusion](#Conclusion)
    [-Resources](Resources)

### Introduction

*SSH is an essential tool for IT professionals. It allows secure remote connections to other computers or servers, file transfers, remote management of services, and more. This guide will explain, step-by-step, how to use SSH to connect to a server, generate security keys, transfer files, and more.
Imagine this:*

*You need to send a very important letter, but you don't want anyone to read it while it's on its way. SSH is like a highly secure postal service that encrypts (hides) everything you send, so even if someone intercepts the letter, they won't be able to read it without the special key to decrypt it.*

### What is SSH?

*SSH (Secure Shell) is a protocol that allows communication with another computer remotely while maintaining a high level of security. It's primarily used for:*

**Remote connections to computers/servers.
    File transfers.
    Running commands on another computer as if you were sitting right in front of it.**

 **Why is SSH important?**

*Before SSH, protocols like Telnet allowed remote connections but sent information without any protection, meaning anyone could easily spy on the information being sent, including passwords. SSH changed this by making remote connections encrypted and much safer.*

### Basic Concepts*

*Before diving into the steps, it's important to understand a few key concepts related to SSH.*
**1. What is a server?**

*A server is simply a computer, often more powerful, that can be accessed remotely to provide services or host data. When you connect using SSH, you're usually connecting to a server.
**2. What is an IP address?**

*An IP address is a unique address of a device (computer, phone, server) on a network. It's like the street address of your house, but for online devices. Example of an IP address:* `192.67.197.104.`
**3. What is a port?**

*A port is like a specific door through which information passes on a network. SSH uses port 22 by default, but it’s possible to change this port for security reasons.

### Steps and Explanations
### SSH Connection*

**Why is it important?**
*Connecting remotely to a server allows you to manage files, run commands, and monitor the system without physically being in front of the machine. Imagine you're at your office, but you want to work on a server located thousands of miles away. With SSH, you can do this.*

*How does it work?
When you want to connect to another computer using SSH, you need to use a special command in a terminal. For example, if your username is mo and the remote computer’s IP address is `192.67.197.104`, you would type this command into your terminal:*

**bash**

`ssh mo@192.67.197.104 -p 2278`

ssh: Tells the system you want to use SSH.
    `mo@192.67.197.104`: Here, mo is your username on the remote computer, and `192.67.197.104` is the IP address of that computer.
    `-p 2278`: This indicates that you're using port 2278 instead of the default SSH port (22).

What happens next?

After running this command, you connect to the remote computer. If it’s your first time connecting, it will ask if you trust this computer, and then it will prompt you for your password.
### SSH Key Generation

**What is it?**
*To make connections even more secure, SSH uses a key system. A key is a long encrypted code that acts as a unique identifier. When you connect, the server checks that you have the correct key before letting you in, like using a magnetic card to enter a secured building.*

### Why use SSH keys?
*SSH keys are much more secure than passwords because they are much harder to break. They are also more convenient because you can set up your SSH connection to not require a password every time.*

### How to generate an SSH key?
*Here is the command to generate a pair of SSH keys (one public, one private):*

**bash**

`ssh-keygen -t rsa -b 4096`

*ssh-keygen: The program that creates a new pair of keys.
    -t rsa: Specifies that the key will be of type RSA (a secure encryption algorithm).
    -b 4096: Means the key will be 4096 bits long, making it very hard to break.*

**What happens next?**

**Two files are created:**

*Private key: Stays on your computer. It’s your access card, never share it.
    Public key: This is copied to the server, and it’s used to verify that you own the private key.*

### File Transfer via SCP

What is it?
SCP (Secure Copy Protocol) is a method that allows you to send files from one computer to another using SSH. It’s like sending a letter, but with special protection to ensure that no one can read it along the way.

How to transfer files?
Let’s say you have a file called file.txt on your computer, and you want to send it to a remote server. Here’s the command to do that:

bash

scp file.txt mo@192.67.197.104:/destination/path

scp: The command to securely copy a file.
    file.txt: The file you want to transfer.
    mo@192.67.197.104:/destination/path: This indicates where you want to send the file on the remote computer (in which folder).

Why is this useful?

With this command, you can easily send or retrieve files without using online storage services like Google Drive or Dropbox.
Port Forwarding

What is it?
Port forwarding lets you use SSH to access services that are on another computer as if they were on your own computer. For example, if a website is hosted on the server, you can view it through your computer but in a secure way.

How does it work?
Let’s say you want to access a web application running on port 80 of a remote server (the port used for websites). Here’s the command you would use to forward that port to your computer:

bash

`ssh -L 8080:localhost:80 mo@192.67.197.104`

`-L 8080:localhost:80:` This means port 8080 on your computer will be connected to port 80 on the remote computer.

Then you open your browser and type http://localhost:8080, and you’ll access the remote website securely through SSH.
Problems and Solutions
Wireshark and Tshark on WSL

### Problems and Solutions

Problem: When I tried to use Wireshark (a graphical tool for monitoring network traffic) on WSL (Windows Subsystem for Linux), I encountered issues because WSL doesn't provide direct access to network interfaces to capture traffic. Since Wireshark runs in graphical mode, this caused compatibility problems with WSL.

Solution: I solved this problem by installing Tshark, the command-line version of Wireshark, directly on WSL. Tshark can capture network packets without needing a graphical interface. However, for a better experience, I later installed Wireshark directly on my host PC (Windows), rather than using WSL. This allowed me to properly monitor the network traffic.

### Why is SSH Secure?

SSH is secure because it encrypts all the information you send and receive. This means that even if someone intercepts the data, they won’t be able to read it. Here are other security measures:

Changing the default port: Using a port other than 22 (like 2278) to reduce the chances of automated attack attempts.
    Fail2Ban: A program that blocks suspicious IP addresses after several failed login attempts to prevent brute force attacks.

Using tools like Wireshark and Tshark, you can monitor traffic and see that all the information sent is encrypted and protected.

### Conclusion

Through SSH, I learned how to remotely connect to a computer, securely transfer files, and forward ports to access remote services. I also learned how to troubleshoot issues like connecting to a specific port and using network monitoring tools.

 ### Resources

-    [Official SSH Documentation](https://www.openssh.com)
-    [ Wireshark Tutorial](https://www.wireshark.org)
-    [Fail2Ban Documentation](https://www.ubuntu-fr.org)
