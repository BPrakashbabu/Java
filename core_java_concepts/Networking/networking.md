Let’s dive into Networking in Java — from basic to advanced concepts, explained step-by-step.

Java Networking — Basic to Advanced
1. What is Networking?

Networking in Java is about communication between two or more devices (computers, servers, etc.) over a network, such as the internet or a local network.

2. Java Networking Basics

Java provides the java.net package to handle networking.

The key classes/interfaces are:

InetAddress — IP addresses (IPv4, IPv6).

Socket — client-side communication endpoint.

ServerSocket — server-side endpoint that listens for client requests.

URL and URLConnection — working with URLs and web connections.

3. Basic Networking Concepts

IP Address — Unique address of a device on the network.

Port Number — Identifies specific applications/services on a device.

Protocol — Rules for communication (TCP, UDP).

TCP (Transmission Control Protocol) — Reliable, connection-oriented.

UDP (User Datagram Protocol) — Faster, connectionless, but unreliable.

4. Working with InetAddress

Get IP address or hostname:

import java.net.*;

public class InetAddressExample {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress ip = InetAddress.getByName("www.google.com");
        System.out.println("IP Address: " + ip.getHostAddress());
        System.out.println("Host Name: " + ip.getHostName());
    }
}

5. Client-Server Communication (TCP)
5.1 Server
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(5000);
        System.out.println("Server started, waiting for clients...");

        Socket clientSocket = serverSocket.accept();  // waits for client
        System.out.println("Client connected");

        BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
        PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

        String msg;
        while ((msg = in.readLine()) != null) {
            System.out.println("Client: " + msg);
            out.println("Server received: " + msg);
            if (msg.equalsIgnoreCase("bye")) break;
        }

        clientSocket.close();
        serverSocket.close();
    }
}

5.2 Client
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 5000);

        BufferedReader userInput = new BufferedReader(new InputStreamReader(System.in));
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

        String msg;
        while (true) {
            System.out.print("Enter message: ");
            msg = userInput.readLine();
            out.println(msg);

            String response = in.readLine();
            System.out.println(response);

            if (msg.equalsIgnoreCase("bye")) break;
        }

        socket.close();
    }
}

6. UDP Communication

UDP uses DatagramSocket and DatagramPacket.

6.1 UDP Server
import java.net.*;

public class UDPServer {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket(9876);
        byte[] buffer = new byte[1024];

        System.out.println("UDP Server is running...");

        while (true) {
            DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
            socket.receive(packet);

            String msg = new String(packet.getData(), 0, packet.getLength());
            System.out.println("Received: " + msg);

            if (msg.equalsIgnoreCase("bye")) break;
        }
        socket.close();
    }
}

6.2 UDP Client
import java.net.*;

public class UDPClient {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        InetAddress ip = InetAddress.getByName("localhost");

        String msg = "Hello UDP Server!";
        byte[] buffer = msg.getBytes();

        DatagramPacket packet = new DatagramPacket(buffer, buffer.length, ip, 9876);
        socket.send(packet);

        socket.close();
    }
}

7. Working with URLs

You can read data from websites.

import java.net.*;
import java.io.*;

public class URLExample {
    public static void main(String[] args) throws Exception {
        URL url = new URL("http://www.example.com");
        BufferedReader in = new BufferedReader(new InputStreamReader(url.openStream()));

        String inputLine;
        while ((inputLine = in.readLine()) != null)
            System.out.println(inputLine);

        in.close();
    }
}

8. Multithreaded Server

To handle multiple clients simultaneously, use threads on the server.

Example Server Handler
import java.io.*;
import java.net.*;

public class ClientHandler extends Thread {
    private Socket clientSocket;

    public ClientHandler(Socket socket) {
        this.clientSocket = socket;
    }

    public void run() {
        try {
            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            String msg;
            while ((msg = in.readLine()) != null) {
                System.out.println("Client: " + msg);
                out.println("Server: " + msg);
                if (msg.equalsIgnoreCase("bye")) break;
            }
            clientSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

9. Advanced Concepts

Non-blocking I/O and NIO (New IO):

Java NIO allows scalable, non-blocking socket channels.

Classes: SocketChannel, ServerSocketChannel, Selector.

SSL/TLS Sockets for secure communication.

RMI (Remote Method Invocation) for calling methods on remote objects.

Multicast Networking (for group communication).

10. NIO Example (Basic Server SocketChannel)
import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;

public class NIOServer {
    public static void main(String[] args) throws IOException {
        ServerSocketChannel serverChannel = ServerSocketChannel.open();
        serverChannel.socket().bind(new InetSocketAddress(5000));
        System.out.println("NIO Server listening on port 5000");

        while (true) {
            SocketChannel client = serverChannel.accept();
            ByteBuffer buffer = ByteBuffer.allocate(256);
            client.read(buffer);

            String msg = new String(buffer.array()).trim();
            System.out.println("Received: " + msg);

            client.close();
        }
    }
}

Summary:
Level	Topics
Basic	InetAddress, Socket, ServerSocket, URL
Intermediate	TCP client-server, UDP communication
Advanced	Multithreaded server, Java NIO, SSL Sockets
Expert	RMI, Multicast, Serialization over network