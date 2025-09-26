## Purpose

This project allows you to control an LED strip remotely via the Arduino IoT Cloud. The strip can be turned on/off and its color changed, independent of the original manufacturer’s remote.

## Hardware

- **Arduino UNO R4 WiFi**  
- **IR LED** connected to pin **3** (IR_SEND_PIN)  
- LED strip (any NEC-compatible)

## How It Works

1. The sketch connects the Arduino to the Arduino IoT Cloud using a Thing named `"SmartHome"`.  
2. Two cloud variables are used:
   - `lED_on` (bool): controls whether the LED strip is on or off  (read/write)
   - `lED_Colour` (int): sets the color/command for the strip  (read/write)

3. When a cloud variable changes, the corresponding handler is called:
   - **`onLEDOnChange()`** — sends NEC codes to switch the strip on or off.  
   - **`onLEDColourChange()`** — sends NEC codes to change the color according to `lED_Colour`.

4. The **IRremote library** handles sending NEC codes to the LED strip. Make sure to use version 4.0 or newer!  

---

## Code 

```cpp
#include "thingProperties.h"
#include <IRremote.hpp> 
#define IR_SEND_PIN 3

void setup() {
  Serial.begin(115200);
  Serial.println(F("Ready to blast LED strip codes"));
  IrSender.begin(IR_SEND_PIN, ENABLE_LED_FEEDBACK, 2);
  initProperties();
  ArduinoCloud.begin(ArduinoIoTPreferredConnection);
}

void loop() {
ArduinoCloud.update();
  delay(10);
}

void onLEDOnChange()  {
  if (lED_on)
  {
    IrSender.sendNEC(0xEF00, 0x3, 0); 
    //delay(1000);
  }
  else {
    IrSender.sendNEC(0xEF00, 0x2, 0); 
    //delay(1000);
  }
}


void onLEDColourChange()  {
  Serial.println(F("Sending NEC code..."));
  IrSender.sendNEC(0xEF00, lED_Colour, 0);  // This HEX Code can vary. To find out which code you must use, execute Get_HEX_Code in the firmware file. 
  //delay(1000);
}



