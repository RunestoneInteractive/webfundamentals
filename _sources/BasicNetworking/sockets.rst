Sockets: The Building Blocks of Network Programming
===================================================


How is it that two programs each running on their own computer can communicate with each other?  This is, of course, what happens many times a day when your browser shows you a web page.  Your browser is a program, and it must communicate with a web server in order to get the HTML, CSS, images, and Javascript that make up a web page.  The details of how this simple communication happens can take an entire semester in a Networking course.  We are going to tackle just the top layer of this problem looking at the application layer of the Networking stack.

The building block of the application layer is the socket.  Sockets provide for easy two way communication between two programs running on two different computers (or hosts).  A socket is uniquely identified by four values:

* source ip address
* source port
* destination ip address
* destination port

These values need some definition.  First, what do we mean by an IP address?  You already know that the computers on the internet have nice memorable names like www.google.com or knuth.luther.edu.  Each name can be translated into a unique IP numerical IP address, such as 192.203.196.71, only 1 machine on the internet can have the IP address of 192.203.196.71  (however, that address can be known by multiple names).   The numerical addresses are necessary for the machinery of the internet to do the work of getting a message from one machine to the other.

The port number is important because one computer may have many programs running each corresponding to a different network service.  For example the web server runs on port 80 while the mail server runs on port 25 and the ssh server runs on port 22.  So the port identifies which program on the computer the socket is connected to.  On your laptop, the situation is similar, you may have a web browser connected to many different web servers in differnt tabs, you have a mail client connected to a mail server, and you probably have an message client connected to a chat server, etc.
