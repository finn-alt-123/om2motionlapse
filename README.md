# OM2 Motionlapse

A free webapp that drives a DJI Osmo Mobile 2 over Bluetooth for motion-lapses, replacing the abandoned DJI GO app. Everything is in one file: `index.html`.

## 1. Put it online (once, free)

Web Bluetooth and the camera only work on an `https://` page, so the file needs hosting:

- **GitHub Pages:** create a public repo, upload `index.html`, then Settings → Pages → Deploy from branch `main`. You get `https://<you>.github.io/<repo>/`.
- **Netlify Drop:** drag the folder with `index.html` onto app.netlify.com/drop.

## 2. Pick a browser

| Device | Browser |
|---|---|
| iPhone / iPad | **Bluefy – Web BLE Browser** (free, App Store). Safari and Chrome on iOS have no Bluetooth for web pages. |
| Android | Chrome |
| Laptop (Windows, Mac, Linux) | Chrome or Edge |

Don't pair the gimbal in the phone's Bluetooth settings. Switch it on, tap **Connect gimbal** and pick it from the list. If it doesn't show up, enable *Settings → Show all Bluetooth devices*.

## 3. Two ways to shoot

### A. iPhone Camera app records (best quality) — needs a second device
The iPhone on the gimbal records with its own Camera app in **Time-lapse** mode. The webapp runs on a **second device** (laptop, Android phone, iPad) and moves the gimbal smoothly.
One iPhone can't do both: iOS pauses web pages as soon as the Camera app is in front, and a web page isn't allowed to start the Camera app's recording.

1. Aim tab: jog the gimbal (or tap the map), **Add keyframe** at the start, then at the end (up to 5 points). **Preview path** runs it quickly.
2. Shoot tab → *iPhone Camera app*: set the move duration in seconds (e.g. 600 for 10 min; 0 = as fast as the gimbal allows), the countdown and the hold.
3. iPhone: Camera app → Time-lapse. Press **Start move** on the controller; the gimbal goes to keyframe 1, counts down — tap record — then glides to the last keyframe. Stop recording when it says Done.

Tip: slow moves look best. 0.05–0.2°/s is typical for a 10–30 min time-lapse; the Shoot tab shows the speed.

### B. This browser records — single phone
Open the webapp in Bluefy on the phone that's on the gimbal. Choose *This browser*, start the camera, set interval and frame count. It moves → waits to settle → takes a frame, repeated. Frames are saved on the phone as they're taken; the **Library** tab turns them into an MP4 (Save / Share → Save Video puts it in Photos) or a ZIP of JPEGs. Image quality is limited to what the browser's camera stream gives (up to 4K on recent iPhones), and iOS may not allow exposure lock, so some flicker is possible.

## 4. If the gimbal behaves oddly

This uses a community-documented protocol (github.com/alkersan/om-research, tested on OM2/OM3/OM4). It hasn't been tuned on every unit, so:

- **Moves the wrong way:** Settings → invert pan / tilt.
- **Want faster moves:** Settings → Speed limit. The default is the OM2's rated 120°/s; higher values are allowed, but the motors may not keep up.
- **Drifts back to center or jumps to odd positions:** Settings → Move commands → *Relative steps*.
- **Weird angles after you used the gimbal's own joystick:** tap **●** (center) or **Sync to gimbal**.
- The **Log** panel at the bottom (with *Show raw Bluetooth packets*) shows exactly what's sent and received.

No gimbal handy? Tap **Simulator** to try the whole flow.
