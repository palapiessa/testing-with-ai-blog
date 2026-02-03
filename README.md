
# Testing with AI and Beyond

Welcome to my personal blog! This repository hosts my thoughts and experiments on **AI in software testing**, automation, and related topics. Each post is written in Markdown and organized for easy navigation.

---

## 📂 Structure
- **docs/**  
  Contains all blog posts in Markdown format.  

- **docs/images**  
Stores images and diagrams used in blog posts.

## 🧪 Code Resources

- [2048 Fork for AI Testing](https://github.com/petria-tieto/2048)

## Setup

### 1. Clone the repos
- Clone this blog (`testing-with-ai-blog`) and the companion game repo (`2048`). Keep them side-by-side so the relative paths referenced in blog posts continue to work.

### 2. Open the 2048 game
- Open `2048/index.html` directly in your browser (double-click the file or drag it into the browser window). Because the project is a pure JS application, no extra server is required unless you prefer one.

### 3. Prepare the Python tooling with `uv`
- From the `2048` repo root create a virtual environment and install the shared dependencies for both the training script and the Flask service:
  ```bash
  cd 2048
  uv venv
  source .venv/bin/activate
  uv pip install numpy scikit-learn flask flask-cors
  ```
- (Optional) if you plan to rerun `train_offline.py`, install `stable-baselines3` as well:
  ```bash
  uv pip install stable-baselines3
  ```
- Start the Flask service (still from the repo root):
  ```bash
  RF_ALLOWED_ORIGINS=http://127.0.0.1:5500 PORT=5050 python service/model_server.py
  ```
  When loading the game from the local file system most browsers send a `null` origin; keeping `RF_ALLOWED_ORIGINS` set to `*` (the default) allows that. If you host the game on a specific origin, tighten the value accordingly.

### 4. Watch the model play
- With the Flask service running and the game page open, launch the browser console and run `autoplay.start()`. The autoplay script will send board states to the Flask service, get back moves, and drive the game automatically.

---

## ✅ License
Feel free to share and adapt the content under the terms of the LICENSE.

---

### 🔗 Connect
Follow me on https://www.linkedin.com/in/petrialapiessa/ for updates and discussions!

