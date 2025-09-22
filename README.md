
# Lab 1: Sampling and Reconstruction of Speech Signals 

This repository contains the implementation and analysis for a lab exercise focused on the fundamentals of digital speech processing, specifically signal sampling, reconstruction, and the source-filter model of speech production.

##  Aim

To study the sampling and reconstruction of speech signals at different sampling rates, evaluate reconstruction quality using zero-order hold and linear interpolation, and implement the source-filter model to analyze the effect of filtering, sampling, and reconstruction on speech quality.

---

## Part 1: Sampling & Reconstruction of a Natural Speech Signal 

This exercise demonstrates the effects of different sampling rates and reconstruction methods on a real speech signal.

### Methodology

1.  An original speech signal is loaded and its time-domain representation is plotted.
2.  The signal is downsampled to three different rates: **8 kHz**, **16 kHz**, and **44.1 kHz**.
3.  The signal is reconstructed from each sampled version using two methods:
    * **Zero-Order Hold** (nearest-neighbor interpolation)
    * **Linear Interpolation**
4.  The **Mean Squared Error (MSE)** is calculated between the original and each reconstructed signal to quantify the reconstruction accuracy.

### Results: Mean Squared Error (MSE)
<img width="773" height="327" alt="Screenshot 2025-09-22 at 12 34 47 PM" src="https://github.com/user-attachments/assets/28bc9e59-8f0e-4d6e-b976-ac0081dc640c" />
<img width="873" height="277" alt="Screenshot 2025-09-22 at 12 34 36 PM" src="https://github.com/user-attachments/assets/817ca999-75e0-47a5-894c-4c16c3d7ace7" />
<img width="873" height="62" alt="Screenshot 2025-09-22 at 12 34 16 PM" src="https://github.com/user-attachments/assets/6c37ce66-8496-47fd-b4c9-ce00a7aed28b" />

### Interpretation

* The consistently **low MSE values (~0.05)** across all tests indicate that the reconstructed signals remain very close to the original signal.
* At **8 kHz**, linear interpolation performs slightly better than zero-order hold. This is expected, as the smooth variations in a speech signal are better approximated by lines than by steps.
* At **16 kHz and 44.1 kHz**, both methods yield almost identical, minimal MSE. This demonstrates that when the sampling rate is well above the **Nyquist frequency** for speech (which is roughly 8 kHz, as most speech energy is below 4 kHz), reconstruction is nearly perfect and the choice of a simple interpolation method becomes less critical.

---

## Part 2: The Source-Filter Model of Speech Production 

This exercise implements a basic source-filter model to generate a synthetic voiced speech signal and analyzes how sampling rates affect its perceived quality and integrity.

### Methodology

1.  **Source Generation:** A glottal pulse train is created to simulate the periodic vibration of vocal cords for a voiced sound.
2.  **Filter Design:** An all-pole filter is designed to model the vocal tract's resonant frequencies, known as **formants**.
3.  **Synthesis:** The source signal is passed through the filter to generate the synthetic speech signal.
4.  **Analysis:** The synthesized signal is sampled at three different rates: **8 kHz**, **4 kHz**, and **2 kHz**.
5.  **Evaluation:** The signals are reconstructed, and the MSE is computed between the original synthetic signal and the reconstructed versions.

### Results: Mean Squared Error (MSE)
<img width="870" height="393" alt="Unknown" src="https://github.com/user-attachments/assets/0d2c0dc9-8269-4107-babb-9031e1cccd38" />



### Inference

* The source-filter model is **highly sensitive to the sampling rate**. The quality of the reconstructed signal degrades rapidly as the sampling rate decreases.
* At **8 kHz**, the MSE is relatively low. This rate is sufficient to capture the most critical vocal tract resonances (formants), preserving the core characteristics of the speech signal. This is considered telephone-quality speech.
* At **4 kHz**, the error increases tenfold. This is because a 4 kHz sampling rate has a Nyquist frequency of 2 kHz, which is too low to capture the higher-frequency formants essential for distinguishing between different vowel sounds. This results in significant loss of detail.
* At **2 kHz**, the error explodes. The Nyquist frequency is now 1 kHz, and the majority of the speech spectrum is lost to **aliasing**. The resulting signal is severely distorted and largely unintelligible.
* **Conclusion:** For intelligible speech, a sampling rate of at least **8 kHz** is necessary. For natural, high-fidelity speech, **16 kHz or higher** is required to accurately capture the full range of formants and harmonics.
