# fmtransmitter
Procedure
1. download code from git. Open your Pi terminal and type this into the terminal

# https://github.com/mohangarapati/fmtransmitter

2. Open your Radio App on your phone or if you still have a functioning radio tune to 100Mhz and then in your terminal type  # sudo ./pifm sound.wav 100.0
# sudo ./pifm sound.wav 100.0 


If everything went well you should now be hearing Star Wars sound track in your radio tuning at 100 MHz. You can transmit any frequency within FM range just typing the frequency instead of 100.0.
 ## Connecting USB Microphone to Raspberry Pi




The Raspberry Pi comes with a 3.5mm analogue stereo audio output, but no input. As a radio amateur I am interested in using the Raspberry Pi as microphone to do this I need an audio input. This can be achieved by connecting a USB audio device to your Raspberry Pi.


Make sure your Raspberry Pi is turned off and insert the USB audio device into one of the USB sockets on the Raspberry Pi, and then power up your Raspberry Pi. The USB audio device should be automatically installed. Go in SSH or LXTerminal window and type the following and press Enter


# sudo apt-get install alsa-utils


You may already have this package on your system, but entering this command won't do any harm even if you do. This will install a package of ALSA utilities if you don't already have them (ALSA stands for Advances Linux Sound Architecture.

Now, You should make sure that the USB audio device is being detected by both the hardware and software. Enter the following command and press enter. 

# lsusb


This will display information regarding attached USB devices. As you can see, the last device listed in the screenshot (image 6) above is the USB audio device labelled as C-Media Electronics, Inc. Audio Adapter. So far, so good.

# Adjusting Volume

You can adjust the volume of your microphone by by an utility called alsamixer.
To start it, simply enter the name in the command line, like so:

# alsamixer


This presents a more graphical view (image 8,9,10) of the volume and information regarding the USB audio device. Using the arrow keys on your keyboard, select the volume column and adjust the volume higher or lower, dependent on your needs. Where possible, keep the volume level below 80–90% to avoid any distortion.

# Transmit Your Voice to FM Band

Our FM transmitter and Microphone setup is ready to transmit our voice. Here is the command you will use to start the broadcast. Each piece will be explained. Note that this command may need modified to work for your mic, just keep reading.



# arecord -fS16_LE -r 22050 -Dplughw:1,0 - | sudo ./pifm - 100.1 22050


Let, break the code snippet

arecord

Program we are using to record audio.

-fS16_LE

Output 16-bit data. Needed this way for PiFM to read it.

-r 22050

This specifies sampling rate to output recording. 22,050 is a good balance for speed and quality.

-Dplughw:1,0

to see all of the audio devices connected.

sudo ./pifm - 100.1 22050


Here sudo for root access, ./pifm run the FM module at '100.1' Mhz to transmit and '22050' is the sampling rate of the input. If you did everything right, after you run the command you should be able to tune your radio to 100.1 Mhz and hear yourself talking through the mic!
