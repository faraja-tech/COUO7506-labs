# Analysis Questions – Answers

## 1. What is the sampling rate of your phone recording?

From the Colab cell that loaded the uploaded MP3 with `librosa.load(filename, sr=None)`, the native sampling rate was printed as:

```
Sampling rate (fs): 48000 Hz
Audio shape: (340992,)
Duration: 7.104 seconds
```

So **fs = 48,000 samples/second = 48 kHz** (sampling interval Ts = 1/48000 ≈ 20.83 µs). The number of samples checks out: 340,992 / 48,000 = 7.104 s.

## 2. How many numbers are needed to store one minute of it in mono?

For a mono (one-channel) signal the number of samples is:

```
N = fs × duration = 48,000 samples/s × 60 s = 2,880,000 samples
```

So **2,880,000 numbers** are needed for one minute of mono audio.

Storage depends on how each number is represented:

- 16-bit PCM (standard WAV, 2 bytes/sample): 2,880,000 × 2 = **5,760,000 bytes ≈ 5.76 MB** (5.49 MiB)
- 32-bit float (as returned by `librosa`, 4 bytes/sample): 2,880,000 × 4 = **11,520,000 bytes ≈ 11.52 MB** (10.99 MiB)

(Stereo would require twice as many numbers.)

## 3. Why is a stem plot more appropriate than a continuous line for x[n]?

`x[n]` is a **discrete-time sequence**: it is defined only at integer values of `n`, and is undefined between them. A stem plot draws a separate stem at each integer index (with a baseline at zero), so it shows exactly which samples exist and their amplitudes. A continuous line connects the samples as if values existed at every non-integer time, which suggests an interpolated continuous-time waveform and can be misleading. Stems make the discreteness, individual sample positions, and zero-valued samples explicit — which is why the cells for δ(n), u(n), r(n) and aⁿu(n) use `ax.stem(...)`.

For a very long sequence such as the 340,992-sample recording, a continuous line is more practical to *display* the waveform, but that is only a plotting convenience; the underlying signal is still discrete.

## 4. For a = 1.1 (exponential growth), which system property would such a signal violate if it were an impulse response?

Consider `h[n] = (1.1)^n u[n]`. A discrete-time LTI system is **BIBO stable** (bounded input → bounded output) **if and only if its impulse response is absolutely summable**:

```
Σ |h[n]| < ∞
```

For `a = 1.1`:

```
Σ(n=0..∞) |1.1|^n  diverges   (because |a| = 1.1 > 1)
```

so the condition fails and the system is **not BIBO stable** — it violates the **stability** property. For example, with the bounded input `x[n] = u[n]`:

```
y[n] = Σ(k=0..n) (1.1)^k = (1.1^(n+1) − 1) / 0.1 → ∞
```

which grows without bound. By contrast, the plotted cases a = 0.5 and a = −0.8 are stable because |a| < 1, so their impulse responses decay and are absolutely summable.

(Note: `h[n] = (1.1)^n u[n]` is still **causal** since it is zero for n < 0; linearity and time-invariance are separate system properties. The property violated here is stability.)
