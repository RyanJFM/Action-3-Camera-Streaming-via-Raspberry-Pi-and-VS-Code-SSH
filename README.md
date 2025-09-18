# Action 3 Camera Streaming via Raspberry Pi and VS Code SSH

This repository documents the setup for streaming video from the **DJI Osmo Action 3 Camera** connected to a **Raspberry Pi**, and receiving the stream on a **personal computer** using Python and OpenCV.

The system connects over a shared Wi-Fi network (`Kira`), with the Raspberry Pi accessed via **VS Code SSH**. The Action 3 Camera is used in **Webcam Mode** and streams video via **FFmpeg**.

---

## Contents
- Action 3 Camera connected in Webcam Mode (via USB to Raspberry Pi)  
- Raspberry Pi (running Ubuntu/Debian-based OS)  
- README.md – This documentation  
- Python script for receiving video stream  

---

## 1. Connecting to Wi-Fi

Ensure both your **Raspberry Pi** and your **PC** are connected to the same Wi-Fi network:

- **Wi-Fi Name:** `Kira`  
- **Password:** `jazz1234`

---

## 2. Preparing the Raspberry Pi

1. Connect the **Action 3 Camera** to the Raspberry Pi using a USB data cable.  
2. Put the Action 3 Camera into **Webcam Mode**.  
3. Verify that the camera is detected by checking available video devices:

   ```bash
   ls /dev/video*

## 3. SSH Access via VS Code

1. Open Visual Studio Code on your PC.
2. Install the extension: Remote - SSH.
3. Connect to the Raspberry Pi using:
      @ Username: user
      @ Password: user

