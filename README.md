#                            sshrotocol 
##                          Table of Contents

-   Introduction
-   Steps and Operations
-   Issues Encountered and Solutions
-   Theoretical Analysis
-   Conclusion
-   Resources

###  Introduction

**The objective of this evaluation is to document all the steps and operations performed during the SSH protocol practical work. The main goal is to understand the use of SSH, including SSH keys, file transfer, port forwarding, and security aspects. This file serves as a reference for anyone wishing to reproduce the exercises.**

Steps and Operations

###     SSH Connection 
**Using the ssh mo@192.67.197.104 command to remotely connect to the server via the SSH protocol.
        Command: 'ssh mo@192.67.197.104 -p 2278'
        Expected result: Secure connection to the remote server.**

###    SSH Key Generation
**Generating a public/private key pair for secure authentication.
        Command: ssh-keygen -t rsa -b 4096
        Expected result: Creation of a 4096-bit RSA key pair.**

 **File Transfer via SCP
    Using scp to transfer files between machines.
        Command: scp file.txt mo@192.67.197.104:/destination/path
        Expected result: File successfully transferred.**

   **Port Forwarding
    Using port forwarding to securely access remote services.
        Command: ssh -L 8080:localhost:80 mo@192.67.197.104
        Expected result: Access the local service on port 8080 via the remote server.**

### Issues Encountered and Solutions

**Wireshark on WSL
    When using Wireshark on WSL, I faced difficulties running the program due to limited access to network interfaces on WSL.**

**Solution: I resolved the issue by installing Wireshark directly on my host PC instead of on WSL, which allowed me to properly monitor network traffic.**

**SSH Access on a Specific Port
    While configuring SSH access on a non-standard port (2278), connection errors occurred.**

**Solution: I modified the SSH configuration file to allow connection on this port and then restarted the SSH service to apply the changes (sudo systemctl restart sshd).**

### Theoretical Analysis



*The importance of SSH encryption lies in its ability to protect data in transit from interception. By using SSH keys for authentication, security is enhanced by avoiding the transmission of passwords in clear text.*

**Changing the default port (from 22 to 2278) is a basic security measure to reduce the number of automated attack attempts.
    Using tools like Fail2Ban helps block suspicious IP addresses after several failed login attempts.**

*During network monitoring with Wireshark and Tshark (the command-line version of Wireshark), I was able to capture and analyze SSH packets to verify that the data was properly encrypted, thus ensuring secure transmission.*
###Conclusion

*This practical work allowed me to better understand the use and configuration of the SSH protocol to establish secure remote connections. I learned how to generate SSH keys, forward ports, securely transfer files, and resolve network configuration issues.
Resources*

-    [Official SSH Documentation](https://www.openssh.com)
-    [ Wireshark Tutorial](https://www.wireshark.org)
-    [Fail2Ban Documentation](https://www.ubuntu-fr.org)
