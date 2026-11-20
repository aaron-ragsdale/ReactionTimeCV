# REACH! Browser Pose Reaction Game

A no-backend, GitHub Pages-compatible webcam reaction game. MediaPipe Pose Landmarker Lite estimates body landmarks locally in the user's browser. The player touches green targets with either wrist to score points.

## Test on your Intel Mac

No Python virtual environment, Node, PyTorch, or API key is required.

```bash
cd pose-reaction-game
python3 -m http.server 8000
```

Open `http://localhost:8000`, click **Enable camera**, allow camera access, then click **Start game**. If you don't already have Python 3, you can install it, or simply upload `index.html` to GitHub Pages and test there.

## Publish to GitHub Pages

1. Create a public GitHub repository named `pose-reaction-game` (or name it `<your-username>.github.io` for a user site).
2. Upload `index.html` to the repository root, commit it.
3. Under **Settings > Pages**, select **Deploy from a branch**, branch `main`, folder `/(root)`, and save.
4. Visit `https://<your-username>.github.io/pose-reaction-game/`, or `https://<your-username>.github.io/` if you used the username repository name.
5. In the browser, allow camera access. GitHub Pages serves HTTPS, as required by webcam APIs.

## How scoring works

- 30-second session
- Green targets appear after a 600 ms delay and expire after 2.4 seconds.
- A hit is detected when a tracked wrist **enters** the target circle after a 160 ms spawn grace period.
- Misses are targets that expire without a detected hit.
- Average reaction time uses successful target hits (from target spawn to detection).
- Download CSV includes outcome, detected wrist, elapsed reaction time and screen-space target coordinates.

This is a first prototype, not a validated measurement instrument. Reaction times include camera capture, model inference and display latency. Pose landmarks are not actual physical contact sensors. Touches are defined in 2D image space and can be fooled by depth or occlusion. For higher precision, consider MediaPipe Hand Landmarker, wrist motion velocity, 3D calibration and controlled latency testing.

## Privacy and costs

Your webcam frames are processed on the device and this app does not upload video. The app initially fetches the MediaPipe library, WebAssembly runtime and model from public CDNs/Google-hosted model storage; they may be cached by the browser. There is no API key, backend or paid inference. Hosting on GitHub Pages is free within GitHub's applicable usage limits.

## Optional local asset hosting

To make the model file a repository asset, download it:

```bash
mkdir -p models
curl -L 'https://storage.googleapis.com/mediapipe-models/pose_landmarker/pose_landmarker_lite/float16/1/pose_landmarker_lite.task' -o models/pose_landmarker_lite.task
```

Then change the `MODEL` constant in `index.html` to `./models/pose_landmarker_lite.task` and commit the model to your repository. The MediaPipe JavaScript and WASM runtime will still be loaded from jsDelivr, so this is not a fully offline app. You can vendor those assets in a later iteration for offline or restricted-network deployments.

## Model and implementation

MediaPipe Tasks Vision `@mediapipe/tasks-vision@0.10.22`, Pose Landmarker Lite, GPU delegate preferred with CPU fallback. Rendering and game logic use HTML canvas plus native JavaScript.
