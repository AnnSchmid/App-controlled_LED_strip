# Purpose

This section explains how to identify the HEX codes used by your LED strip’s remote control.

To use the provided script:

1. Connect the Arduino’s **DI2 pin** to an **IR receiver**.  
2. Aim the supplier’s remote at the IR receiver.  
3. Press any button on the remote.  

The **serial monitor** will display two codes:

- **Long code:** Shows the transmission format, such as which bits are inverted. This can vary depending on the LED strip manufacturer.  
- **Short code:** Represents the actual command value that will be used later to control the LED strip.

```cpp
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 2

void setup() {
  Serial.begin(115200);
  IrReceiver.begin(IR_RECEIVE_PIN, ENABLE_LED_FEEDBACK);
  Serial.println(F("Ready to receive IR signals..."));
}

void loop() {
  if (IrReceiver.decode()) {
    IrReceiver.printIRResultShort(&Serial);
    IrReceiver.printIRSendUsage(&Serial);
    IrReceiver.resume(); // prepare for next
  }
}

```
