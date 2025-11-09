C++ Networked File Sharing Application

This project implements a simple, networked file-sharing application with a server and client in C++. It uses native sockets for networking (supporting both Windows and Linux/macOS) and demonstrates basic authentication and encryption concepts.

Project Status: Complete (Educational)

Security Warning: The encryption used (XOR cipher) is NOT secure and is for educational purposes only. Do not use this for sensitive data. A real-world application must use TLS/SSL (e.g., via OpenSSL).

Features
Cross-Platform: Compiles and runs on Windows, macOS, and Linux.

Multi-Threaded Server: The server handles each client in a separate thread.

Authentication: A simple username/password check is required to connect.

File Listing: Clients can request a list of files available on the server.

File Download: Clients can download files from the server.

File Upload: Clients can upload files to the server.

"Educational" Encryption: All communication (passwords, commands, file data) is "encrypted" with a simple XOR cipher.

File Structure
FileShareApp_CPP/ ├── .gitignore # Tells Git which files to ignore ├── Dockerfile # Recipe to build a Docker container for the server ├── Makefile # Build script for Linux, macOS, and Windows (with MSYS2) ├── README.md # This guide ├── client.cpp # The client-side C++ code └── server.cpp # The server-side C++ code

How to Build and Run
Build on Linux or macOS

You must have g++ and make installed.

Open a terminal in the project directory.

Compile the code:

make

This will create two executables in a new build/ directory: server and client.

Run the server:

./build/server

Open a new terminal and run the client:

./build/client

Build on Windows

Compiling C++ socket code on Windows is easiest in a Linux-like environment. The recommended way is to use MSYS2.

Install MSYS2: Download and run the installer from msys2.org.

Open the MSYS2 MINGW64 Terminal (from your Start Menu).

Install build tools: Run the following command to install g++ and make:

pacman -S mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-make

Navigate to your project directory: (e.g., if your project is at C:\Users\YourName\FileShareApp_CPP)

cd /c/Users/YourName/FileShareApp_CPP

Compile the code:

make

This will create two executables in build/: server.exe and client.exe.

Run the server:

./build/server.exe

Open a new MSYS2 terminal and run the client:

./build/client.exe

How to Use the Application
Once the server is running, the client will connect and ask for a username and password.

Username: user

Password: pass123

(You can change these in server.cpp.)

Once authenticated, you can use these commands in the client terminal:

list - Show files on the server.

download [filename] - Download a file (e.g., download test1.txt).

upload [filename] - Upload a file from your client_files folder (e.g., upload doc.pdf).

quit - Disconnect from the server.

Dockerize the Server (Optional)
This step packages your server into a self-contained Linux container.

Install Docker Desktop.

Open a terminal in your project directory.

Build the container image:

docker build -t fileshare-server .

Run the container:

docker run -p 9999:9999 -d --name my-server fileshare-server

-p 9999:9999 maps your computer's port 9999 to the container's port 9999.

-d runs it in detached (background) mode.

--name my-server gives your container an easy name.

Your C++ server is now running inside a container. You can connect to it using your local C++ client (./build/client or client.exe) because it's running on 127.0.0.1:9999.
