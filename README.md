# 🍄 Autonomous Super Mario Bros (PPO + Custom Wrapper Stack)

An autonomous agent trained to play the original **Super Mario Bros (NES)** using Deep Reinforcement Learning. Unlike standard implementations, this project features a custom-built wrapper stack to process raw game frames and a patched environment pipeline to run legacy 2018 libraries on modern hardware.

## 📺 Demo: The "Brain View"
https://github.com/user-attachments/assets/a870173c-ca71-434a-908d-d1ef86d306f0


*Note: This video visualizes exactly what the AI sees—a grayscale, 84x84 pixel stream. By removing color and stacking 4 frames, the agent learns to perceive motion and velocity without unnecessary data overhead.*

## 🧠 Tech Stack
* **Language:** Python 3.10+ (Jupyter Notebook)
* **Frameworks:** Stable-Baselines3, Gym, NES-Py
* **Algorithm:** Proximal Policy Optimization (PPO) with CnnPolicy
* **Engineering:** Custom Wrapper Stack (Grayscale, Resize, Frame Stacking), NumPy 2.0 Compatibility Patches

## 🛠️ The Engineering Pipeline
To make the NES emulator compatible with modern RL algorithms, I engineered a data pipeline:
1.  **Raw Input:** 240x256 RGB Images (too complex for real-time processing).
2.  **Grayscale & Resize:** Downsampled to 84x84 grayscale (reduces dimensionality by ~90%).
3.  **Frame Stacking:** Stacked the last 4 frames into a single observation channel. This allows the CNN to "see" time (e.g., is Mario falling or jumping?).
4.  **Legacy Patching:** Manually patched the `nes_py` library to fix `uint8` memory overflows and injected `np.bool8` compatibility for NumPy 2.0 support.

## 💻 Usage
The project is contained entirely within the Jupyter Notebook, which handles the dependency patching automatically.

1.  Open `mario_agent.ipynb` in Google Colab or a local Jupyter environment.
2.  Run the cells sequentially to install dependencies, apply the library patches, and train the agent.
