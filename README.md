# IP-Multicast-Live-Streaming

This repository contains an Internet TV/Radio application implemented using the multicast IP `ASM (Any Source Multicast)` model in `C`. This project was developed as part of CSE330 (Computer Networks) on October 2019. The live streaming service can be deployed on any LAN (WLAN/Ethernet), provided the server and clients are on the same network.

The project utilizes two different transport layer protocols: TCP/IP and UDP, for distinct types of communication. TCP is used for fetching the radio list, and UDP is used for streaming services.

## Installation & Dependencies

This project relies on several `GUI` and `VLC` plugins to display the continuously received video stream. Make sure you install VLC using the `apt` package manager rather than `snap`.

### Prerequisites

- **VLC Media Player:**  
  Install VLC via `apt`:
  ```bash
  sudo apt install vlc
  ```
  **Note:** If VLC is installed via `snap`, uninstall it and install via `apt`.

- **Server File:**  
  Requires `ffmpeg` for streaming media:
  ```bash
  sudo apt install ffmpeg
  ```

- **Client File:**  
  The client uses `GTK2` for the GUI and `libvlc` for embedding the VLC window in the GUI.

  - GTK3:  
    ```bash
    sudo apt install libgtk-3-dev
    ```

  - GTK2:  
    ```bash
    sudo apt install libgtk2.0-dev
    ```

  - libvlc:  
    ```bash
    sudo apt install libvlc-dev
    ```

## Usage

**Before running the application, convert an existing audio/video file (any format) to a streamable format (preferably MP4) using `ffmpeg`:**
```bash
ffmpeg -i inputfile.mp4 -f mpegts streamable_output.mp4
```

### Compile the Code

To compile both server and client:
```bash
make
```

Alternatively, compile them individually:

- **Server:**
  ```bash
  gcc iserver.c -o server -lpthread
  ```

- **Client:**
  ```bash
  gcc -o guiclient guiclient.c `pkg-config --libs gtk+-2.0 libvlc` `pkg-config --cflags gtk+-2.0 libvlc`
  ```

### Run the Application

- **Server:**
  ```bash
  ./server
  ```

- **Client:**
  ```bash
  sudo ./guiclient
  ```
  `sudo` is required to access the network interface for multicast IP.

## Project Objective

The main objective of this project is to gain insights into multimedia traffic, particularly video traffic, which is expected to drive mobile data traffic growth. This Internet TV/Radio application uses multicast to stream media. The project covers the following key concepts:

- Sending data over a TCP connection.
- Sending multimedia data over UDP.
- Structuring data to ensure inter-operability between differently implemented applications on various platforms.

This project implements the `Any Source Multicast (ASM)` model, where multicast messages are identified by the multicast group address alone, allowing multiple senders to exist in the same group.

## GTK+ 3

For more details about GTK+ 3, visit the official documentation at:  
[GTK+ 3 Documentation](https://developer.gnome.org/gtk3/stable/)
