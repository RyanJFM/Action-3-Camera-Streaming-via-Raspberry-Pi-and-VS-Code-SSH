# Action 3 Camera Streaming via Raspberry Pi and VS Code SSH

This repository documents the setup for streaming video from the **DJI Osmo Action 3 Camera** connected to a **Raspberry Pi**, and receiving the stream on a **personal computer** using Python and OpenCV.

The system connects over a shared Wi-Fi network (In this example:- `Kira`), with the Raspberry Pi accessed via **SSH** (we SSH via VS code). The Action 3 Camera is used in **Webcam Mode** and streams video via **FFmpeg**.

---

## Contents
- Action 3 Camera connected in Webcam Mode (via USB to Raspberry Pi)  
- Raspberry Pi (running minimal Ubuntu/Debian-based OS)  
- README.md – This documentation  
- Python script for receiving video stream  

---

## 1. Connecting to Wi-Fi

Ensure both your **Raspberry Pi** and your **PC** are connected to the same Wi-Fi network:

In this exmaple:-
- **Wi-Fi Name:** `Kira`  
- **Password:** `jazz1234`

---

## 2. Preparing the Raspberry Pi

1. Connect the **Action 3 Camera** to the Raspberry Pi using a USB data cable.  
2. Put the Action 3 Camera into **Webcam Mode**.  
3. Verify that the camera is detected by checking available video devices:

   ```bash
   ls /dev/video*
---
   
After this command the vidoe ports should be appeared as vidoe0 and vidoe1.
vidoe0 used raw vidoe values and vidoe1 used compressed vidoe steam.
**Use viode0 with ffmpeg. vidoe1 resulted an error.**

## 3. SSH Access via VS Code
   
1. Open Visual Studio Code on your PC.
2. Install the extension: Remote - SSH.
3. Connect to the Raspberry Pi using:
      - Username: user (Username)
      - Password: user (Password)

## 4.Streaming the Camera Feed

On the Raspberry Pi terminal (inside VS Code), run the following command to start streaming:

 ```bash
ls /dev/video*
```
 ```bash
ffmpeg -f v4l2 -input_format mjpeg -video_size 1920x1080 -framerate 30 \
-i /dev/video0 -c:v libx264 -preset ultrafast -tune zerolatency \
-f mpegts udp://10.198.116.249:5000
```

Explanation of parameters:

1920x1080 – Resolution

30 – Frames per second

udp://10.198.116.249:5000 – Destination IP and port (replace 10.198.116.249 with your PC’s local IP address)

### 5. Receiving the Stream on the PC

On your PC, create a Python file (e.g., receive_stream.py) with the following code:
```bash
import cv2

cap = cv2.VideoCapture("udp://10.198.116.249:5000")

while True:
    ret, frame = cap.read()
    if not ret:
        print("No frame received!")
        break
    cv2.imshow("UDP Stream", frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

Run the script:

```bash
python3 receive_stream.py
```

Press q to exit the video window.

## 6. Notes

The Action 3 Camera must remain in Webcam Mode for /dev/video0 to be available.

Always replace the IP address in both FFmpeg and Python commands with your PC’s actual local IP address.

If you see Cannot open device /dev/video0, confirm the camera is in webcam mode and recheck with ls /dev/video*.

If video is laggy, try reducing resolution or frame rate in the FFmpeg command.

7. References

FFmpeg Documentation

OpenCV Python VideoCapture

VS Code Remote - SSH
