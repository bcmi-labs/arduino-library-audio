# arduino-library-audio
Arduino Audio Library for stm32 platform

_There is one Audio library for Arduino Due (https://github.com/arduino-org/Arduino/tree/master/libraries/Audio). This library have only tre "commands"_

_1. begin_<br>
_2. prepare_<br>
_3. write_

_In my opinion this commands are not sufficient for Otto board audio interface, because there are no command to use the microphones and to select the output channel._

# AUDIO API definition
## _(First Proposal)_

#### **Audio.begin(_device_, _rate_, _size_):**
Initialize the Audio Device
* _**device**_: set the device to be initialized.
  * _STD_: initialize the onboard audio codec
  * _HDMI_: initilaize the HDMI audio codec
* _int **rate**_: sets the sample rate of the file to be reproduced or the acquisition datarate
* _int **size**_: is the size of audio buffer in milliseconds


#### **Audio.prepare(_buffer_, _samples_, _volumes_):**
Prepare the audio samples from the buffer and set the volumes
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of sample to play
* _int **volume**_: set the volume of the audio being played (value between 0 and 1023)


#### **Audio.play(_buffer_, _device_, _samples_):**
Write audio data from a buffer to a given device
* _long **buffer**_: is the buffer containing the audio samples
* _**device**_: select the output device
  * _HPOUT_: select the audio jack microphones
  * _SPKOUT_: select the pin header audio output connector
  * _HDMI_: select the HDMI audio output
* _int **samples**_: is the number of sample to play


#### **Audio.rec(_buffer_, _device_, _samples_):**
Read audio from a given input source and put the data in a given buffer
* _long **buffer**_: is the buffer containing the audio samples
* _**device**_: select the input device
  * _STDMIC_: select the onboard microphones connected to onboard codec
  * _MCUMIC_: select the onboard microphones connected to MCU
  * _EXTMIC_: select the audio jack microphones
* _int **samples**_: is the number of samples to record


### **Audio.pause(_device_):**
Pause the audio reproduction for a given output device
* _**device**_: select the device
  *  _STD_:  onboard audio codec
  * _HDMI_: HDMI audio codec


### **Audio.stop(_device_):**
Stop the audio reproduction for a given output device
* _**device**_: select the device
  * _STD_:  onboard audio codec
  * _HDMI_: HDMI audio codec


## Remarks:

Francesco Alessi: This proposal, in my opinion is better than the second, because the command are the same for all devive, and is possible to use one or another changing one argument.


## _(Second Proposal)_

### **Audio.begin(_rate_, _size_):**
Initialize the onboard Audio Codec
* _int **rate**_: sets the sample rate of the file to be reproduced or the accquisition datarate
* _int **size**_: is the size of audio buffer in milliseconds

### **AudioHDMI.begin(_rate_, _size_):**
Initialize the HDMI Audio Codec
* _int **rate**_: sets the sample rate of the file to be reproduced or the accquisition datarate
* _int **size**_: is the size of audio buffer in milliseconds


### **AudioMCU.begin(_rate_, _size_):**
Initialize the onboard codec and use the onboard microphones connected to MCU
* _int **rate**_: sets the sample rate of the file to be reproduced or the accquisition datarate
* _int **size**_: is the size of audio buffer in milliseconds

### **Audio.prepare(_buffer_, _samples_, _volumes_):**
Prepare the audio samples from the buffer and set the volumes for onboard codec
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to play
* _int **volume**_: set the volume of the audio being played (value between 0 and 1023)

### **AudioHDMI.prepare(_buffer_, _samples_, _volumes_):**
Prepare the audio samples from the buffer and set the volumes for HDMI codec
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to play
* _int **volume**_: set the volume of the udio being played (value between 0 and 1023)

### **Audio.play(_buffer_, _samples_):**
Write audio data from a buffer to the Audio jack
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to play

### **Audio.playSpk(_buffer_, _samples_):**
Write audio data from a buffer to the Audio pin header connectors
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to play

### **AudioHDMI.play(_buffer_, _samples_):**
Write audio data from a buffer to the HDMI Audio
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to play

### **Audio.rec(_buffer_, _samples_):**
Read audio from onboard microphones connected to Audio Codec and put data into a given buffer
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to record

### **Audio.recExt(_buffer_, _samples_):**
Read audio from external microphone connected to Audio jack and put data into a given buffer
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to record

### **AudioMCU.rec(_buffer_, _samples_):**
Read audio from onboard  microphones connected to MCU and put data into a given buffer
* _long **buffer**_: is the buffer containing the audio samples
* _int **samples**_: is the number of samples to record

### **Audio.pause():**
Pause the audio reproduction for audio jack and pin header audio connector

### **AudioHDMI.pause():**
Pause the audio reproduction for HDMI audio Device

### **Audio.stop():**
Stop the audio reproduction for audio jack and pin header audio connector

### **AudioHDMI.stop():**
Stop the audio reproduction for HDMI audio Device


###Remark:
