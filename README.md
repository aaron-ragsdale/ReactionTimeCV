# REACH! Reaction Game

REACH! is a 30-second webcam reaction game played by reaching toward targets on the screen. It uses browser-based hand tracking to detect your knuckles, including when you make a fist. No controller, account, or paid inference service is required.

## How to play

1. Open the game and select **Enable camera**. Allow camera access when prompted.
2. Keep both hands visible in good lighting. Choose **Standard (Mac)** or **Smooth (iPad)** before starting the camera.
3. Select **Start game**. Reach into green circles with either hand's knuckles or a closed fist.
4. Avoid touching red circles. Use **Full Screen** for a larger play area and **Show hands** to display hand landmarks.
5. Review the score and optionally download the session's event data as a CSV.

## Game mechanics

- **Green dots:** Earn 100–1,000 points based on how quickly you reach each dot. They last about 1.4–1.95 seconds.
- **Red dots:** Cost 300 points when touched. They last about 0.8–1.2 seconds.
- **Timing:** Targets appear unpredictably, with occasional bursts and pauses.
- **Crowding:** At most two green dots and one red dot appear at once.
- **Hit detection:** The four MCP knuckles (hand landmarks 5, 9, 13, 17) and their estimated center can trigger hits. Green targets have more forgiving hit tolerance than red targets.
- **Misses:** Expired green targets count as misses, without a score deduction.
- **Duration:** Each round lasts 30 seconds.

## Troubleshooting

- **Camera doesn't start:** Check browser camera permissions and use the HTTPS GitHub Pages site.
- **Hands are missing or jittery:** Improve lighting, move far enough back to keep both hands visible, and avoid moving them out of frame.
- **iPad performance is slow:** Try **Smooth (iPad)** before enabling the camera. If GPU tracking is unreliable, refresh and test **CPU**.
- **Hits are not registering:** Keep your knuckles visible to the camera; very fast movement or occlusion can temporarily reduce accuracy.
- **Game looks outdated:** Reload or refresh the page to get the latest version.

## Privacy

Camera frames are processed on your device using MediaPipe Hand Landmarker. The site downloads the model and runtime files when needed, but the game does not upload camera frames. Session data is downloaded locally only when you choose CSV export.
