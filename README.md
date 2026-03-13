<p align="center">
    <img src="https://raw.githubusercontent.com/ferranpons/llamatik/main/assets/llamatik-new-logo.png" alt="Llamatik Logo" width="120"/>
</p>

<p align="center">
    <b>Remote inference backend for the Llamatik ecosystem.</b>
</p>
<p align="center">
Ktor · Kotlin/JVM · llama.cpp-compatible API · Drop-in remote inference
</p>
<p align="center">
    <img src="https://img.shields.io/badge/Kotlin-JVM-blueviolet" />
    <img src="https://img.shields.io/badge/Ktor-Server-ff4088" />
    <img src="https://img.shields.io/badge/LLM-llama.cpp-orange" />
    <img src="https://img.shields.io/badge/License-MIT-lightgrey" />
</p>

------------------------------------------------------------------------

## ✨ What is Llamatik Server?

**Llamatik Server** is a lightweight HTTP backend that exposes the
**same API as the Llamatik Kotlin library**, enabling seamless remote
inference.

It allows you to:

-   🧠 Run LLM inference remotely
-   🌐 Switch from on-device to server inference with no API changes
-   🚀 Deploy scalable inference backends
-   🔁 Build hybrid offline-first applications with online fallback

If you're using **Llamatik** in your app, this server acts as a
**drop-in remote backend**.

------------------------------------------------------------------------

## 🧱 Architecture

    Your App
    │
    ▼
    LlamaBridge (shared Kotlin API)
    │
    ├─ llamatik-core     → On-device inference (llama.cpp, whisper.cpp, SD)
    ├─ llamatik-client   → Remote HTTP client
    └─ llamatik-server   → This backend

Switching between **local and remote inference requires no API changes**
---\
only configuration.

------------------------------------------------------------------------

## 🚀 Features

-   ✅ Implements the same API contract as Llamatik
-   ✅ Compatible with llama.cpp-based inference
-   ✅ Streaming & non-streaming generation
-   ✅ JSON schema-constrained generation
-   ✅ Embeddings support
-   ✅ Production-ready Ktor server
-   ✅ Docker-ready deployment

------------------------------------------------------------------------

## 🛠 Requirements

-   JVM **21+**
-   Docker (optional, for containerized deployment)

------------------------------------------------------------------------

# ▶️ Running Locally

From the project root:

``` bash
./gradlew run
```

The server will start on:

    http://localhost:8080

------------------------------------------------------------------------

# 🐳 Running with Docker

Build the image:

``` bash
docker build -t llamatik .
```

Run the container:

``` bash
docker run -p 8080:8080 llamatik
```

------------------------------------------------------------------------

# 🖥 Running as a Linux Service (systemd)

Create:

    /etc/systemd/system/docker.llamatik.service

``` ini
[Unit]
Description=Llamatik
After=docker.service
Requires=docker.service

[Service]
TimeoutStartSec=0
Restart=always
ExecStartPre=-/usr/bin/docker exec %n stop
ExecStartPre=-/usr/bin/docker rm %n
ExecStart=/usr/bin/docker run -p 8080:8080 llamatik

[Install]
WantedBy=default.target
```

Enable on boot:

``` bash
sudo systemctl enable docker.llamatik
```

Control manually:

``` bash
sudo service docker.llamatik stop
sudo service docker.llamatik start
```

------------------------------------------------------------------------

# 🔄 Hybrid Mode (Local + Remote)

Llamatik is designed for **offline-first apps**.

You can:

-   Run inference locally (llama.cpp via Kotlin/Native)
-   Fallback to this server when needed
-   Switch dynamically based on connectivity

------------------------------------------------------------------------

# 🌍 Production Deployment

For production usage you should:

-   Add HTTPS (via reverse proxy like Nginx or Caddy)
-   Use container orchestration (Docker Compose / Kubernetes)
-   Configure resource limits
-   Add authentication if exposed publicly

Example architecture:

    Internet
       │
    Reverse Proxy (TLS)
       │
    Llamatik Server (Docker)
       │
    llama.cpp runtime

------------------------------------------------------------------------

# 📦 Related Projects

-   🔗 **Llamatik Library** -- Kotlin Multiplatform AI SDK\
    https://github.com/ferranpons/llamatik

------------------------------------------------------------------------

# 🤝 Contributing

Contributions are welcome: - Performance improvements - Deployment
enhancements - Documentation updates

Open an issue or PR 🚀

------------------------------------------------------------------------

# 📜 License

This project is licensed under the MIT License.\
See LICENSE for details.

------------------------------------------------------------------------

Built with ❤️ for the Kotlin & AI community.
