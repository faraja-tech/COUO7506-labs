# COUO7506-labs

Discrete-time signals lab work completed in Google Colab.

## Contents

- `Discrete_Time_signal_Assignment.ipynb` — Colab notebook with the signal-generation plots, voice-recording analysis (waveform and spectrogram), and the analysis answers.
- `analysis_questions.md` — standalone copy of the analysis answers.
- `Record (online-voice-recorder.com).mp3` — the uploaded voice recording analysed in the notebook (48 kHz, 7.104 s).

## Analysis questions

1. **Sampling rate of the phone recording:** 48,000 Hz (48 kHz), read from `librosa.load(..., sr=None)` in the notebook. The uploaded clip is 340,992 samples = 7.104 s.
2. **Numbers for one minute in mono:** `48,000 × 60 = 2,880,000` samples. That is 5,760,000 bytes (≈5.76 MB) at 16-bit PCM, or 11,520,000 bytes (≈11.52 MB) as 32-bit float.
3. **Stem plot vs continuous line:** `x[n]` exists only at integer `n`; stems show the individual samples and make the discrete nature explicit, while a connecting line implies values between samples.
4. **`a = 1.1` as an impulse response:** `h[n] = (1.1)^n u[n]` is not absolutely summable, so it violates **BIBO stability**. A bounded input such as `u[n]` produces an unbounded output.

See `analysis_questions.md` for full working and explanations.
