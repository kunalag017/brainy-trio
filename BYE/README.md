# Brainy Trio Puzzle Hub

This repository contains a single-page web app (HTML/CSS/JS) that runs entirely in the browser.

## 🚀 Publish as a short public link (GitHub Pages)

The easiest way to get a **clean, short link** that anyone (including mobile phones) can open is to host this repo with **GitHub Pages**.

### 1) Create a GitHub repository
1. Go to https://github.com/new
2. Name it something like `brainy-trio` (or any name you like).
3. Do not initialize with a README (this repo already has one).

### 2) Push this project to GitHub
Run these commands from this folder (`c:\Users\y3kp2\BYE`):

```powershell
# If you haven't already configured Git, set your name/email once:
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Initialize & add files (if not already initialized)
git init

git add .
git commit -m "Initial site"

# Add the GitHub remote (replace with your repo URL)
git remote add origin https://github.com/<your-username>/<your-repo>.git

git branch -M main

git push -u origin main
```

### 3) Enable GitHub Pages
1. Go to your repo Settings → Pages.
2. Under **Source**, set it to `main` branch and folder `/ (root)`.
3. Save.

After a minute or two, your site will be live at:

```
https://<your-username>.github.io/<your-repo>/
```

### 4) Share the link
Now you can share that link with any mobile phone anywhere, and it will load the app instantly.

---

## 🧩 Local development
To preview locally:

```powershell
python -m http.server 8000
```

Then open: `http://localhost:8000`
