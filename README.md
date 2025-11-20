# EVALUATION-OF-TIME-DIVISION-MULTIPLEXING

### Aim:
Study of TDM pulse amplitude modulation/ demodulation with transmitter block (clock) and channel identification information linked directly to the receivers.  

### Apparatus Required:

1)	Experimental kit DCL-02  
2)	Connecting chord  
3)	Power supply  
4)	20 MHz dual trace oscilloscope.  

### Theory:
In PAM, PPM the pulse is present for a short duration and for most of the time between the two pulses no signal is present. This free space between the pulses can be occupied by pulses from other channels. This is known as Time Division Multiplexing. Thus, time division multiplexing makes maximum utilization of the transmission channel. Each channel to be transmitted is passed through the low pass filter. The outputs of the low pass filters are connected to the rotating sampling switch (or) commutator.
It takes the sample from each channel per revolution and rotates at the rate of f s. Thus the sampling frequency becomes fs the single signal composed due to multiplexing of input channels. These channels signals are then passed through low pass reconstruction filters. If the highest signal frequency present in all the channels is fm, then by sampling theorem, the sampling frequency fs must be such that fs≥2fm. Therefore, the time space between successive samples from any one input will be  Ts=1/fs, and Ts =1/2fm.

### Procedure:

1)	Refer to the block diagram and carry out the following connections and switch setting. 
2)	Connect power supply in proper polarity DCL-02 and s it switch it on.  
3)	Connect 250hz, 500hz, 1khz and 2khz sine wave signals from the function generator to the multiplexer input channels CH0, CH1,CH3 by means of connecting chords.  
4)	Connect the multiplexer output txd of the transmitted section to the de multiplexer input rxd of the receiver section.  
5)	Connect the output of the receiver section CH0, CH1, CH2,CH3 to the IN0, IN1, IN2. IN3 of the filter section.  
6)	Connect the sampling clock TX CLK channel identification clock TXSYNC of the transmitter section to the corresponding RXCLK, RXSYNC of the receiver section respectively.  
7)	Set the amplitude of the input sine wave desired.   
8)	Take the observations as mentioned below.

### Kit Diagram
<img width="480" height="324" alt="image" src="https://github.com/user-attachments/assets/b2f8f171-ceff-4481-add2-bc4ef1c42506" />

## Program

t = linspace(0, 1, 1000);

fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));

for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));

for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;

cutoff_freq = 8 / (fs/2); 

h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));

for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
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

title('FDM Signal');

scf(3);

clf;

for i = 1:6
    
    subplot(3,2,i);
    
    plot(t, demux_signals(i, :));
    
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

### Model Graph
<img width="718" height="933" alt="image" src="https://github.com/user-attachments/assets/09c11b43-dc9c-4bf9-a04a-0728d0b0fea3" />

### Tabulation

![WhatsApp Image 2025-11-19 at 18 30 35_cf1f755e](https://github.com/user-attachments/assets/98654439-4358-4552-b08c-02c2599af086)

## Output

![WhatsApp Image 2025-11-19 at 18 31 55_a972b129](https://github.com/user-attachments/assets/9260f12c-fdd5-483b-ade2-12af7a6a14e2)

![WhatsApp Image 2025-11-19 at 18 32 17_f05874db](https://github.com/user-attachments/assets/8f5ec14b-918a-463c-8e07-009046ae221d)

### Result

Thus , the Frequency division multiplexing is done experimentally and output is verified.


