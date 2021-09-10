# Sketch VIDOR FPGA Basic

This repository contains a basic file structure to upload a custom FPGA design
to the Arduino VIDOR 4000 FPGA EEPROM.

Code base comes from a [zip file](https://content.arduino.cc/assets/SketchVidorFPGA.zip)
inside the following [tutorial](https://www.arduino.cc/en/Tutorial/VidorGSVHDL).
It's a bit modified to make the process is easier.

    :warning: This code is not official nor fully tested. It has worked in the
    past but also start failing at loading without clear reason.

## Files

The following is a description of the files you must change:

* **app.h:** This is actually a `.ttf` file with the extension changed so it
  can be included later using the preprocessor. This is YOUR FPGA custom
  design file.
* **signature.h:** This is the signature of your design, it is usually printed
  by the program that converts the Quartus ttf file.
* **Sketch.ino:** This is the main Arduino program and it includes the other
  files of the folder. You can add more modules to it depending on your
  necessity.

The `defines.h` and `jtag` files should not need any modification. They contain
the basic code to load the design and initialize the FPGA.

## Conversion software

Bitstreams produced by Quartus (in ttf format) are not suitable to be directly
burned on the flash because their nibble encoding is reverse. You will find the
[make composite binary tool](https://github.com/vidor-libraries/VidorBitstream/tree/release/TOOLS/makeCompositeBinary)
inside the [VidorBitsream](https://github.com/vidor-libraries/VidorBitstream)
repository. Use this tool to reverse the Quartus ttf bits and obtain your
new ttf file (app.h) and design signature (signature.h).

## Loading the design

Once you have all your files ready, open the `Sketch.ino` using the Arduino IDE
and upload your design as you will normally do with any other Arduino.
