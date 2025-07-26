# PixelSonic
Text to Sound Communication using FSK Modulation
This project demonstrates the transmission of text data by converting it into an audible sound using Frequency-Shift Keying (FSK) modulation. It includes scripts to convert text to FSK-modulated sound, play it, and then decode the sound back into the original text. An additional feature uses speech recognition to capture spoken words, which are then transmitted as sound.

🚀 Features
Text to Sound: Converts any given string into an FSK-modulated audio waveform.

Sound to Text: Decodes an FSK-modulated waveform back into the original text.

Speech to Sound: Utilizes a microphone to capture speech, converts it to text, and then encodes it into an FSK-modulated sound.

Audio Enhancement (Optional): Includes imports for a deep learning-based audio enhancement model to improve audio quality, although the core logic does not depend on it.

🤔 How It Works
The core of the project is the modulation and demodulation of a signal.

Text to Binary: The input text is first converted into its binary representation using 8 bits for each character (ASCII).

FSK Modulation: A digital signal is generated where a '0' bit is represented by a low-frequency sine wave (FREQ_0) and a '1' bit is represented by a high-frequency sine wave (FREQ_1). These waves are concatenated to form a continuous audio waveform.

Transmission: The generated waveform is played as sound using the computer's speakers.

FSK Demodulation: To decode, the received waveform is processed in segments, one for each bit.

The dominant frequency in each segment is determined. The current implementation uses a zero-crossing rate calculation as a simple method to approximate the frequency.

Based on whether the dominant frequency is closer to FREQ_0 or FREQ_1, the segment is decoded as a '0' or a '1'.

Binary to Text: The resulting binary string is grouped into 8-bit chunks, which are then converted back to their corresponding ASCII characters to retrieve the original text.

📦 Modules
The provided code is structured into two main functionalities:

1. Text-to-Sound Conversion
This part takes a hardcoded string (e.g., "Hello World"), converts it to an FSK sound, plays it, and then decodes the generated waveform back to text to verify the process.

2. Speech-to-Sound Conversion
This script uses the microphone to listen for speech.

It uses the SpeechRecognition library to convert the spoken audio into a text string.

This text is then put through the same FSK modulation process as above.

Finally, it decodes the waveform to verify the transmission.

📋 Requirements
To run this project, you'll need Python 3 and the following libraries. You can install them using pip:

pip install numpy sounddevice scipy SpeechRecognition librosa torch soundfile deepfilternet

numpy: For numerical operations and creating the waveform.

sounddevice: To play and record audio.

scipy: Used for signal processing, specifically the Hilbert transform for demodulation.

SpeechRecognition: For converting speech to text (requires an internet connection for the Google Web Speech API).

pyaudio: A dependency for SpeechRecognition to access the microphone.

librosa, torch, soundfile, deepfilternet: These are imported for the df (DeepFilterNet) audio enhancement functionality.

⚙️ Usage
You can save the code from the notebook cells into two separate Python files (e.g., text_to_sound.py and speech_to_sound.py) or run them in a Jupyter Notebook.

Running the Text-to-Sound Script
Save the relevant code into a file named text_to_sound.py.

Run from the terminal:

python text_to_sound.py

You will hear a short burst of sound, and the console will display the original text, its binary form, and the decoded text.

Running the Speech-to-Sound Script
Save the relevant code into a file named speech_to_sound.py.

Make sure you have a working microphone.

Run from the terminal:

python speech_to_sound.py

When prompted with "Speak something...", say a short phrase.

The script will recognize the text, play it as FSK sound, and then print the decoded result.
💡 Future Improvements
Real-time Communication: The scripts could be adapted for a real-time, two-way communication system between two computers.

Error Correction: Implement error-checking and correction codes (like parity bits or checksums) to make the transmission more robust against noise.

GUI: A simple graphical user interface could be built to make the application more user-friendly.

Improved Demodulation: The current frequency detection is basic. A more robust method using a Fast Fourier Transform (FFT) on each segment would provide more accurate demodulation.
