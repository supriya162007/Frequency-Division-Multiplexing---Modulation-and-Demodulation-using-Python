# Frequency-Division-Multiplexing---Modulation-and-Demodulation-using-Python

## Aim:

To generate an FDM signal by multiplexing multiple baseband message signals on different carrier frequencies, transmit (sum) them, optionally add channel noise, then recover each message by bandpass filtering and coherent demodulation in Python (Google Colab). Observe time & frequency domain signals and measure recovery quality.

## Apparatus Required:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

## Theory:

FDM places different message signals in separate, non-overlapping frequency bands by modulating each message onto a distinct carrier frequency. The multiplexed signal is the sum of all modulated channels. At the receiver, bandpass filters (or tuned filters) isolate each channel; then each isolated carrier is demodulated (coherently multiplied by a synchronized carrier) and low-pass filtered to recover the original baseband.

## Procedure:

1 — Imports and parameters

2 — Create message signals and carriers

3 — Modulate each message (standard AM DSB-SC) and form FDM signal

4 — Frequency domain (spectrum) of FDM signal

5 — (Optional) Add AWGN noise to FDM signal

6 — Receiver: isolate each channel with bandpass filter

7 — Demodulate each isolated channel (coherent) and low-pass filter to recover baseband

Program:
~~~

t = linspace(0, 1, 1000);

freqs = [5, 5.5, 6, 6.5, 7, 7.5];

signals = zeros(6, length(t));

for i = 1:6

signals(i, :) = sin(2 * %pi * freqs(i) * t);

end

fdm_signal = zeros(1, length(t));

for i = 1:6

fdm_signal = fdm_signal + signals(i, :);

end

demux_signals = zeros(6, length(t));

for i = 1:6

demux_signals(i, :) = fdm_signal .* sin(2 * %pi * freqs(i) * t);

end

scf(1);

clf;

for i = 1:6

subplot(3,2,i);

plot(t, signals(i, :));

title('Original Signal f=' + string(freqs(i)));

end

scf(2);

clf;

plot(t, fdm_signal);

title("FDM Signal");

scf(3);

clf;

for i = 1:6

subplot(3,2,i);

plot(t, demux_signals(i, :));

title('Demultiplexed Signal f=' + string(freqs(i)));

end
~~~
## Output:
### Modulated Signal
<img width="1280" height="688" alt="image" src="https://github.com/user-attachments/assets/95ac735c-242e-4b1d-a6e6-e1e7e0ea17ce" />
<img width="1280" height="695" alt="image" src="https://github.com/user-attachments/assets/4a3b2114-6812-473b-ac79-e804f237fa94" />

### Demodulated Signal
<img width="1280" height="688" alt="image" src="https://github.com/user-attachments/assets/95ac735c-242e-4b1d-a6e6-e1e7e0ea17ce" />

## Result:

FDM was successfully simulated. The six input signals were combined into one composite signal and later recovered correctly through demultiplexing using Scilab.
