# High-Performance C TCP Multi-Client Chat Server

A lightweight, high-performance concurrent TCP chat application written in C. This project utilizes non-blocking I/O multiplexing (`select()`) on the server side to efficiently handle multiple client connections simultaneously, paired with a multi-threaded C client interface (`pthread`).

---

## Key Features & Capabilities

- **I/O Multiplexing with `select()`**: The server dynamically handles up to `MAX_CLIENTS` concurrent connections without creating a separate thread for every incoming connection, reducing overhead.
- **Multithreaded Client Architecture**: The client utilizes POSIX threads (`pthread`) to continuously listen for incoming broadcast messages in the background while keeping user input responsive.
- **Real-Time Message Broadcasting**: Messages sent by any connected client are instantly forwarded to all other active participants on the server.
- **Dynamic Connection Management**: Automatic detection and cleanup of disconnected clients without interrupting active sessions.
- **Built-in Build System**: Includes a lightweight `Makefile` for quick compilation, building, and cleanup.

---

##  Project Architecture

```
         +------------------+
         |   C TCP Server   |
         |  (select() loop) |
         +--------+---------+
                  |
    +-------------+-------------+
    |             |             |
+---v----+    +---v----+    +---v----+
| Client |    | Client |    | Client |
| (Peer) |    | (Peer) |    | (Peer) |
+--------+    +--------+    +--------+
```

---

##  Quick Start

### Prerequisites
- GCC Compiler (`gcc`)
- POSIX-compliant environment (Linux, macOS, WSL)
- Make utility (`make`)

### 1. Clone the Repository
```bash
git clone https.github.com/your-username/c-tcp-multiclient-chat.git
cd c-tcp-multiclient-chat
```

### 2. Build the Executables
Use the included Makefile to compile both the server and client binaries:
```bash
make
```
make file may fail. So for manual compiling of client run this command ```gcc client.c -o client -pthread```

### 3. Run the Application

#### Start the Server:
```bash
./server
```
*(Server listens by default on port `8888`)*

#### Connect Clients:
Open separate terminal windows or run on separate machines and start clients:
```bash
./client
```

---

##  Potential Enhancements & How to Improve It

Want to contribute or extend this project? Here are some great starting points:

1. **User Authentication & Nicknames**: 
   - Add a handshake protocol allowing clients to set custom usernames instead of broadcasting plain raw text.
2. **Private Messaging (Direct Messages)**:
   - Implement custom command syntax like `/msg <username> <message>` for 1-on-1 private conversations.
3. **SSL/TLS Encryption**:
   - Wrap standard TCP socket operations in OpenSSL or `mbedtls` for end-to-end secure communication.
4. **Epoll / Kqueue Upgrade**:
   - Upgrade the server event loop from `select()` to `epoll` (Linux) or `kqueue` (BSD/macOS) for $O(1)$ scaling capability to handle thousands of concurrent connections.
5. **Room/Channel Management**:
   - Allow users to join, create, or leave specific chat rooms (`/join #room_name`).

---

## Future Vision: Where This Can Reach

- **Microservice Message Broker**: Expand this into a lightweight, custom high-throughput pub/sub message broker or IPC (Inter-Process Communication) layer for distributed microservices.
- **Cross-Platform GUI Client**: Build a modern graphical user interface using **Qt**, **GTK**, or a Web frontend via WebSockets.
- **Embedded / IoT Communications**: Due to its minimal memory footprint and zero external dependencies, this architecture is ideal for resource-constrained IoT edge devices communicate status updates and telemetry data.

---

## Makefile Commands

| Command | Action |
| :--- | :--- |
| `make` / `make all` | Compiles both `server` and `client` binaries with `-Wall -pthread` |
| `make server` | Compiles only the server executable |
| `make client` | Compiles only the client executable |
| `make clean` | Removes compiled binary files |

---

## Contributing

Contributions are welcome! Feel free to open an Issue or submit a Pull Request to help refine the code or add new features.

---

## License
Created by the Runes Room Community pushed by Runea Saga (The Learners offer) in Uganda, Africa.
This project is open-source and available under the [MIT License](LICENSE).
