# Factory Demo

[中文版本](./README_CN.md)

This example, based on [ESP_Brookesia](https://github.com/espressif/esp-brookesia), demonstrates an Android-like interface that includes many different applications. The example utilizes the development board's MIPI-DSI, MIPI-CSI, SD card slot, ESP32-C6, and audio interfaces. Based on this example, the ESP32-P4-Function-EV-Board can be used to experience the performance of the ESP32-P4.


## Getting Started


### Prerequisites

* An ESP32-P4-Function-EV-Board.
* A 7-inch 1024 x 600 LCD screen powered by the [EK79007](../../docs/_static/esp32-p4-function-ev-board/camera_display_datasheet/display_driver_chip_EK79007AD_datasheet.pdf) IC, accompanied by a 32-pin FPC connection [adapter board](../../docs/_static/esp32-p4-function-ev-board/schematics/esp32-p4-function-ev-board-lcd-subboard-schematics.pdf) ([LCD Specifications](../../docs/_static/esp32-p4-function-ev-board/camera_display_datasheet/display_datasheet.pdf)).
* A MIPI-CSI camera powered by the SC2336 IC, accompanied by a 32-pin FPC connection [adapter board](../../docs/_static/esp32-p4-function-ev-board/schematics/esp32-p4-function-ev-board-camera-subboard-schematics.pdf) ([Camera Specifications](../../docs/_static/esp32-p4-function-ev-board/camera_display_datasheet/camera_datasheet.pdf)).
* A USB-C cable for power supply and programming.
* Please refer to the following steps for the connection:
    * **Step 1**. According to the table below, connect the pins on the back of the screen adapter board to the corresponding pins on the development board.

        | Screen Adapter Board | ESP32-P4-Function-EV-Board |
        | -------------------- | -------------------------- |
        | 5V (any one)         | 5V (any one)               |
        | GND (any one)        | GND (any one)              |
        | PWM                  | GPIO26                     |
        | LCD_RST              | GPIO27                     |

    * **Step 2**. Connect the FPC of LCD through the `MIPI_DSI` interface.
    * **Step 3**. Connect the FPC of Camera through the `MIPI_CSI` interface.
    * **Step 4**. Use a USB-C cable to connect the `USB-UART` port to a PC (Used for power supply and viewing serial output).
    * **Step 5**. Turn on the power switch of the board.


### ESP-IDF Required

- This example supports ESP-IDF release/v5.3 and later branches. By default, it runs on ESP-IDF release/v5.3.
- Please follow the [ESP-IDF Programming Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html) to set up the development environment. **We highly recommend** you [Build Your First Project](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#build-your-first-project) to get familiar with ESP-IDF and make sure the environment is set up correctly.

### Get the esp-dev-kits Repository

To start from the examples in esp-dev-kits, clone the repository to the local PC by running the following commands in the terminal:

```
git clone --recursive https://github.com/espressif/esp-dev-kits.git
```


### Configuration

Run ``idf.py menuconfig`` and go to ``Board Support Package(ESP32-P4)``:

```
menuconfig > Component config > Board Support Package
```


## How to Use the Example


### Build and Flash the Example

Run `esptool.py --port PORT write_flash 0 p4_factory_v14_031.bin` to flash the project.

To exit the serial monitor, type ``Ctrl-]``.

See the [ESP-IDF Getting Started Guide](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html) for full steps to configure and use ESP-IDF to build projects.

### Note
To experience video playback, save MJPEG format videos on an SD card and insert the SD card into the SD card slot. **Currently, only MJPEG format videos are supported**. After inserting the SD card, the video playback app will automatically appear on the interface.

#### Video Format Conversion
* Install ffmpeg.
```
    sudo apt update
    sudo apt install ffmpeg
```
* Use ffmpeg to convert video.
```
   ffmpeg -i YOUR_INPUT_FILE_NAME.mp4 -vcodec mjpeg -q:v 2 -vf "scale=1024:600" -acodec copy YOUR_OUTPUT_FILE_NAME.mjpeg
```

### Example Output

- The complete log is as follows:

    ```c
    I (27) boot: ESP-IDF v5.4-dev-2166-g4eebfc4165 2nd stage bootloader
    I (28) boot: compile time Aug 13 2024 10:21:24
    I (28) boot: Multicore bootloader
    I (33) boot: chip revision: v0.1
    I (36) qio_mode: Enabling default flash chip QIO
    I (41) boot.esp32p4: SPI Speed      : 40MHz
    I (46) boot.esp32p4: SPI Mode       : QIO
    I (51) boot.esp32p4: SPI Flash Size : 16MB
    I (56) boot: Enabling RNG early entropy source...
    I (61) boot: Partition Table:
    I (65) boot: ## Label            Usage          Type ST Offset   Length
    I (72) boot:  0 nvs              WiFi data        01 02 00009000 00006000
    I (79) boot:  1 phy_init         RF data          01 01 0000f000 00001000
    I (87) boot:  2 factory          factory app      00 00 00010000 00900000
    I (94) boot:  3 storage          Unknown data     01 82 00910000 00400000
    I (102) boot:  4 model            Unknown data     01 82 00d10000 00200000
    I (109) boot:  5 fr               Unknown data     01 06 00f10000 00020000
    I (118) boot: End of partition table
    I (121) esp_image: segment 0: paddr=00010020 vaddr=48110020 size=42bb6ch (4373356) map
    I (881) esp_image: segment 1: paddr=0043bb94 vaddr=30100000 size=00020h (    32) load
    I (883) esp_image: segment 2: paddr=0043bbbc vaddr=30100020 size=0003ch (    60) load
    I (888) esp_image: segment 3: paddr=0043bc00 vaddr=4ff00000 size=04418h ( 17432) load
    I (900) esp_image: segment 4: paddr=00440020 vaddr=48000020 size=105730h (1070896) map
    I (1088) esp_image: segment 5: paddr=00545758 vaddr=4ff04418 size=1722ch ( 94764) load
    I (1109) esp_image: segment 6: paddr=0055c98c vaddr=4ff1b680 size=037f4h ( 14324) load
    I (1119) boot: Loaded app from partition at offset 0x10000
    I (1119) boot: Disabling RNG early entropy source...
    I (1131) hex_psram: vendor id    : 0x0d (AP)
    I (1131) hex_psram: Latency      : 0x01 (Fixed)
    I (1132) hex_psram: DriveStr.    : 0x00 (25 Ohm)
    I (1135) hex_psram: dev id       : 0x03 (generation 4)
    I (1141) hex_psram: density      : 0x07 (256 Mbit)
    I (1146) hex_psram: good-die     : 0x06 (Pass)
    I (1151) hex_psram: SRF          : 0x02 (Slow Refresh)
    I (1157) hex_psram: BurstType    : 0x00 ( Wrap)
    I (1163) hex_psram: BurstLen     : 0x03 (2048 Byte)
    I (1168) hex_psram: BitMode      : 0x01 (X16 Mode)
    I (1174) hex_psram: Readlatency  : 0x04 (14 cycles@Fixed)
    I (1180) hex_psram: DriveStrength: 0x00 (1/1)
    I (1185) MSPI DQS: tuning success, best phase id is 2
    I (1373) MSPI DQS: tuning success, best delayline id is 12
    I esp_psram: Found 32MB PSRAM device
    I esp_psram: Speed: 200MHz
    I (1374) mmu_psram: flash_drom_paddr_start: 0x10000
    I (1704) mmu_psram: flash_irom_paddr_start: 0x440000
    I (1787) hex_psram: psram CS IO is dedicated
    I (1788) cpu_start: Multicore app
    I (2112) esp_psram: SPI SRAM memory test OK
    W (2122) clk: esp_perip_clk_init() has not been implemented yet
    I (2128) cpu_start: Pro cpu start user code
    I (2129) cpu_start: cpu freq: 360000000 Hz
    I (2129) app_init: Application information:
    I (2132) app_init: Project name:     eui_demo
    I (2137) app_init: App version:      2f78502e-dirty
    I (2142) app_init: Compile time:     Aug 13 2024 10:21:13
    I (2148) app_init: ELF file SHA256:  7443ef054...
    --- Warning: Checksum mismatch between flashed and built applications. Checksum of built application is dea2628c204a0aed070c5d54306be1ab34e311fa13a058d4d045fe8d28559d3a
    I (2154) app_init: ESP-IDF:          v5.4-dev-2166-g4eebfc4165
    I (2160) efuse_init: Min chip rev:     v0.0
    I (2165) efuse_init: Max chip rev:     v0.99 
    I (2170) efuse_init: Chip rev:         v0.1
    I (2175) heap_init: Initializing. RAM available for dynamic allocation:
    I (2182) heap_init: At 4FF22CD0 len 000182F0 (96 KiB): RAM
    I (2188) heap_init: At 4FF3AFC0 len 00004BF0 (18 KiB): RAM
    I (2195) heap_init: At 4FF40000 len 00040000 (256 KiB): RAM
    I (2201) heap_init: At 50108080 len 00007F80 (31 KiB): RTCRAM
    I (2207) heap_init: At 3010005C len 00001FA4 (7 KiB): TCM
    I (2213) esp_psram: Adding pool of 23104K of PSRAM memory to heap allocator
    I (2221) spi_flash: detected chip: generic
    I (2226) spi_flash: flash io: qio
    I (2230) host_init: ESP Hosted : Host chip_ip[18]
    I (2263) H_API: ESP-Hosted starting. Hosted_Tasks: prio:23, stack: 5120 RPC_task_stack: 5120
    sdio_mempool_create free:23784316 min-free:23784316 lfb-def:23592960 lfb-8bit:23592960

    I (2269) gpio: GPIO[18]| InputEn: 0| OutputEn: 0| OpenDrain: 0| Pullup: 1| Pulldown: 0| Intr:0 
    I (2279) gpio: GPIO[19]| InputEn: 0| OutputEn: 0| OpenDrain: 0| Pullup: 1| Pulldown: 0| Intr:0 
    I (2288) gpio: GPIO[14]| InputEn: 0| OutputEn: 0| OpenDrain: 0| Pullup: 1| Pulldown: 0| Intr:0 
    I (2297) gpio: GPIO[15]| InputEn: 0| OutputEn: 0| OpenDrain: 0| Pullup: 1| Pulldown: 0| Intr:0 
    I (2307) gpio: GPIO[16]| InputEn: 0| OutputEn: 0| OpenDrain: 0| Pullup: 1| Pulldown: 0| Intr:0 
    I (2316) gpio: GPIO[17]| InputEn: 0| OutputEn: 1| OpenDrain: 0| Pullup: 0| Pulldown: 0| Intr:0 
    I (2326) H_API: ** add_esp_wifi_remote_channels **
    I (2331) transport: Add ESP-Hosted channel IF[1]: S[0] Tx[0x4800d500] Rx[0x4801a032]
    ...
    ```

## Troubleshooting

- Screen backlight dim: It might be due to poor soldering of the R12 resistor.
- Screen not lighting up: It could be due to a poor connection with the Dupont wire.
- Screen gradually turning white: It indicates that there is an issue with the screen ribbon cable..
- Unable to turn on the camera: This might be due to an improper connection of the camera FPC.

## Technical Support and Feedback

Please use the following feedback channels:

- For technical queries, go to the [esp32.com](https://esp32.com/viewforum.php?f=22) forum.
- For a feature request or bug report, create a [GitHub issue](https://github.com/espressif/esp-dev-kits/issues).

We will get back to you as soon as possible.
