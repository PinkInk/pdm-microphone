# pdm-microphon
Using PIO sample the MP34DT05-A PDM Microphone on the Arduino Nano RP2040 
Connect dev board.

Currently samples 256 bits (8 No. 4 byte words - conveniently the capacity of 
combined PIO RX & TX buffers) using PIO, counts the set-bits in this meta-sample 
and stores the result as a 1 byte PCM sample in the current of two 1kb double 
buffers using assembler.

Once each buffer is full a buffer_handler is queued as a soft irq to deal with
the samples.

As of now the buffer_handler is used to demonstrate the basic functionality and
hence 40kb of samples (around 3.5s) are written out to output.wav.  Because the 
sample and bit rate are fixed and no decimation or further processing is 
occuring the result is a 12kHz 8-bit mono audio file.

Audio quality is terrible and the noise ceiling is very high however, since 
voice is easily discernable and this is an early proof-of-concept I consider it
a "great success".

## References
https://www.st.com/resource/en/datasheet/mp34dt05-a.pdf

https://docs.arduino.cc/hardware/nano-rp2040-connect#resources

https://3cfeqx1hf82y3xcoull08ihx-wpengine.netdna-ssl.com/wp-content/uploads/2016/05/AN-000111-PDM-Decimation-v1.0.pdf