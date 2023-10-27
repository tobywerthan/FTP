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
       The purpose of Homework 5 was to create an FTP server and client that communicate through TCP. 
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
  <img width="300" height="800" src="https://github.com/tobywerthan/FTP/assets/55803740/3e4c9880-396c-4dbe-9813-b6c4b8781ab8">
</p>

<p align="center">Figure 2 (Flowchart of tcp_server)</p>
</p></dd></dl></dd></dl>

<h2>Finite State Machines</h2> <a name="create"></a>

<dl><dd><h3>Client</h3> <a name="createDesc"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="500" height="600" src="https://github.com/tobywerthan/FTP/assets/55803740/0d9b4a0b-ee82-4473-b2b4-f836303b0e4e">
</p>
<p align="center">Figure 3 (Client FSM)</p>

</p></dd></dl></dd></dl>

<dl><dd><h3>Server</h3> <a name="createChart"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="500" height="600" src="https://github.com/tobywerthan/FTP/assets/55803740/d093f977-4099-401e-89e6-af33f0477a74">
</p>
<p align="center">Figure 4 (Server FSM)</p>

</p></dd></dl></dd></dl>

<dl><dd><h3>Threading</h3> <a name="createCode"></a></dd></dl> 

<dl><dd><dl><dd><p>
<p align="center">
  <img width="500" height="600" src="https://github.com/tobywerthan/FTP/assets/55803740/9b369936-b789-4854-b3cc-a2d0c957efac">
</p>
<p align="center">Figure 5 (Threading FSM)</p>

</p></dd></dl></dd></dl>

<h2>Conclusion</h3>  <a name="conclusion"></a>

<dl><dd>
 <p>
     The client is able to store files, retrieve files, login, logout, make directories, remove directories, navigate directories, send messages, list the current directory, and more on the FTP server.
 </p>
</dd><dl>
    
</div>

