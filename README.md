# 🚀 Deep Packet Inspection (DPI) Engine

A **multi-threaded Deep Packet Inspection (DPI) engine** built in **C++17** that analyzes network traffic from PCAP files, identifies applications such as **YouTube, GitHub, Facebook, Google**, and applies custom blocking rules to generate a filtered PCAP along with detailed traffic statistics.

---

# 📌 What is Deep Packet Inspection?

Imagine a **security checkpoint at an airport**.

- A normal checkpoint only checks **who is entering**.
- A smart security system also checks **where they're going, what they're carrying, and whether they should be allowed inside**.

A **DPI Engine** works the same way for network traffic.

Instead of only looking at IP addresses and ports, it looks deeper into the packet to identify the actual application (YouTube, GitHub, Facebook, etc.) and decides whether to **allow** or **block** the traffic.

---

# 🌍 Real World Applications

This technology is commonly used in:

- 🏢 Enterprise Firewalls
- 🌐 ISP Traffic Management
- 🔐 Cybersecurity Appliances
- 👨‍👩‍👧‍👦 Parental Control Systems
- 📊 Network Monitoring & Analytics

---

# ⚙️ How the Engine Works

```text
                 Input PCAP File
                       │
                       ▼
               Read Network Packets
                       │
                       ▼
             Parse Network Headers
                       │
                       ▼
        Detect Application (DPI Engine)
        (YouTube, GitHub, DNS, HTTPS...)
                       │
                       ▼
             Apply Blocking Rules
        (Application / Domain / IP)
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        Forward Packet      Drop Packet
             │
             ▼
         Output PCAP File
```

---

# 💡 Real World Analogy

Think of a supermarket.

Instead of one cashier handling every customer, customers are distributed across multiple checkout counters.

The same idea is used here.

```text
               Customers
                    │
                    ▼
              Queue Manager
              (Load Balancer)
             ╱      │      ╲
            ▼       ▼       ▼
       Counter1 Counter2 Counter3
       (Fast Paths / Worker Threads)
             │
             ▼
          Exit Counter
```

This significantly improves processing speed for large network captures.

---

# ✨ Features

- Multi-threaded Packet Processing
- Deep Packet Inspection (DPI)
- Ethernet, IPv4, TCP & UDP Parsing
- TLS SNI Extraction
- HTTP Host Detection
- Application Identification
- Rule-based Packet Blocking
- Connection (Flow) Tracking
- Packet Statistics
- Filtered PCAP Generation

---

# 📦 Supported Applications

- YouTube
- GitHub
- Google
- Facebook
- Instagram
- TikTok
- Discord
- Telegram
- Spotify
- Zoom
- Amazon
- Apple
- Cloudflare
- HTTP
- HTTPS
- DNS

---

# 🧩 Project Architecture

```text
                 PCAP Reader
                      │
                      ▼
             Packet Parser
                      │
                      ▼
          Application Detection
          (SNI / HTTP Host Parsing)
                      │
                      ▼
               Rule Engine
       (App / Domain / IP Blocking)
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
      Forward Packet         Drop Packet
          │
          ▼
   Generate Output PCAP
          │
          ▼
    Statistics & Reports
```

---

# ⚡ Multi-threaded Processing

```text
                 Reader Thread
                      │
                      ▼
             Load Balancer Threads
               ┌─────────────┐
               ▼             ▼
         Fast Path 1    Fast Path 2
               ▼             ▼
         Fast Path 3    Fast Path 4
               └──────┬──────┘
                      ▼
              Output Writer Thread
```

Each packet is assigned to a worker using a hash of its **Five-Tuple**, ensuring packets belonging to the same connection are always processed by the same worker thread.

---

# 🛠️ Tech Stack

### Language

- C++17

### Concepts

- Multi-threading
- Producer-Consumer Pattern
- Thread-safe Queues
- Mutex
- Condition Variables
- Hashing
- Flow Tracking

### Networking

- Ethernet
- IPv4
- TCP
- UDP
- TLS
- HTTP

---

# 📂 Project Structure

```text
packet_analyzer/

├── include/
│   ├── packet_parser.h
│   ├── pcap_reader.h
│   ├── sni_extractor.h
│   └── types.h
│
├── src/
│   ├── dpi_mt.cpp
│   ├── packet_parser.cpp
│   ├── pcap_reader.cpp
│   ├── sni_extractor.cpp
│   └── types.cpp
│
├── test_dpi.pcap
└── README.md
```

---

# 🚀 Build

```bash
g++ -std=c++17 -pthread -O2 -I include \
-o dpi_engine \
src/dpi_mt.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp
```

---

# ▶️ Run

Analyze a PCAP file:

```bash
./dpi_engine input.pcap output.pcap
```

Block specific applications or domains:

```bash
./dpi_engine input.pcap output.pcap \
--block-app YouTube \
--block-app TikTok \
--block-domain facebook \
--block-ip 192.168.1.50
```

---

# 📊 Sample Output

```text
Packets Processed : 77
Forwarded         : 69
Dropped           : 8

Detected Applications

HTTPS
GitHub
YouTube
Google
Facebook
Discord
Spotify
TikTok
...
```

---

# 🎯 Future Enhancements

- Live Packet Capture
- HTTP/3 (QUIC) Support
- Real-time Traffic Dashboard
- AI-assisted Traffic Classification
- Threat Detection
- Intrusion Detection Rules

---

# 👩‍💻 Author

**Aashi Singh**

If you found this project useful, consider ⭐ starring the repository!
