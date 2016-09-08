# arduino-library-audio
Arduino Audio Library for stm32 platform

_There is one Audio library for Arduino Due (https://github.com/arduino-org/Arduino/tree/master/libraries/Audio). This library has only three "commands"_

_1. begin_<br>
_2. prepare_<br>
_3. write_

_This commands are not sufficient for Audio Interface of Otto board because there are no commands to use the microphones and to select the output channel._

_For this reason we can use Processing Sound library: https://processing.org/reference/libraries/sound/_

# AUDIO API definition

## **AudioDevice**

- **Constructor:**
AudioDevice(theParent, sampleRate, bufferSize)

- **Description:**
Audio Device allows for configuring the audio server. If you need a low latency server you can reduce the buffer size. Allowed values are power of 2. For changing the sample rate pass the appropriate value in the constructor.

- **Example:**

      import processing.sound.*;
      AudioDevice myAudioServer;

      void setup() {
         myAudioServer = new AudioDevice(this, 44100, 128);
       }

       void loop() {
       }




## **AudioIn**

- **Constructor:**
AudioIn(theParent, in)

- **Description:**
Audio Device allows for configuring the audio server. If you need a low AudioIn let's you grab the audio input

- **Methods:**
 - __start()__: Starts the input stream.
 - __play()__: Start the Input Stream and route it to the Audio Hardware Output
 - __set()__:	 Set multiple parameters at once.
 - __amp()__: Change the amplitude/volume of the input steam.
 - __add()__: Offset the output of the input stream by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the input stream.

- **Example:**

      import processing.sound.*;
      AudioIn in;

      void setup() {

         // Create the Input stream
         in = new AudioIn(this, 0);
         in.play();
      }

      void loop() {
      }



## **SoundFile**

- **Constructor:**
SoundFile(theParent, path)

- **Description:**
This is a Soundfile Player which allows to play back and manipulate soundfiles. Supported formats are: WAV, AIF/AIFF, MP3.

- **Methods:**
 - __frames()__: Returns the number of frames/samples of the sound file.
 - __sampleRate()__: Returns the sample rate of the soundfile.
 - __channels()__: Returns the number of channels in the soundfile.
 - __duration()__: Returns the duration of the the soundfile.
 - __play()__: Starts the playback of a soundfile. Only plays the soundfile once.
 - __loop()__: Starts the playback of a soundfile to loop.
 - __jump()__: Jump to a specific position in the file while continuing to play.
 - __cue()__: Cues the playhead to a fixed position in the soundfile. Note that the time parameter supports only integer values.
 - __set()__: Set multiple parameters at once
 - __pan()__: Move the sound in a stereo panorama, only supports Mono Files
 - __rate()__: Change the playback rate of the soundfile.
 - __amp()__: Changes the amplitude/volume of the player.
 - __add()__: Offset the output of the player by given value
 - __stop()__: Stops the player

- **Example:**

      import processing.sound.*;
      SoundFile file;

      void setup() {

        // Load a soundfile from the /data folder of the
        // sketch and play it back
        file = new SoundFile(this, "sample.mp3");
        file.play();
      }

      void loop() {
      }



## **LowPass**

- **Constructor:**
LowPass(parent)

- **Description:**
This is a low pass filter.

- **Methods:**
 - __process()__: Start the filter
 - __stop()__: Stop the filter
 - __freq()__: Sets the cut off frequency for the filter

- **Example:**

       import processing.sound.*;

       WhiteNoise noise;
       LowPass lowPass;

       float amp=0.0;

       void setup() {

         // Create a noise generator and a bandpass filter
         noise = new WhiteNoise(this);
         lowPass = new LowPass(this);

         noise.play(0.5);
         lowPass.process(noise, 800);
       }

       void loop() {
       }



## **HighPass**

- **Constructor:**
 HighPass(parent)

- **Description:**
This is a high pass filter.

- **Methods:**
  - __process()__: Start the filter
  - __stop()__: Stop the filter
  - __freq()__: Sets the cut off frequency for the filter

- **Example:**

       import processing.sound.*;

       WhiteNoise noise;
       HighPass highPass;

       float amp=0.0;

       void setup() {

          // Create a noise generator and a bandpass filter
          noise = new WhiteNoise(this);
          highPass = new HighPass(this);

          noise.play(0.5);
          highPass.process(noise, 5000);
        }

        void loop() {
        }



## **BandPass**

- **Constructor:**
BandPass(parent)

- **Description:**
This is a high pass filter.

- **Methods:**
 - __process()__: Start the Filter
 - __set()__: Sets frequency and bandwidth of the filter with one method.
 - __freq()__: Set the cutoff frequency for the filter
 - __bw()__:Set the bandwidth for the filter.
 - __stop()__: Stops the filter.

- **Example:**

       import processing.sound.*;

       WhiteNoise noise;
       BandPass bandPass;

       float amp=0.0;

       void setup() {

       // Create a noise generator and a bandpass filter
       noise = new WhiteNoise(this);
       bandPass = new BandPass(this);

        noise.play(0.5);
        bandPass.process(noise, 100, 50);
       }

       void loop() {
       }



## **Delay**

- **Constructor:**
Delay(theParent)

- **Description:**
This is a simple Delay Effect.

- **Methods:**
 - __process()__: Start the delay effect
 - __set()__:  Set delay time and feedback values at once
 - __time()__: Changes the delay time of the effect.
 - __feedback()__: Change the feedback of the delay effect.
 - __stop()__: Stop the delay effect.

- **Example:**

       import processing.sound.*;

       AudioIn in;
       Delay delay;

       void setup() {

         // create the input stream
         in = new AudioIn(this, 0);

         // create a delay effect
         delay = new Delay(this);

         // start the input stream
         in.play();

         // Patch the delay
         delay.process(in, 5);
         delay.time(0.5);
       }

       void loop() {
       }



## **Reverb**

- **Constructor:**
Reverb(theParent)

- **Description:**
This is a simple Reverb Effect.

- **Methods:**
 - __process()__: Start the reverb effect.
 - __set()__: Set multiple parameters at once
 - __room()__: Change the room size of the reverb effect.
 - __damp()__: Change the dampening of the reverb effect
 - __wet()__: Change the dry/wet ratio of the delay effect
 - __stop()__: Stop the reverb effect

- **Example:**

       import processing.sound.*;

       AudioIn in;
       Reverb reverb;

       void setup() {

         // create the input stream
         in = new AudioIn(this, 0);

         // create a reverb effect
         reverb = new Reverb(this);

         // start the input stream
         in.play();
         reverb.process(in);
       }

       void loop() {
       }



## **Amplitude**

- **Constructor:**
Amplitude(theParent)

- **Description:**
This is a volume analyzer. It calculates the root mean square of the amplitude of each audio block and returns that value.

- **Methods:**
 - __input()__: Defines the audio input source of the amplitude analyzer.
 - __analyze()__: Queries a value from the analyzer and returns a float between 0. and 1.


- **Example:**

       import processing.sound.*;
       Amplitude amp;
       AudioIn in;

       void setup() {
         // Create an Input stream which is routed into the Amplitude analyzer
         amp = new Amplitude(this);
         in = new AudioIn(this, 0);
         in.start();
         amp.input(in);
       }

       void loop() {
         println(amp.analyze());
       }



## **FFT**

- **Constructor:**
FFT(theParent, fftSize)

- **Description:**
This is a Fast Fourier Transform (FFT) analyzer. It calculates the normalized power spectrum of an audio stream the moment it is queried with the analyze() method.

- **Methods:**
 - __input()__: Define the audio input for the analyzer.
 - __analyze()__: Queries a value from the analyzer and returns a vector the size of the pre-defined number of bands.


- **Example:**

       import processing.sound.*;

       FFT fft;
       AudioIn in;
       int bands = 512;
       float[] spectrum = new float[bands];

       void setup() {
         Serial.begin(9600)

         // Create an Input stream which is routed into
         // the Amplitude analyzer
         fft = new FFT(this, bands);
         in = new AudioIn(this, 0);

         // start the Audio Input
         in.start();

         // patch the AudioIn
         fft.input(in);
       }

       void loop() {
         fft.analyze(spectrum);

         for(int i = 0; i < bands; i++){
         // The result of the FFT is normalized
         // print the value for frequency i band
         Serial.println(spectrum[i]);
         }
      }



## **WhiteNoise**

- **Constructor:**
WhiteNoise(theParent)

- **Description:**
This is a White Noise Generator. White Noise has a flat spectrum.

- **Methods:**
 - __play()__: Start the generator
 - __set()__: Set multiple parameters at once.
 - __amp()__: Change the amplitude/volume of the generator
 - __add()__: Offset the generator by a given Value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the generator


- **Example:**

       import processing.sound.*;
       WhiteNoise noise;

       void setup() {
         // Create the noise generator
         noise = new WhiteNoise(this);
         noise.play();
       }

       void loop() {
       }



## **PinkNoise**

- **Constructor:**
PinkNoise(theParent)

- **Description:**
This is a Pink Noise Generator. Pink Noise has a decrease of 3dB per octave.

- **Methods:**
 - __play()__: Start the generator
 - __set()__: Set multiple parameters at once.
 - __amp()__: Change the amplitude/volume of the generator
 - __add()__: Offset the generator by a given Value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the generator


- **Example:**

       import processing.sound.*;
       PinkNoise noise;

       void setup() {
         // Create the noise generator
         noise = new PinkNoise(this);
         noise.play();
       }

       void loop() {
       }


## **BrownNoise**

- **Constructor:**
BrownNoise(theParent)

- **Description:**
This is a Brown Noise Generator. Brown Noise has a decrease of 6dB per octave.

- **Methods:**
 - __play()__: Start the generator
 - __set()__: Set multiple parameters at once.
 - __amp()__: Change the amplitude/volume of the generator
 - __add()__: Offset the generator by a given Value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the generator


- **Example:**

       import processing.sound.*;
       BrownNoise noise;

       void setup() {
         // Create the noise generator
         noise = new BrownNoise(this);
         noise.play();
       }

       void loop() {


## **SinOsc**

- **Constructor:**
SinOsc(theParent)

- **Description:**
This is a simple Sine Wave Oscillator.

- **Methods:**
 - __play()__: Starts the oscillator
 - __set()__: Set multiple parameters at once
 - __freq()__: Set the frequency of the oscillator in Hz.
 - __amp()	__: Set the amplitude/volume of the oscillator
 - __add()__: Offset the output of the oscillator by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()	__: Stop the oscillator.


- **Example:**

       import processing.sound.*;
       SinOsc sine;

       void setup() {
         // Create the sine oscillator.
         sine = new SinOsc(this);
         sine.play();
       }

       void loop() {
      }



## **SawOsc**

- **Constructor:**
SawOsc(theParent)

- **Description:**
This is a simple Sawtooth Wave Oscillator.

- **Methods:**
 - __play()__: Starts the oscillator
 - __set()__: Set multiple parameters at once
 - __freq()__: Set the frequency of the oscillator in Hz.
 - __amp()__: Set the amplitude/volume of the oscillator
 - __add()__: Offset the output of the oscillator by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the oscillator.

- **Example:**

       import processing.sound.*;
       SawOsc saw;

      void setup() {
         // Create sawtooth wave oscillator.
         saw = new SawOsc(this);
         saw.play();
        }

       void loop() {
       }



## **SqrOsc**

- **Constructor:**
SqrOsc(theParent)

- **Description:**
This is a simple Square Wave Oscillator.

- **Methods:**
 - __play()__: Starts the oscillator
 - __set()__: Set multiple parameters at once
 - __freq()__: Set the frequency of the oscillator in Hz.
 - __amp()__: Set the amplitude/volume of the oscillator
 - __add()__: Offset the output of the oscillator by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the oscillator.

- **Example:**

       import processing.sound.*;
       SqrOsc square;

      void setup() {
         // Create square wave oscillator.
         square = new SqrOsc(this);
         square.play();
        }

       void loop() {
       }



## **TriOsc**

- **Constructor:**
TriOsc(theParent)

- **Description:**
This is a simple Triangle Wave Oscillator.

- **Methods:**
 - __play()__: Starts the oscillator
 - __set()__: Set multiple parameters at once
 - __freq()__: Set the frequency of the oscillator in Hz.
 - __amp()__: Set the amplitude/volume of the oscillator
 - __add()__: Offset the output of the oscillator by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the oscillator.

- **Example:**

       import processing.sound.*;
       TriOsc tiangle;

      void setup() {
         // Create triangle wave oscillator.
         triangle = new TriOsc(this);
         triangle.play();
        }

       void loop() {
       }



## **Pulse**

- **Constructor:**
Pulse(theParent)

- **Description:**
This is a simple Pulse Oscillator.

- **Methods:**
 - __play()__: Starts the oscillator
 - __set()__: Set multiple parameters at once
 - __freq()__: Set the frequency of the oscillator in Hz.
 - __amp()__: Set the amplitude/volume of the oscillator
 - __add()__: Offset the output of the oscillator by given value
 - __pan()__: Move the sound in a stereo panorama
 - __stop()__: Stop the oscillator.

- **Example:**

       import processing.sound.*;
       Pulse pulse;

       void setup() {
         // Create and start the sine oscillator.
         pulse = new Pulse(this);

         //Start the Pulse Oscillator.
         pulse.play();
       }

       void loop() {
       }



## **Env**

- **Constructor:**
Env(theParent)

- **Description:**
This is a ASR Envelope Generator.

- **Methods:**

 - __play()__: Triggers the envelope

- **Example:**

       import processing.sound.*;

       TriOsc triOsc;
       Env env;

       float attackTime = 0.001;
       float sustainTime = 0.004;
       float sustainLevel = 0.3;
       float releaseTime = 0.4;

       void setup() {
          // Create triangle wave
         triOsc = new TriOsc(this);

         // Create the envelope
         env  = new Env(this);
       }

       void loop() {
       }

       void mousePressed() {
         triOsc.play();
         env.play(triOsc, attackTime, sustainTime, sustainLevel, releaseTime);
       }
