# esp32eforth
esp32eforth is derived from espForth_44 of esp8266 on arduino IDE by Chen-Hanson Ting.
esp32eforth is developed for esp32 wifiboy and NodeMCU 12E via arduino IDE by Derek Lai, Albert Lu, Sam Suan Chen, Chen-Hanson Ting.
<table width = "100%"><tr><td valign="middle"><center>
<img src="jpg/0010_wifiboy_front.jpg" width = "100%" alt="0010_wifiboy_front.jpg" align=center />
</td><td valign="middle"><center>
<img src="jpg/0020_wifiboy_back.jpg" width = "100%" alt="0020_wifiboy_back.jpg" align=center />
</td></tr>
<tr><td valign="middle"><center>
img01 wifiboyfront
</td><td valign="middle"><center>
img02 wifiboy back
</td></tr></table>

## arduino IDE
After nstalling arduino IDE, select File/New to create a new sketch with default name .
<table>
<tr><td valign="middle"><center>
<img src="jpg/0030_arduino_IDE_selectNew.jpg" width = "100%" alt="0030_arduino_IDE_selectNew.jpg" align=center />
</td><td valign="middle"><center>
<img src="jpg/0031_arduino_IDE_createNewSketch.jpg" width = "100%" alt="0031_arduino_IDE_createNewSketch.jpg" align=center />
</td></tr>
<tr><td valign="middle"><center>
img03 select New
</td><td valign="middle"><center>
img04 create New Sketch
</td></tr>
<tr><td valign="middle"><center>
<img src="jpg/0032_arduino_IDE_clearPasteAndSaveAs.jpg" width = "100%" alt="0032_arduino_IDE_clearPasteAndSaveAs.jpg" align=center />
</td><td valign="middle"><center>
<img src="jpg/0033_arduino_IDE_saveAs_esp32ef_11.jpg" width = "100%" alt="0033_arduino_IDE_saveAs_esp32ef_11.jpg" align=center />
</td></tr>
<tr><td valign="middle"><center>
img05 clear, copy, paste, and SaveAs
</td><td valign="middle"><center>
img06 saveAs esp32ef_11
</td></tr>
</table>

## ver 1
First derived from espForth_44 by Albert Lu, Sam Suan Chen, Chen-Hanson Ting on 22 sep 2017.
#### Modify esp8266 espForth_44.ino for esp32 wifiboy and NodeMCU 12E as esp32eforth.
    1. ignore WIFI and UDP
    2. ignore tone() since not yet implemented for ESP32.
    3. add input line echoing.
    4. modify COLD at the end to call .OK stead of CR.
    5. modify .OK to print one more space.
#### Try wifiboy led control line by line.
The back slash "\" and the left parenthesis "(" are comment words. All the messages after back slash and between parentheses will be ignored.

	\ to show all defined words, enter the following: 
	words

img_010 show_all_words

    \ to set wifiboy led pin as output direction (led on), enter the following:
    2 ( output ) 10 ( led pin gpio# in hex ) pinSel
    \ set led pin level high to turn off led.
    1 ( high ) decimal 16 ( led pin gpio# in decimal ) pinOut
    \ set led pin level low to turn on led.
    0 ( low ) 16 pinOut
    \ change number base to hexadecimal.
    hex
    \ define led as constant 0x10 (gpio #16).
    10 constant led
    \ define off as constant 0x1.
    1 constant high
    \ define on as constant 0x0.
    0 constant low
    \ define W to wait for a while.
    : wait FFFFF for next ;
    \ define off to turn off led.
    : off high led pinOut wait ;
    \ define on to turn on led.
    : on low led pinOut wait ;
    \ define blinks to blink given number of times.
    : blinks for aft on off then next ;
    \ blink 5 times.
    5 blinks
