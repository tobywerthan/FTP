# Homework 5: FTP Server & Client

Toby Werthan

10/27/2023

ENCE 3321

## Table of Contents
1. [Introduction](#introduction)
2. [Flowcharts](#main)
    1. [tcp_client](#mainDesc)
    2. [tcp_server](#mainChart)
3. [Finite State Machines](#create)
    1. [Client](#createDesc)
    2. [Server](#createChart)
    3. [Threading](#createCode)
4. [Client](#ping)
6. [Server](#stats)
7. [Conclusion](#conclusion)

*Note: If images are hard to view, please click on them. A new tab will open, displaying the full-size image.*
<div align="left">
<h2>Introduction</h2>  <a name="introduction"></a>
<dl><dd>
    <p>
       The purpose of this homework was to create a UDP client in Python that acts as a pinger. The client is meant to interact with the provided server through UDP sockets. The client sends a message (utf-8 encoded) to the server and receives one back depending on if simulated packet loss is enabled. The round trip time of each packet, as well as the total RTT of 10 transmitted packets, is calculated. Each packet's RTT is displayed if the message from the server is received. Once all packets have been transmitted, the pinger statistics are displayed including total RTT, packet loss, and packets transmitted. This program uses the packages: time, sys, and socket. 
    </p>
</dd><dl>

<h2>Flowcharts</h2> <a name="main"></a>

<dl><dd><h3>tcp_client</h3> <a name="mainDesc"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="350" height="600" src="https://github.com/tobywerthan/FTP/assets/55803740/fa953e9e-cf74-447a-9a59-1f96a8ab2afe">
</p>

<p align="center">Figure 1 (Flowchart of tcp_client)</p>

</p></dd></dl></dd></dl>

<dl><dd><h3>tcp_server</h3> <a name="mainChart"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="350" height="800" src="https://github.com/tobywerthan/FTP/assets/55803740/3e4c9880-396c-4dbe-9813-b6c4b8781ab8">
</p>

<p align="center">Figure 2 (Flowchart of tcp_server)</p>
</p></dd></dl></dd></dl>

<h2>Finite State Machines</h2> <a name="create"></a>

<dl><dd><h3>Client</h3> <a name="createDesc"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="250" height="600" src="https://github.com/tobywerthan/ENCE_3321_NetworkDesign_2023/assets/55803740/5d87614f-569c-4796-9e3a-a76e2b391555">
</p>
<p align="center">Figure 3 (Client FSM)</p>

</p></dd></dl></dd></dl>

<dl><dd><h3>Server</h3> <a name="createChart"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="250" height="600" src="https://github.com/tobywerthan/ENCE_3321_NetworkDesign_2023/assets/55803740/5d87614f-569c-4796-9e3a-a76e2b391555">
</p>
<p align="center">Figure 4 (Server FSM)</p>

</p></dd></dl></dd></dl>

<dl><dd><h3>Threading</h3> <a name="createCode"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="250" height="600" src="https://github.com/tobywerthan/ENCE_3321_NetworkDesign_2023/assets/55803740/5d87614f-569c-4796-9e3a-a76e2b391555">
</p>
<p align="center">Figure 5 (Threading FSM)</p>

</p></dd></dl></dd></dl>

<h2>Client</h2> <a name="ping"></a>

<dl><dd><p>

    def ping_client():
        # Global variables
        global s, host, port, RTT, ptime, addr, time, packet_lost
    
        # Sequence number of the ping message
        ptime = 0
    
        # Set round trip time, number of packets lost, client input, and number of client inputs to empty or zero
        RTT = 0
        packet_lost = 0
        client_input = ""
        input_count = 0
    
        # Get the input message from the client
        while not (client_input == "RND" or client_input == "NO RND"):
            if input_count > 0:
                print("ping> Unrecognized Command: {}".format(client_input))
                print("      Valid Commands: RND, NO RND")
            client_input = input("ping> ").strip()
            input_count += 1
        print("")
        print("Pinging server in mode: {}".format(client_input))
        print("")
    
        # Ping for 10 times
        while ptime < 10:
            ptime += 1
            # Format the message to be sent
            message = client_input
    
            try:
                # Sent time
                RTTb = time.time()
    
                # Send the UDP packet with the ping message
                try:
                    s.sendto(message.encode("utf-8"), (host, port))
                except socket.error as msg:
                    print(str(msg))
    
                # Receive the server response
                data, addr = s.recvfrom(2048)
    
                # Received time
                RTTa = time.time()
    
                # Compute RTT
                RTT_packet = RTTa - RTTb
                RTT = (RTT_packet) + RTT
    
                # Display packet time
                dataCount = len(data)
                print(
                    "{} bytes from {}: seq={} time={} ms".format(
                        dataCount, addr[0], ptime, RTT_packet * 1000
                    )
                )
    
                # Delay for readability
                sleep(1)
    
            except:
                # Server does not response
                # Assume the packet is lost
                print("Request timed out.")
                packet_lost += 1
                continue
    
        # Close socket
        s.close()
<p align="center">Figure 6 (Snippet of the code from ping_client())</p>
</p></dd></dl> 

<h2>Server</h2> <a name="stats"></a>

<dl><dd><p>

    def ping_client():
        # Global variables
        global s, host, port, RTT, ptime, addr, time, packet_lost
    
        # Sequence number of the ping message
        ptime = 0
    
        # Set round trip time, number of packets lost, client input, and number of client inputs to empty or zero
        RTT = 0
        packet_lost = 0
        client_input = ""
        input_count = 0
    
        # Get the input message from the client
        while not (client_input == "RND" or client_input == "NO RND"):
            if input_count > 0:
                print("ping> Unrecognized Command: {}".format(client_input))
                print("      Valid Commands: RND, NO RND")
            client_input = input("ping> ").strip()
            input_count += 1
        print("")
        print("Pinging server in mode: {}".format(client_input))
        print("")
    
        # Ping for 10 times
        while ptime < 10:
            ptime += 1
            # Format the message to be sent
            message = client_input
    
            try:
                # Sent time
                RTTb = time.time()
    
                # Send the UDP packet with the ping message
                try:
                    s.sendto(message.encode("utf-8"), (host, port))
                except socket.error as msg:
                    print(str(msg))
    
                # Receive the server response
                data, addr = s.recvfrom(2048)
    
                # Received time
                RTTa = time.time()
    
                # Compute RTT
                RTT_packet = RTTa - RTTb
                RTT = (RTT_packet) + RTT
    
                # Display packet time
                dataCount = len(data)
                print(
                    "{} bytes from {}: seq={} time={} ms".format(
                        dataCount, addr[0], ptime, RTT_packet * 1000
                    )
                )
    
                # Delay for readability
                sleep(1)
    
            except:
                # Server does not response
                # Assume the packet is lost
                print("Request timed out.")
                packet_lost += 1
                continue
    
        # Close socket
        s.close()
<p align="center">Figure 6 (Snippet of the code from ping_client())</p>
</p></dd></dl> 

<h2>Conclusion</h3>  <a name="conclusion"></a>

<dl><dd>
 <p>
  
 </p>
</dd><dl>
    
</div>

