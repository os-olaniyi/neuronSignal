# NeuroTrans - Neurotransmitter Spike Classifier

A standalone desktop app for classifying acetylcholine nanotip exocytosis events as **Sharp-Spike** or **Complex-Spike**.

Upload a spreadsheet of spike measurements and get instant predictions - no Python, no installation, no setup required.

---

## Download

**[→ Download the latest release](https://github.com/os-olaniyi/neuronSignal/releases/latest)**

Click the link above, then download `neurtrans-mac.zip` from the Assets section.

> **Requires macOS 12 (Monterey) or later** · Apple Silicon and Intel both supported

---

## How to run

```bash
# 1. Unzip the downloaded file
unzip neurtrans-mac.zip

# 2. Enter the folder
cd neurtrans

# 3. Start the app
./neurtrans
```

The app starts a local server and **opens automatically in your browser** at `http://127.0.0.1:8000`.

Press `Ctrl+C` in the terminal to quit.

---

## First-run security warning (macOS Gatekeeper)

On the first launch, macOS will block the app because it is not signed with an Apple Developer certificate.

**To bypass this once:**

1. Right-click (or Control-click) the `neurtrans` file
2. Select **Open**
3. Click **Open** in the dialog

You will not be prompted again after this.

Alternatively, from the terminal:

```bash
xattr -d com.apple.quarantine neurtrans
./neurtrans
```

---

## What the app does

| Feature | Description |
|---------|-------------|
| **Batch upload** | Upload an Excel or CSV file and classify all spikes at once |
| **Manual entry** | Enter a single spike's parameters and get an instant prediction |
| **Results** | Predicted class, confidence score, and decision score per spike |
| **Model info** | View model performance metrics, parameters, and preprocessing pipeline |

---

## Input format

Your spreadsheet must contain the following columns (any column order):

| Column | Unit | Description |
|--------|------|-------------|
| t<sub>1/2</sub> [ms] | ms | Half-width of the spike |
| I<sub>max</sub> [pA] | pA | Peak current |
| Q [pC] | pC | Total charge (integral of the spike) |
| Rise<sub>(25–75)</sub> [ms] | ms | Rise time from 25 % to 75 % of peak |
| Fall<sub>(75–25)</sub> [ms] | ms | Fall time from 75 % to 25 % of peak |

> **Exact header names required** - the app expects these strings verbatim in your file header:
> `t1/2[ms]` · `Imax [pA]` · `Q [pC]` · `Rise(25-75)[ms]` · `Fall(75-25) [ms]`

Rows with missing or invalid values are skipped automatically and reported in the output.

---

## Model

The classifier is a Support Vector Machine (SVM) trained on log-space features derived from the five raw measurements above (Set-B feature set). It was developed and validated on acetylcholine nanotip exocytosis recordings at Chalmers University of Technology.

---

## Contact

For questions or bug reports, open an [issue](https://github.com/os-olaniyi/neuronSignal/issues) on this repository.
