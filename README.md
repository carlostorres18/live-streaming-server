# 🚀 Stream-It-Yourself: A Beginner's Live Streaming Server Guide
A personal project to build a minimal Twitch.tv-like streaming service using **RTMP** and **HLS**.

## 📝 Project Overview

This project serves as a hands-on guide and educational tool to understand the fundamentals of live video streaming. We demonstrate how audio and video data are captured, encoded, delivered through a server, and finally displayed on a webpage.

My motivation is rooted in my interest in video games and the desire to understand the technology behind platforms I frequently use, such as Twitch.tv. This repository is primarily a learning tool to explore the inner workings of a modern streaming website.

---

## 📡 Streaming Technology Explained

The core of this project relies on two key streaming protocols: **RTMP** for ingestion and **HLS** for delivery. 

### 1. Ingestion: Real Time Messaging Protocol (RTMP)

RTMP is the protocol used to push the live stream from the encoder (like OBS) to the server.

* **What it is:** A live video streaming technology for transferring data over the internet.
* **How it works:** Data is broken down into small, quickly transferable **data packets** by an encoder, sent to the server, and then reassembled for viewing.
* **Why use it?**
    * **Low-Latency:** Still a good option for minimal stream delay.
    * **Simplicity:** Easy to set up for the first-mile delivery.
    * **Security:** Supports **RTMPS** (a more secure version).
    * **Connection:** Maintains constant contact between the server and the video player.

> **Note:** Due to its deep ties with the now-deprecated Adobe Flash, RTMP is now primarily used for **stream ingestion** (the first-mile delivery), not the final delivery to the viewer.

### 2. Delivery: HTTP Live Streaming (HLS)

HLS is the protocol used to deliver the stream from the server to the end-viewer's browser.

* **What it is:** An adaptive streaming protocol developed by Apple.
* **How it works:** The server breaks the incoming RTMP stream into small, downloadable **HTTP-based files** (usually `.ts` segments and a `.m3u8` playlist). The client device then loads and plays these segments back as a video.
* **Key Advantage: Adaptive Bitrate Streaming (ABS):** HLS automatically adjusts the video quality (increase or decrease) based on the viewer's network connection, ensuring uninterrupted playback.
* **Universal Support:** Since it uses standard HTTP, it is supported by virtually all internet-connected devices.

### 🛠️ The Live Streaming Workflow (Simplified)

1.  **Video Capture:** Camera and mic capture audio and video.
2.  **Encoding (OBS):** The encoder processes the raw data, applies compression, and breaks it down into RTMP data packets.
3.  **Server Ingestion (RTMP):** The streaming server receives the packets via the **Stream URL** and **Stream Key**. 
4.  **Server Processing (HLS Conversion):** The server converts the incoming RTMP stream into HLS segments. 
5.  **Playback:** The viewer's browser requests and plays the HLS segments from the server.

---

## ⚙️ Getting Started

### Prerequisites

You will need the following software installed:

1.  **Docker Desktop** (with WSL2/Ubuntu setup on Windows)
    * [Link: https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
2.  **OBS Studio (Open Broadcaster Software)**
    * The free, open-source encoder used to send the stream.
    * [Link: https://obsproject.com/download](https://obsproject.com/download)
3.  **VS Code**
    * Make sure you are running it within your **WSL/Ubuntu** environment.
    * [Link: https://code.visualstudio.com/download](https://code.visualstudio.com/download)

### Installation & Setup

1.  **Clone this repository.**
2.  **Open Docker Desktop** and ensure the engine is running.
3.  **In your terminal** (inside the project folder):
   
    ```bash
    docker-compose build
    docker-compose up
    ```

### Running the Stream

Once the server is running via `docker-compose`, follow these steps:

1.  **Open OBS Studio.**
2.  Go to **Settings** > **Stream**.
3.  Set the service to **Custom**.
    * **Server URL:** `rtmp://localhost:1935/live`
    * **Stream Key:** `test?key=supersecret`

    > **🔑 IMPORTANT:** The default stream key in this project is hardcoded in `index.html` (line 14) to `carlostorres18`. You will need to **change it to `test`** to match the key used in OBS.

4.  **Start Streaming** in OBS.
5.  **Open your browser** and navigate to: `http://localhost:8080`
6.  **Press Play** on the video player to view your live stream!



---
Here is how the program communicates to each part for the stream key and stream URL authentication:

<img width="908" height="429" alt="image" src="https://github.com/user-attachments/assets/78c5967a-4ea7-41ca-80d5-a842b37292c6" />
<br></br>

Here is how the server is able to convert the video/audio from the encoder for the stream to be seen on websites:

<img width="911" height="327" alt="image" src="https://github.com/user-attachments/assets/eab22591-297c-4f06-820c-871e7f14ad9c" />
<br></br>

Here is how the streaming website looks like when it's running:

<img width="950" height="980" alt="image" src="https://github.com/user-attachments/assets/6f2a24ff-e2d0-4a73-ba5e-0b46372de703" />

---

## 📚 References & Documentation

* [tiangolo/nginx-rtmp Docker Hub](https://hub.docker.com/r/tiangolo/nginx-rtmp/)
* [YouTube Playlist Guide on Streaming](https://www.youtube.com/playlist?list=PL7XcC35Z6WFB3L2xLVV3S4bG_Z37MqcRe)
* [RTMP Streaming Explained (Riverside Blog)](https://riverside.com/blog/rtmp-streaming)
