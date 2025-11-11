ESP8266 KeyMouse
===========================
Description
Supports acting as a WiFi hotspot or connecting to a WiFi network. Uses a WebSocket connection to send commands for simulating mouse, keyboard, and multimedia key functions.
On first boot, a red breathing light indicates it has entered SmartConfig mode (http://wx.ai-thinker.com/api/old/wifi/config).
After successful configuration, a blue breathing light activates upon a successful STA connection.
If the STA connection fails, a green breathing light will activate.
Basic Functions
Simulate mouse commands (CH9329)
Simulate keyboard commands (CH9329)
LED light control (WS2812)
Development Language
C++
Deployment Environment
ESP8266
Default Addresses
Connection Password (WifiKeyBoard/12345678)
192.168.4.1 HTTP 80
192.168.4.1 WebSocket 81
Hardware Communication Interface
System Setting Commands (start with @)
@INFO Returns device ID, AP IP, STA IP, firmware version, and company information.
@RSPWSSID:PASSWORD,timeout Sends SSID and PASSWORD. timeout is the connection timeout duration in ms, range 500~60000.
@CLAP Calls the interface to close the AP ----- About to be deprecated
#57ab00010003 Get hardware information, special key status, etc. ----- Deprecated
@CLDM60 Adjust mode 0-59
@CLDC65535 Set static color 000000 - FFFFFF
@CLDS1000 Set speed 0-65535
@CLDB127 Set brightness 0-254
@SAVE Save configuration
@CLSP Reset AP mode and restore client account/password to i5jie.com/12345678
@SCWF Search for WiFi signals, excluding its own AP name.
@SICR Set IC serial port return data. 0=Do not show details, 1=Return IC details.
@RBOT Reboot device.
@UOTA{#RKEY#} {#RKEY#} is the license system address upgrade key. Downloads and performs an upgrade from (http://license.i5jie.com/download/downloadbin?key=#RKEY#).
Chip Simplified Commands (start with $)
$SL02 Batch shortcut commands (CMD_SEND_KB_GENERAL_DATA) Legacy only, composed of batches of 8-byte data, the last byte is the checksum.
Test command: $SL0200001E000000000000000000000000001F00000000000000000000000000000020000000000000000000000000005D
$SL03 Batch shortcut commands (CMD_SEND_KB_GENERAL_DATA) Legacy only, composed of batches of 2-byte data, the last byte is the checksum.
Test command:
$SL04 Batch shortcut commands (CMD_SEND_KB_GENERAL_DATA) Legacy only, composed of batches of 7-byte data, the last byte is the checksum.
Test command:
$SL05 Batch shortcut commands (CMD_SEND_KB_GENERAL_DATA) Legacy only, composed of batches of 5-byte data, the last byte is the checksum.
Test command:
$QKKB Only supports individual key press operations from <Appendix 1 - "CH9329 Keycode Table"> in the <CH9329 Communication Protocol.pdf>.
Test command: $QKKB12345@163.com
Chip Native Commands (start with #)
Refer to the manual <CH9329 Communication Protocol.pdf> for details.
Connection Failure Error List (@RSPW)
255: WL_NO_SHIELD – A return value of 255 indicates no shield. The ESP8266 has built-in network functionality and does not require an extra shield, so this error generally does not occur.
0: WL_IDLE_STATUS – A return value of 0 indicates it is trying to connect.
1: WL_NO_SSID_AVAIL – A return value of 1 indicates the specified SSID network was not found.
2: WL_SCAN_COMPLETED – A return value of 2 indicates the network scan is complete.
3: WL_CONNECTED – A return value of 3 indicates a successful connection.
4: WL_CONNECT_FAILED – A return value of 4 indicates the connection failed.
5: WL_CONNECTION_LOST – A return value of 5 indicates the connection was lost.
6: WL_WRONG_PASSWORD – A return value of 6 indicates the wrong password was used.
7: WL_DISCONNECTED – A return value of 7 indicates it is disconnected.
-1: WiFi connection timeout.
Light Effect List (@CLDM)
0 Static - No flicker. Just a plain, old-fashioned static light.
1 Blink - Normal blinking. 50% on/off time.
2 Breathe - Performs the well-known "standby breathing" of i-Devices. Fixed speed.
3 Color Wipe - Lights up all LEDs one after another. Then turns them off in sequence. Repeats.
4 Color Wipe Inverse - Same as "Color Wipe," but with the on/off colors swapped.
5 Color Wipe Reverse - Lights up all LEDs one after another. Then turns them off in reverse sequence. Repeats.
6 Color Wipe Reverse Inverse - Same as "Color Wipe Reverse," but with the on/off colors swapped.
7 Color Wipe Random - Turns all LEDs to a random color in sequence. Then starts over with another color.
8 Random Color - Lights up all LEDs with one random color. Then switches them to the next random color.
9 Single Dynamic - Lights up each LED with a random color. Changes one or more random LEDs to a random color.
10 Multi Dynamic - Lights up each LED with a random color. Changes all LEDs to new random colors simultaneously.
11 Rainbow - All LEDs cycle through the rainbow at the same time.
12 Rainbow Cycle - Cycles a rainbow pattern across the entire LED strip.
13 Scan - A single pixel runs back and forth.
14 Dual Scan - Two pixels run back and forth in opposite directions.
15 Fade - Fades the lights in and (almost) out.
16 Theater Chase - Theater-style crawling lights. Inspired by the Adafruit example.
17 Theater Chase Rainbow - Theater-style crawling lights with a rainbow effect. Inspired by the Adafruit example.
18 Running Lights - Running lights effect with smooth sine transitions.
19 Twinkle - Flashes a few LEDs, resets, repeats.
20 Twinkle Random - Flashes several LEDs in random colors, resets, repeats.
21 Twinkle Fade - Flashes a few LEDs, then fades them out.
22 Twinkle Fade Random - Flashes a few LEDs in random colors, then fades them out.
23 Sparkle - Flashes one LED at a time.
24 Flash Sparkle - Lights up all LEDs in the selected color. Randomly flashes a single white pixel.
25 Hyper Sparkle - Sparkles like Flash Sparkle, but with more flashes.
26 Strobe - Classic strobe effect.
27 Strobe Rainbow - Classic strobe effect that cycles through the rainbow.
28 Multi Strobe - Strobe effect with different strobe counts and pauses, controlled by the speed setting.
29 Blink Rainbow - Classic blink effect that cycles through the rainbow.
30 Chase White - A color runs on a white background.
31 Chase Color - White running on a color background.
32 Chase Random - A random color running on a white background.
33 Chase Rainbow - White running on a rainbow background.
34 Chase Flash - A color with a white flash running.
35 Chase Flash Random - A white flash followed by a random color.
36 Chase Rainbow White - A rainbow running on a white background.
37 Chase Blackout - A black color running.
38 Chase Blackout Rainbow - A black color running on a rainbow background.
39 Color Sweep Random - Introduces alternating random colors from the start and end of the strip.
40 Running Color - Alternating running colored/white pixels.
41 Running Red Blue - Alternating running red/blue pixels.
42 Running Random - Randomly colored pixels running.
43 Larson Scanner - K.I.T.T.
44 Comet - A comet is fired from one end.
45 Fireworks - Fireworks sparks.
46 Fireworks Random - Randomly colored fireworks sparks.
47 Merry Christmas - Alternating running green/red pixels.
48 Fire Flicker - Fire flicker effect. Like a flame in a strong wind.
49 Fire Flicker (Soft) - Fire flicker effect. Slower/softer.
50 Fire Flicker (Intense) - Fire flicker effect. Wider range of colors.
51 Circus Combustus - Alternating running white/red/black pixels.
52 Halloween - Alternating running orange/purple pixels.
53 Bicolor Chase - Two LEDs running on a background color.
54 Tricolor Chase - Three alternating running colored pixels.
55 TwinkleFOX - Lights randomly fade in and out.
