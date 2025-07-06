# Hand Gesture Controlled Virtual Drone

This project enables control of a **virtual drone** (and optionally a real drone, e.g. Tello) using hand gestures captured by a webcam. It performs real-time hand segmentation, gesture recognition, and translates those gestures into drone actions. The virtual drone simulator is built with Pygame.

---

## Features

* **Real-Time Hand Segmentation:** Uses computer vision (OpenCV) to segment the hand from the background, even under changing lighting conditions.
* **Gesture Recognition:** Detects and classifies gestures such as *left*, *right*, *up*, *down*, *forward*, and *picture*.
* **Drone Simulation:** A Pygame-based 2D drone responds to gestures for movement and rotation.
* **Threaded Architecture:** Vision and simulation run in parallel for real-time response.
* **Extensible:** Code is modular and prepared for real drone (DJITelloPy) integration.

---

## File Structure

| File                  | Description                                              |
| --------------------- | -------------------------------------------------------- |
| `black_seg_hand.py`   | Hand segmentation, skin detection, ROI, and tracking.    |
| `clean_hand_final.py` | HSV mask adjustment and object isolation helpers.        |
| `get_action_final.py` | Gesture detection and mapping gestures to drone actions. |
| `virtual_drone.py`    | The Pygame-based virtual drone simulator and main entry. |

---

## Requirements

* **Python 3.7+**
* `opencv-python`
* `numpy`
* `pygame`
* `scikit-image` (for advanced metrics, optional)

**Install all dependencies:**

```sh
pip install opencv-python numpy pygame scikit-image
```

---

## How to Run

1. **Clone or download the project.**
   Place all files in the same directory.

2. **Connect a webcam** to your computer.

3. **Run the main simulator:**

   ```sh
   python virtual_drone.py
   ```

   * Two windows will appear:

     * Webcam hand detection and gesture interface.
     * Virtual drone simulator (Pygame window).

4. **Control the drone with hand gestures:**

   * Place your hand in the webcam's view.
   * Use the following gestures:

     * **Move Forward**: Open palm (forward-facing hand).
     * **Rotate Left/Right**: Point left/right.
     * **Move Up/Down**: Point up/down (changes drone size in sim).
     * **Take Picture**: OK gesture (detects two fingers at the top).
   * The drone will respond after a short stabilization period (for robust gesture detection).

5. **Quit:**

   * Press **Q** in the webcam window, or close the Pygame window.

---

## How it Works (Technical Summary)

1. **Hand Segmentation (`black_seg_hand.py`):**

   * Segments hand using HSV color filtering, Gaussian modeling, and post-processing.
   * Tracks hand position using bounding boxes and Kalman filter.

2. **HSV Fine-Tuning (`clean_hand_final.py`):**

   * Interactive window to adjust HSV thresholds for your hand/lighting.
   * (Use this if segmentation is unreliable.)

3. **Gesture Recognition (`get_action_final.py`):**

   * Detects direction and shape of the hand contour.
   * Maps gestures to drone actions using a histogram-based voting system for stability.

4. **Drone Simulator (`virtual_drone.py`):**

   * Draws and animates a drone based on received commands.
   * Communicates with the gesture detection via thread-safe variables.
   * (Optionally, supports real drone control—commented code for Tello.)

---

## Troubleshooting

* **Bad hand detection?**

  * Make sure you have good lighting and a simple background.
  * Adjust the HSV thresholds by running the function in `clean_hand_final.py`.

* **No webcam detected?**

  * Check that your webcam is connected and not used by another application.

* **Dependencies not found?**

  * Run `pip install` as shown above.

---

## Credits & License

* Project by Roee Shamoon, Amit Busani, Amit Ahroni and Roi Grief
* Uses OpenCV, Pygame, NumPy, scikit-image
* For research, learning, and demonstration purposes.
* **MIT License** (change if needed).

---

## Extending

* Add more gestures by editing `get_action_final.py`.
* Plug in a real drone (DJITelloPy) by uncommenting and using the provided drone interface in `virtual_drone.py`.

---

## Contact

For questions, improvements, or collaboration, open an issue or contact \[[shahmoonroey@gmail.com](mailto:your-email@example.com)].
