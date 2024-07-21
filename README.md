# STM32F401CCU6_BlackPill
Contains test codes for each modules, solutions of popular issues

## ST-link v2

if your Stlink v2 (cheaper clone one) is not working and throwing these errors, here's how you can fix these issues:

**Error in initializing ST-LINK device. Reason: ST-LINK firmware upgrade required. Please upgrade the ST-LINK firmware using the upgrade tool.**

In stm32cubeIDE you will get this error along with stm32cubeIDE will ask you to upgrade. Press yes and upgrade window will open:

+ Detach your stlink from USB port and connect again
+ Scan for upgrad it will find your stlink, if not then scan again
+ once your stlink is found upgrade it by flashing the firmware


after closing the window try again to flash the code, it can through this error:

**Error in initializing ST-LINK device. Reason: No device found on target.**

Now you have to download the STlink utility software from stmicroelectronics official website, once downloaded do these:

+ Connect with your stlink by going to target and press connect
+ If throws an error detach your stlink and connect again
+ Press Boot0 button on stm32f401ccu6 to make it high (or in other board find boot0 pin and provide 3v)
+ While boot0 is high, press the reset button and release reset then boot0 button (remove 3v now)
+ Try connecting again and this time you will see some hex values (pre-loaded firmware in mcu)
+ Now again goto target and press "Erase Chip" this will make all the values as FFFF
+ you will see that stlink shows red and blue led color showing its ready to upload firmware into MCU
+ Now you can goto STM32CubeIDE again and flash the firmware


for successful download of firmware you will see these logs in console

**File download complete**
**Verifying ...**
**Download verified successfully**
**Shutting down...**
**Exit.**

## Debugger Configurations in STM32CubeIDE

In my case I have stlink v2 attached with black pill srm32f401ccu6, make sure for the following things:

+ stlink is correctly connected to board check 3v3, GND, CLK and DIO pins
+ Open the cap and verify of the mapped pins on the cover is correctly presented as its inside the stlink
+ For any issue related to stlink, go through the above stlink solutions
+ STlink should appear in device manager under USB Serial Bus section

After above stated verifications go to RUN, select run configurations,  window will pop up, press debugger and check for the following settings if not already set by default:

+ GDB Connections: Auto Start Local GDB server (bullet)
+ Debug probe: ST-LINK(ST-LINK GDB SERVER)
+ Interface : SWD
+ Reset Behaviour Type: Connection Under Reset

this should be it to get you started


## UART LOGS
***UART 1: PINS RX PA10 - TX PA9***

## BUILTIN LED
***GPIO OUT: PIN PC13***

## I2C COMMUNICATION
***I2C 1 : PINS CLK PB6 - SDA PB7***

**I2C Scanner**

That scans 0x01 till 0x7f 7 bit memory i2c addresses

**Added MLX GY-96014 - I2C Sensor**

Checks the device is ready at default bit shifted address of 5A<<1 
Read register for Temp at 0x06<<1 2 bytes
Converts the temperature into Celsius by shifting bits and arithemtic calculation