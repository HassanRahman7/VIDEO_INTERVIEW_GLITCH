# Video Interview Glitch

Say **"ummm"** on camera and your video feed glitches like your internet connection just dropped: it freezes, gets choppy, blocky, and then recovers on its own. This is designed to buy you a few extra seconds to think during a difficult question on a video call.


## Local Setup & Testing

1. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Run the application:
   ```bash
   python um_glitch.py
   ```

A window will open displaying your webcam feed. Say "ummm" (hold it for half a second) and watch the feed break.

### Keyboard Controls

| Key | Action |
| :--- | :--- |
| `space` | Trigger the glitch manually |
| `d` | Show the detector's debug numbers |
| `q` / `esc` | Quit the application |

## How to use in Google Meet / Zoom (OBS Virtual Camera)

Video conferencing applications cannot directly read the Python desktop window as a camera source. You must use OBS Studio to route the OpenCV window into a virtual webcam driver.

1. **Install OBS Studio:** Download and install OBS Studio. This automatically installs the necessary Virtual Camera driver on your system.
2. **Run the Script:** Execute `python um_glitch.py`. Leave the "um glitch" window open and visible on your screen.
3. **Capture the Window in OBS:**
   * Open OBS. In the **Sources** box (bottom left), click the **+** icon and select **Window Capture**.
   * In the **Window** dropdown, select your Python application (e.g., `[python.exe]: um glitch`).
   * *If the preview is black:* Click **Properties**, change the **Capture Method** to **Windows 10 (1903 and up)**, and uncheck **Capture Cursor**. Click **OK**.
   * *If the window doesn't fill the screen:* Right-click the video feed in OBS, go to **Transform**, and click **Fit to screen**.
4. **Start the Virtual Camera:** Click **Start Virtual Camera** in the bottom-right Controls panel of OBS.
5. **Connect to your Call:** Open Google Meet or Zoom, go to **Settings > Video**, and change your Camera to **OBS Virtual Camera**.

> ⚠️ **CRITICAL:** For your keyboard controls (`space`, `d`, `q`) to work during a live meeting, the Python OpenCV window must be the active, focused window on your computer. If you click into Google Meet or OBS, your keystrokes will not register.

## Tuning the Detector

Microphone quality and room noise vary. If the script behaves poorly, press `d` to view the live debug numbers on your feed and adjust the constants in the `SETTINGS` block at the top of `um_glitch.py`:

* **Normal talking triggers it:** Lower the `FLUX` value.
* **Your "ums" are ignored:** Raise `FLUX` slightly, or lower `VOICED`.
* **Change the glitch duration:** Modify the `DROP` value.
