# Natural-Sampling
## Aim 
To perform natural sampling by multiplying a message signal with a pulse train. To analyze the sampled signal and observe its reconstruction.
## Tools required 
- Personal Computer with Scilab
- Python IDE (Numpy)
## Program 
~~~
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Define message signal (low-frequency signal)
fs = 1000  # High sampling rate to represent original signal
t = np.arange(0, 1, 1/fs)
fm = 2  # Message signal frequency
message_signal = np.sin(2 * np.pi * fm * t)  # Message signal

# Define pulse train for natural sampling
fs_sampled = 20  # Sampling frequency
duty_cycle = 0.3  # Duty cycle of pulse (30% width)
pulse_train = np.zeros_like(t)
pulse_width = int(duty_cycle * (fs / fs_sampled))

# Generate pulse train
for i in range(0, len(t), fs // fs_sampled):
    pulse_train[i:i + pulse_width] = 1

# Natural sampled signal (Message signal × Pulse train)
sampled_signal = message_signal * pulse_train

# Reconstruction using sinc interpolation
reconstructed_signal = resample(sampled_signal, len(t))

# Plot Message Signal
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, label="Original Message Signal", color='b')
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Message Signal")
plt.legend()
plt.grid()
plt.show()

# Plot Natural Sampling
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, linestyle="dashed", alpha=0.7, label="Original Signal")
plt.plot(t, sampled_signal, 'r', label="Naturally Sampled Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Natural Sampling of Message Signal")
plt.legend()
plt.grid()
plt.show()

# Plot Reconstructed Signal
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, linestyle="dashed", alpha=0.7, label="Original Signal")
plt.plot(t, reconstructed_signal, 'g', label="Reconstructed Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Reconstruction from Natural Sampling")
plt.legend()
plt.grid()
plt.show()
~~~

## Output Waveform
![image](https://github.com/user-attachments/assets/e4e8ba77-146d-42f9-80fc-cf10ef993722)

![image](https://github.com/user-attachments/assets/21fd8f9b-792a-42de-a1ad-8007ab9a9790)

![image](https://github.com/user-attachments/assets/803487b2-6ce0-4a4f-8ddc-08fbff7f9d80)

## Results
Natural sampling was successfully performed by modulating the message signal with a pulse train. The reconstruction process demonstrated that a higher duty cycle improves signal recovery, while a lower duty cycle leads to distortion.

