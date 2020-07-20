# Network Programming
> writing programs that execute across multiple devices (computers), in which the devices are all connected to each other using a network.

## `java.net` package of J2SE API 
> provide a collection fo classes and interface about low-level communication details.

### Support two commonn network protocols
1. TCP: Transmission Control Protocol,which allows for reliable communication between two applications. TCP is typically used over the Internet Protocol, which is referred to as TCP/IP.
2. UDP: User Datagram Protocol, a connection-less protocol that allows for packets of data to be transmitted between applications.
---
## `java.net.URL`
> Class URL represents a Uniform Resource Locator, a pointer to a "resource" on the World Wide Web. 

* URL parts
```
protocol://host:port/path?query#ref
http://www.amrood.com/index.htm?language=en#j2se
```
* URL does not specify a port, in which case the default port for the protocol is used.

### URL Class Methods

* Constructor
```
URL(String spec)// Creates a URL object from the String representation.
URL(String protocol, String host, int port, String file)//Creates a URL object from the specified protocol, host, port number, and file.
URL(String protocol, String host, String file)
```

* Methods: accessing the various parts of the URL
```
public String getPath();
public String getQuery()
public String getAuthority()
public int getPort()
ublic String getProtocol()
public String getHost()
public String getRef()
public URLConnection openConnection() throws IOException// Returns a URLConnection instance that represents a connection to the remote object referred to by the URL.
```
----

## java.net.URLConnection
> an abstract class whose subclasses represent the various types of URL connections.
```
HttpURLConnection(URL u);
Object getContent()//Retrieves the contents of this URL connection.
String getContentEncoding()//Returns the value of the content-encoding header field.
int getContentLength()//Returns the value of the content-length header field.
String getContentType()//Returns the value of the content-type header field.
void disconnect()// Indicates that other requests to the server are unlikely in the near future.
public void setDoInput(boolean input)//Passes in true to denote that the connection will be used for input.

```
---
## Socket Programming
> Sockets provide the communication mechanism between two computers using TCP

* A socket is an endpoint for communication between two machines.

When the connection is made, the server creates a socket object on its end of the communication. The client and the server can now communicate by writing to and reading from the socket.

* `java.net.Socket`:implements client sockets (also called just "sockets")
* `java.net.ServerSocket` class provides a mechanism for the server program to listen for clients and establish connections with them.

### Establishing a TCP connection between two computers using sockets
1. The server instantiates a ServerSocket object, denoting which port number communication is to occur on.
2. The server invokes the accept() method of the ServerSocket class. This method waits until a client connects to the server on the given por3. 
3. After the server is waiting, a client instantiates a Socket object, specifying the server name and the port number to connect to.
4. The constructor of the Socket class attempts to connect the client to the specified server and the port number. If communication is established, the client now has a Socket object capable of communicating with the server.
5. On the server side, the accept() method returns a reference to a new socket on the server that is connected to the client's socket.


After the connections are established, communication can occur using I/O streams,Each socket has both an OutputStream and an InputStream. The client's OutputStream is connected to the server's InputStream.

TCP is a two-way communication protocol, hence data can be sent across both streams at the same time

### ServerSocket methods
> A server socket waits for requests to come in over the network.
>> t performs some operation based on that request, and then possibly returns a result to the requester.
```
public ServerSocket(int port) throws IOException
public Socket accpet()// Listens for a connection to be made to this socket and accepts it.
public bind()// Binds the ServerSocket to a specific address (IP address and port number).
public close()// Closes this socket
public getChannel()// Returns the unique ServerSocketChannel object associated with this socket, if any.
public int getLocalPort() // Returns the port number on which this socket is listening.
public void setSoTimeout(int timeout)
```

### Socket methods
The client obtains a Socket object by instantiating one, whereas the server obtains a Socket object from the return value of the accept() method.
```
public Socket(InetAddress host, int port) throws IOException
public void connect(SocketAddress host, int timeout) throws IOException
public int getPort()//Returns the port the socket is bound to on the remote machine.
public int getLocalPort()// Returns the port the socket is bound to on the local machine.
public SocketAddress getRemoteSocketAddress()// Returns the address of the remote socket.
public InputStream getInputStream() throws IOException// Returns the input stream of the socket. The input stream is connected to the output stream of the remote socket.
public OutputStream getOutputStream() throws IOException
```
### InetAddress Class Methods
> Internet Protocol (IP) address
```
static InetAddress getByAddress(byte[] addr)//Returns an InetAddress object given the raw IP address.
static InetAddress getByAddress(String host, byte[] addr)//Creates an InetAddress based on the provided host name and IP address.
static InetAddress getByName(String host)//Determines the IP address of a host, given the host's name.
String getHostAddress()
String getHostName()
String toString()
```
