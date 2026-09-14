# Tonal Compass 🧭🎶

**Tonal Compass** is a real-time web application that listens through your microphone and estimates the musical key of live audio using pitch-class profile matching and the Krumhansl–Kessler key-finding algorithm.

![Tonal Compass](https://img.shields.io/badge/Web_Audio-API-blue)
![GitHub Pages](https://img.shields.io/badge/Deploy-GitHub_Pages-brightgreen)
![License](https://img.shields.io/badge/License-MIT-orange)

---

## ✨ Features

- 🎙️ **Real-time Microphone Analysis**: Captures live audio and extracts pitch-class profiles using high-resolution Web Audio API FFT analyzer nodes.
- 🎼 **Krumhansl–Kessler Tonal Profile Correlation**: Calculates Pearson correlation coefficients ($r$) against 24 standard major and minor key profiles.
- ⭕ **Interactive Circle of Fifths Wheel**: Visualizes live pitch-class energy distribution across all 12 chromas in real time.
- 🎹 **Diatonic Chord Grid**: Displays the 7 diatonic chords of the currently estimated key and dynamically highlights which chord matches the live audio signal best.
- 📈 **Trailing Window & Stability Engine**: Smooths out live guesses over a ~20s trailing window to provide a stable, reliable key estimate despite short breaks or solos.
- 🔊 **Verify-by-Ear Triad Synthesizer**: Play reference tonic triads directly in the browser to double-check candidate keys by ear.
- 🎯 **Relative Major/Minor Ambiguity Detection**: Flags relative major/minor pairs (e.g., C Major vs. A Minor) when their pitch profiles are mathematically close, guiding you on how to resolve them by ear.
- 🔒 **100% Client-side & Private**: All Web Audio processing runs locally in your browser — zero audio data is recorded or sent anywhere.

---

## 🚀 Quick Start & Local Development

No build step or dependencies required! Tonal Compass is built with vanilla HTML5, CSS3, and JavaScript (Web Audio API).

### Running locally:

Using Python:
```bash
python3 -m http.server 8000
```
Then open `http://localhost:8000` in your web browser.

Using Node `npx`:
```bash
npx serve .
```

> **Note**: Microphones require HTTPS or `localhost` context due to browser security restrictions (`getUserMedia`).

---

## 🌐 Deploying to GitHub Pages

This repository is pre-configured for GitHub Pages deployment.

### Option 1: Automatic Deployment via GitHub Actions (Recommended)

1. Push this repository to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/tonal-compass.git
   git push -u origin main
   ```
2. Go to your repository on GitHub -> **Settings** -> **Pages**.
3. Under **Build and deployment** -> **Source**, select **GitHub Actions**.
4. The workflow in `.github/workflows/deploy.yml` will automatically build and publish your site!

### Option 2: Classic Branch Deployment

1. Go to your repository **Settings** -> **Pages**.
2. Under **Source**, select **Deploy from a branch**.
3. Choose branch `main` (or `master`) and directory `/ (root)`.
4. Click **Save**.

---

## 🧠 How It Works

1. **Audio Signal Processing**: The browser's `AudioContext` captures microphone input with `echoCancellation: false` and `autoGainControl: false` for maximum harmonic fidelity.
2. **Chromagram Analysis**: Frequency bins from an $N=16384$ FFT are mapped to 12 pitch classes ($C, C\sharp, D, \dots, B$).
3. **Template Correlation**: A 12-element live chroma vector is compared via Pearson correlation ($r$) against Krumhansl–Kessler major and minor key profiles:
   $$\text{corr}(x, y) = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2 \sum (y_i - \bar{y})^2}}$$
4. **Candidate Ranking**: The top candidate key with the highest correlation coefficient is identified and plotted across the trailing timeline.

---

## 📄 License

[MIT License](LICENSE) © 2026
