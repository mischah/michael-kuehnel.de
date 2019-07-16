---
layout: post
lang: en_GB
title: "How to flash ESP8266 (and ESP32) to use Espruino firmware on macOS"
date: 2019-07-16 23:34:16
category: IoT
tags: "IoT, Internet of Things, Espruino, ESP8266, ESP32, D1 Mini, NodeMCU, JavaScript, Microcontrollers, macOS"
image: ""
excerpt: "Espruino is firmware with a integrated JavaScript interpreter for microcontrollers coming with its own IDE. So it’s possible to run JavaScript natively on the most affordable microcontrollers like the ESP8266. This Guide helps you to set things up to explore the possibilities of the Internet of Things using the language of the web."
---

{{page.excerpt}}

## About Espruinos JavaScript abilities

Espruino sports a subset of ES6 features as shown in the [language feature](https://www.espruino.com/Features) list. You’ll find the comprehensive [API documentation](https://www.espruino.com/Reference#software) including built-in modules on the website as well.

The module system is similiar to CommonJS but you won’t be able to use the npm eco system. Learn more about Espruinos [modules](https://www.espruino.com/Modules).

## Espruino compatible microcontrollers

Espruino [sells](https://shop.espruino.com/espruino-boards) different own development boards with various hardware features that are specifically designed to work with this firmware. Fortunately, Espruino can also be used with other, much cheaper [boards](https://www.espruino.com/Other+Boards).

I recommend using a development board (D1 Mini or NodeMCU) based on the ESP8266 or ESP32 depending on your needs. The main difference (beside the size and the price) is that the ESP32 comes with Bluetooth 4.2 and Bluetooth low energy in addition to the WI-FI capabilities of the ESP32. See [this comparison](https://makeradvisor.com/esp32-vs-esp8266/) to make your choice.

## Install macOS drivers

Download and install one of the following drivers to be able to successfully connect your development board via USB to your Mac:

- [ESP8266](https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver)
- [ESP32](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

### Load and enable the extensions

Since macOS High Sierra you have to load and enable the drivers after the installation.

*Loading the ESP8266 driver in the Terminal:*

```bash
sudo kextload /Library/Extensions/usbserial.kext
```

*Loading the ESP32 driver in the Terminal:*

```bash
sudo kextload /Library/Extensions/SiLabsUSBDriver.kext
```

**Important:**  
After loading the driver you have to approve the usage by clicking the »Allow« button in the »Security & Privacy« system preferences panel.

## Install esptool

You need a command line tool called »esptool« to be able to flash your ESP based development board. You can get it via HomeBrew:

```bash
brew install esptool
```

## Flashing

Connect your ESP via USB to your Mac.

### Check connectivity

Enter the following to figure out if you verything is set up properly:

```bash
esptool.py flash_id
```

If the driver is correctly installed and activated your Terminal should respond with something like:

```markup
esptool.py v2.6
Found 5 serial ports
Serial port /dev/cu.wchusbserial1440
Connecting....
Detecting chip type... ESP8266
Chip is ESP8266EX
Features: WiFi
MAC: 84:f3:eb:ed:6d:54
Uploading stub...
Running stub...
Stub running...
Manufacturer: 68
Device: 4016
Detected flash size: 4MB
Hard resetting via RTS pin...
```

#### Port

`Serial port /dev/cu.wchusbserial1440` tells us which port to use for flashing the ESP and transfering code to it later..

*Note: Your port may differ.*

### Download firmware

Visit <http://www.espruino.com/Download> to get the latest Espruino release:

1. Choose your board (ESP32 respectively ESP8266)
1. Click the following link
    - for ESP8266:
      > Release: espruino_[latest-version]_esp8266_4mb/ (Directory)
    - for ESP32:
      > Release: espruino_[latest-version]_esp32/ (Directory)
1. Create a directory and download all files

### Erase your board

Enter the following to erase the flash of your board:

```bash
esptool.py --port /dev/<port> erase_flash
```

*Note: Replace `<port>` with your port.*

### Write firmware

*Note:*

- *Replace `<path/to/firmware>` with the directory directory containing the downloaded firmware files.*
- *Replace `<port>` with your port.*

#### ESP8266

```bash
$ cd <path/to/firmware>
$ esptool.py                                    \
    --port /dev/<port>             \
    --baud 115200                               \
    write_flash                                 \
    --flash_freq 80m                            \
    --flash_mode qio                            \
    --flash_size 32m                            \
    0x0000 boot_v1.6.bin                        \
    0x1000 espruino_esp8266_user1.bin           \
    0x3FC000 esp_init_data_default.bin          \
    0x3FE000 blank.bin
```

#### ESP32

```bash
$ cd <path/to/firmware>
$ esptool.py                                    \
    --chip esp32                                \
    --port /dev/<port>               \
    --baud 921600                               \
    --after hard_reset write_flash              \
    -z                                          \
    --flash_mode dio                            \
    --flash_freq 40m                            \
    --flash_size detect                         \
    0x1000 bootloader.bin                       \
    0x8000 partitions_espruino.bin              \
    0x10000 espruino_esp32.bin
```

## Testing aka Hello World

Horray, We should now be able to run JavaScript on the board 🎉

Let’s check if everythings works like expected:

1. Install the [Espruino Web IDE](https://www.espruino.com/Web+IDE)
1. Set the correct connection speed
    1. ESP8266: Settings → Communications → Baud Rate → 115200
    1. ESP32: Settings → Communications → Baud Rate → 921600
1. Hit the »connect« button in the upper left corner
1. Enter the following code to interact with the built in LED:

    ```javascript
    // ESP8266
    const pin = 2;
  
    // ESP32
    //const pin = 8;
  
    let on = 0;
    digitalWrite(pin, on);
    setInterval(() => {
      on = on === 0 ? 1 : 0;
      digitalWrite(pin, on);
    }, 100);
    ```

1. Hit the »Send to Espruino« button to transfer the code to your board

*Tip: See Espruinos [Quick Start](https://www.espruino.com/Quick+Start+Code) for writing code Espruino IDE to learn more.*

## Espruino CLI as alternative to using Espruino IDE

The Espruino CLI can be used to send the code your are writing with any code editor to your board. 

This way you can use the features of the IDE/editor you are used to when writing JavaScript.

## Install

```bash
npm install espruino -g
```

Enter `espruino -h` to see all available options.

## List all available devices and exit

```bash
espruino --list
```

## Useful snippets

*Note:*
*Replace `/dev/<port>` with your port and the baud rate from `115200` to `921600` when using an ESP32.*

### Reset the code on your board

```bash
espruino -p /dev/<port> -b 115200 -e 'reset(); digitalWrite(2, 1); save();
```

### Push code to board

```bash
espruino -p /dev/<port> -b 115200 filename.js
```

### Push code to board and save

```bash
espruino -p /dev/tty.wchusbserial14110 -b 115200 -e 'save()' filename.js
```

## Additional links

- <https://www.espruino.com/EspruinoESP8266>
- <https://www.espruino.com/ESP32>
- <https://www.espruino.com/Tutorials>
