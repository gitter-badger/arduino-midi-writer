<img src="docs/images/tft_emulator.png" width="200">

This folder contains source code for: 
* firm-ware of the ```teensy-midi-looper``` device 
* simulation code intended for development, debugging and testing on desktop computer  

#### structure
```arduino-midi-writer/Software```
  * ```arduino```
    * c++ abstractions and implementations which allow compiling arduino code for x86_64.
  * ```common```
    * library with classes which are common to arduino, and x86_64 
      * MidiLoopSequencer	
      * MidiWriter 
      * TFTPianoDisplay
  * ```x86```
    * application with test harness for x86_64 architecture

#### compatibilty for x86 / x64 / arm 
I am writing these c++ classes with compatibility for both x86 and arduino/teensy to allow me to debug the code without needing to upload the compiled binaries a microcontroller to test; 

(I am thinking about implementing some form of mock tft display for use when debugging locally on my x86 platform, perhaps using JUCE)  

#### build, run and test on x86/x64
* You need a x86/x64 compatible c++11 toolchain installed
  * x86_64 build system uses `cmake` https://cmake.org/
    * each directory contains a CMakeLists.txt file
    * running `cmake` will create a .Makefile 
    * build process can be triggered by running `make`
  * JetBrains CLion IDE
    * Very good integrated development environment. integrates very well with cmake.  
      
* to build for x86/x64
  * open terminal to arduino_midi_writer/Software
    * build arduino abstractions library (libarduino_abstraction.a)
    ```
    $cd arduino
    $mkdir cmake-build-debug
    $cd cmake-build-debug/
    cmake ..
    make
    ```
    * build common library (libteensy_midi_common.a)
    ```
    $cd ../../common/
    $mkdir cmake-build-debug
    $cd cmake-build-debug/
    cmake ..
    make
    ```  
    * build x86/x64 application (libarduino_abstraction.a)
    ```
    $cd ../../x86/
    $mkdir cmake-build-debug
    $cd cmake-build-debug/
    cmake ..
    make
    ```  
* to run
  * follow build instructions above
open terminal to arduino_midi_writer/Software/x86/cmake-build-debug/
  ```
  ./arduino_midi_writer
  ```
#### classes
  * MidiWriter.h
    * write simple midi events to SMF on SD card 
    * currently saves single track SMF (SMF type 0)
  * TFTPianoDisplay.h
    * display incomming midi note on/off messages on a piano keyboard view
  * MidiLoopSequencer.h (work in progress)
    * manage looping / recording / playing / event callbacks
  
#### dependencies
* arduino midi library 
  * https://github.com/PaulStoffregen/MIDI
* cppQueue 
  * https://github.com/SMFSW/Queue
* Arduino menu 
  * https://github.com/neu-rah/ArduinoMenu
* AdafruitGFX, Adafruit_ST7735
  * https://github.com/adafruit/Adafruit-GFX-Library 
  * https://github.com/adafruit/Adafruit-ST7735-Library
* https://github.com/mpaland/printf
