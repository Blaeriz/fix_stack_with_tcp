# FIX Protocol Stack with TLS & AES-256-GCM

A modular C++ implementation of the FIX 4.2 protocol featuring transport-layer security (TLS 1.3) and application-layer payload encryption (AES-256-GCM).

## Prerequisites

- **C++:** GCC/Clang (C++17), CMake
- **Security:** OpenSSL 3.x
- **Simulator:** Python 3.11+, `uv`

## 1. Build the Server (Exchange)

```bash
mkdir build && cd build
cmake ..
make
cd ..
```

## 2. Generate Security Certificates

```bash
mkdir -p certs
openssl req -x509 -newkey rsa:4096 -keyout certs/key.pem -out certs/cert.pem -days 365 -nodes -subj "/CN=localhost"
```

## 3. Run the Demonstration

**Terminal 1: Start the Exchange**
```bash
./build/main_server
```

**Terminal 2: Start the Client Simulator**
```bash
cd simulator
uv run python client.py
```

## Features

- **FIX Engine:** Session management, sequence numbers, and heartbeat logic.
- **Security:** 
    - **TLS:** Mandatory transport encryption via OpenSSL.
    - **AES-GCM:** Optional authenticated payload encryption (pre-shared 256-bit key).
- **Simulator:** Python-based driver using `simplefix` for automated order flow.
